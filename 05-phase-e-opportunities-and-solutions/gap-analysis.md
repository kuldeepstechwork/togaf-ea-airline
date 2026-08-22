# Gap Analysis

## Method

Gaps are derived directly from the capability-map.md maturity deltas, cross-referenced against the as-is/to-be business and information systems architectures. Each gap is prioritized using a simple High/Medium/Low scale weighted by business impact (from vision-and-scope.md success metrics) and delivery risk/complexity, then sequenced into the migration roadmap.

## Prioritized Gap Register

| Gap | Capability Area | Business Impact | Delivery Complexity | Priority | Addressed By |
|---|---|---|---|---|---|
| No NDC-conformant distribution capability exists | NDC Distribution | High — direct compliance/deadline driver | High — new gateway, schema conformance, certification | **Critical** | NDC API Gateway SBB, Wave 1 |
| No bundled offer construction at point of sale | Offer Bundling | High — primary ancillary revenue driver | High — new offer domain, rules engine integration | **Critical** | Offer Construction Service SBB, Wave 1-2 |
| Loyalty accrual/redemption is batch-only | Real-Time Loyalty | High — blocks partner integrations, customer experience | High — new event-sourced ledger, real-time balance projection | **Critical** | Loyalty Ledger Service SBB, Wave 2 |
| No structured Order data model | Order Management | Medium-High — prerequisite for offer/order flow and reconciliation | Medium — vendor product exists, mainly configuration | **High** | Order Management Service SBB, Wave 1-2 |
| PNR/Order reconciliation mechanism does not exist | Data Architecture | High — without it, dual-model operation is unmanageable | High — Halvern-specific, no vendor product fits | **Critical** | Reconciliation Service SBB, Wave 1 (earliest start, longest lead time) |
| Channel onboarding is bespoke per partner | Channel Onboarding | Medium — cost/speed driver, not a hard deadline blocker | Medium — largely solved by gateway architecture | **Medium** | NDC API Gateway configuration model, Wave 2-3 |
| No dynamic/personalized pricing capability | Dynamic Pricing | Medium-High — secondary ancillary/yield driver | Medium — rules engine is vendor-provided, rules authoring is new organizational skill | **High** | Rules Engine SBB + Revenue Management enablement, Wave 2 |
| Customer profile fragmented across 4 systems | Customer Profile | Medium — data quality, not a program-blocking gap | Low-Medium — scoped to read-only consolidated view only | **Low** (partial fix only, deliberately) | Customer Profile Consolidated View SBB, Wave 3 |
| No formal architecture governance body existed prior to program | Architecture Governance | High — enables/de-risks everything above | Low — organizational, not technical | **Critical** (already addressed) | ARB stood up in Preliminary Phase, prior to this register |
| PCI scope not assessed for new components | Security | High — regulatory/compliance risk if unaddressed | Medium | **High** | Security architecture review, concurrent with Wave 1 |

## Gaps Explicitly Not Prioritized for Closure in This Program

Consistent with the scope boundaries in vision-and-scope.md, the following gaps were identified during discovery but are **deliberately not sequenced into this program's roadmap**:

- **Full customer profile system-of-record consolidation** — the fragmentation gap is real, but closing it fully requires touching contact center CRM and web identity systems outside this program's chartered scope; a full fix is recommended as a distinct future initiative, and this program delivers only a partial, read-only mitigation.
- **PSS core inventory/reservations modernization** — as established in reference-architecture.md, this program's pattern deliberately does not touch PSS core capability; any gap in PSS core functionality itself is out of scope by design, not by oversight.
- **Revenue management pricing science (elasticity modeling, forecasting)** — the rules *engine* is in scope; the pricing *science* that would populate sophisticated dynamic pricing rules is explicitly excluded, per vision-and-scope.md, and left to a separate Commercial-led initiative.

## How This Feeds Phase F

The three "Critical" gaps with the longest lead times and highest Halvern-specific delivery risk — NDC API Gateway, Offer Construction, and Reconciliation Service — anchor Wave 1 of the migration roadmap specifically because delaying them delays everything downstream; the "Medium" and "Low" priority gaps are deliberately sequenced into later waves where their lower urgency accepts a longer wait in exchange for reduced program risk concentration in Wave 1.

*Fictional case study — see [README](../README.md) for full disclaimer.*
