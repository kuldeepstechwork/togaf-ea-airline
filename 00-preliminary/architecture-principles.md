# Architecture Principles

These principles were ratified by the Halvern Air Architecture Review Board (ARB) during the Preliminary Phase and govern every subsequent architecture decision in this program. Each follows the standard TOGAF principle format: Name, Statement, Rationale, Implications. Principles are numbered for traceability from later decisions (see ADRs and Phase G architecture contracts, which cite these by number).

---

### 1. PSS Remains System of Record for Booking and Ticketing

**Statement:** The existing Passenger Service System (reservations, inventory, departure control) remains the authoritative system of record for confirmed bookings, ticket documents, and check-in/boarding state until a formal, separately governed decision replaces it.

**Rationale:** A full PSS replacement carries multi-year timelines and revenue-critical cutover risk that the NDC deadline does not allow for. Treating the PSS as stable ground lets retailing and distribution modernize independently.

**Implications:** New retailing and offer-management components must be built to read from and reconcile with the PSS, not to replace its record-keeping functions. Any future PSS replacement is a distinct, separately chartered program.

---

### 2. Offer and Order Are First-Class Architectural Concepts, Distinct from the Booking Record

**Statement:** "Offer" (a priced, bundled proposition made to a shopper) and "Order" (a confirmed commercial agreement, per the IATA ONE Order model) are modeled as first-class domain entities, separate from the legacy PNR/booking record, even while the PSS remains system of record for the underlying booking.

**Rationale:** The legacy PNR model cannot express bundles, dynamic pricing, or ancillary-inclusive fares. Bolting NDC fields onto the PNR schema perpetuates the constraint the program exists to remove.

**Implications:** Requires a new data domain and a reconciliation layer between offer/order and PNR (see ADR-003). Downstream systems (revenue accounting, loyalty) must eventually consume order data, not PNR data, as the source of commercial truth.

---

### 3. Distribution Channels Are Decoupled from Fare Filing Mechanics

**Statement:** Channel-facing systems (NDC API, GDS edge, direct/web) consume a common internal offer construction service; no channel integrates directly against PSS fare tables.

**Rationale:** Direct channel-to-PSS coupling is why every past channel addition at Halvern has taken 6+ months of custom integration. A common offer layer amortizes that cost across all channels, present and future.

**Implications:** All new channel integrations (including future ones not yet identified) are required to go through the retailing platform's offer API. Legacy GDS distribution continues via existing EDIFACT interfaces until formally retired.

---

### 4. Buy Before Build, Except at the Point of Competitive Differentiation

**Statement:** For undifferentiated capability (NDC schema handling, GDS/EDIFACT connectivity, standard IATA messaging), Halvern buys and configures commercial or open-source software. Custom build is reserved for offer construction logic that encodes Halvern's specific commercial strategy (bundling rules, dynamic pricing policy, loyalty integration).

**Rationale:** Halvern's engineering organization is sized for an airline of this scale, not for maintaining a bespoke NDC stack. Differentiation should be spent on pricing/retailing logic that competitors cannot buy off the shelf, not on standards compliance.

**Implications:** Vendor evaluation (Phase E) is mandatory before any build decision on infrastructure-layer capability. Custom build requires an ARB waiver citing this principle.

---

### 5. Every Integration Assumes Eventual Consistency, Never Assumes a Single Transaction Boundary

**Statement:** No architecture component may assume synchronous, single-transaction consistency across the PSS and the new retailing/loyalty platforms. All cross-system state changes are designed for eventual consistency with explicit reconciliation and compensation logic.

**Rationale:** The PSS was never designed to participate in distributed transactions with modern platforms. Pretending otherwise produces brittle integrations that fail silently under load — precisely the failure mode Halvern's current bolt-on loyalty system exhibits today.

**Implications:** Every integration design must specify its reconciliation window, idempotency strategy, and failure/compensation path. "It'll usually be consistent" is not an acceptable design statement in any ARB submission.

---

### 6. Loyalty Ledger Entries Are Immutable and Event-Sourced

**Statement:** Point accrual and redemption are recorded as an append-only, immutable event log; current balance is always a derived projection, never a directly mutated field.

**Rationale:** The current bolt-on loyalty system stores only current balance, which makes disputes, fraud investigation, and real-time accrual essentially impossible to reconcile. An auditable event history is a prerequisite for real-time redemption at point of sale.

**Implications:** Requires a new ledger store and event-sourcing discipline from any team building against loyalty (see ADR-004). Increases initial storage and query complexity in exchange for auditability and real-time capability.

---

### 7. Security and PCI Scope Is Minimized by Design, Not Retrofitted

**Statement:** Payment card data handling is isolated to a certified payment boundary from day one of any new component design; no new service is permitted to persist or log raw cardholder data even temporarily.

**Rationale:** Halvern's existing PCI DSS scope is already costly to audit because payment touchpoints are scattered across legacy systems. Every new component is an opportunity to shrink that scope, not add to it.

**Implications:** All new retailing and offer components must integrate with the existing tokenized payment boundary rather than handling card data directly. ARB reviews explicitly check PCI scope impact on every submission touching payment.

---

### 8. Architecture Decisions Are Recorded and Reversible by Default

**Statement:** Every architecturally significant decision is documented as an ADR with alternatives considered and consequences stated; decisions are treated as reversible unless explicitly marked otherwise, with the cost of reversal stated at decision time.

**Rationale:** A program spanning 24+ months and multiple vendor and delivery teams will lose institutional memory of *why* a decision was made unless it's written down. Treating decisions as reversible-by-default avoids premature lock-in.

**Implications:** No architecture contract (Phase G) may reference an undocumented decision. ADRs are reviewed at each ARB cadence for continued validity (see governance-framework-setup.md).

---

### 9. Regulatory and Standards Compliance Is Non-Negotiable, Implementation Detail Is Not

**Statement:** Conformance to IATA NDC schema versions, PCI DSS, and applicable data protection law (e.g., regional passenger data residency rules) is mandatory and out of scope for trade-off discussion; *how* Halvern implements conformance is open to architectural judgment.

**Rationale:** Distinguishing "must comply" from "how we comply" keeps governance debates focused on implementation trade-offs rather than re-litigating whether compliance is required.

**Implications:** Technology standards (Phase D) name specific NDC schema versions as mandatory floors. Exceptions process (see technology-standards.md) applies only to implementation choices, never to the compliance requirement itself.

---

### 10. New Components Are Built for Multi-Channel Reuse, Not Single-Channel Delivery

**Statement:** No new retailing or distribution component is approved for a single consuming channel; every component must have a stated reuse path across at least two of {NDC API, direct/web, GDS edge, call center}.

**Rationale:** Halvern's legacy landscape is a graveyard of single-channel integrations that now require duplicate maintenance. This principle exists specifically to stop that pattern from recurring in the new architecture.

**Implications:** Solution building blocks (Phase E) must document their multi-channel consumption model. A single-channel proposal requires an explicit ARB waiver with a stated remediation plan.

---

### 11. Data Ownership Is Assigned to Exactly One System per Domain

**Statement:** For each data domain (PNR, Offer, Order, Loyalty Ledger, Customer Profile), exactly one system is designated as owner/system-of-record; all other systems hold read-only replicas or derived views.

**Rationale:** Halvern's current landscape has customer profile data independently maintained in four systems with no reconciliation, which is a direct cause of loyalty data quality complaints. Ambiguous ownership does not scale past two integrated systems.

**Implications:** Data architecture (Phase C) must explicitly name the owning system for every domain. Any component proposing to write to a domain it does not own requires ARB approval and a stated synchronization contract.

---

### 12. Architecture Scales Down as Well as Up

**Statement:** Reference architectures and standards must remain viable for Halvern's actual scale (~120 aircraft, ~9M passengers/year) and must not default to hyperscale patterns whose operational overhead exceeds their benefit at this scale.

**Rationale:** Off-the-shelf reference architectures are frequently authored for airlines an order of magnitude larger. Adopting them wholesale would burden a mid-size carrier's engineering team with operational complexity it cannot staff.

**Implications:** Every reference architecture decision (Phase D) must include a stated rationale for why the chosen pattern fits Halvern's scale, and an explicit statement of the scale at which the pattern should be reconsidered.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
