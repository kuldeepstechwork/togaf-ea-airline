# Architecture Contracts

## What an Architecture Contract Contains

An architecture contract is the formal agreement between the Enterprise Architecture function (via the ARB) and a delivery team, scoping exactly what the team is authorized to build, against which architecture decisions, with what constraints. Per TOGAF's Phase G guidance, it is the mechanism that translates an approved Solution Building Block (05-phase-e-opportunities-and-solutions/solution-building-blocks.md) into an accountable delivery commitment. At Halvern, every contract contains the following sections:

1. **Scope** — the specific SBB(s) covered, explicitly bounded (what the team is and is not building).
2. **Architecture Principles Alignment** — a statement against each of the 12 principles (00-preliminary/architecture-principles.md): Aligned / Aligned with exception / Not applicable, per the ARB submission requirement.
3. **Reference Architecture Conformance** — which reference pattern(s) the component must conform to, and any approved deviations.
4. **Data Ownership Statement** — which data domain(s) this component owns (system of record) versus reads/consumes, per Architecture Principle 11.
5. **Integration Contracts** — the specific interfaces this component exposes and consumes, referencing technology-standards.md.
6. **Non-Functional Requirements** — availability, latency, and reconciliation-window targets specific to this component.
7. **Governance Checkpoints Applicable** — which of the governance-framework.md checkpoints apply and when.
8. **Acceptance Criteria** — objective, testable criteria for Production Readiness Review sign-off.
9. **Named Accountable Parties** — the Solution Architect accountable for ongoing conformance, and the delivery team lead accountable for build.

## Worked Example — Reconciliation Service Architecture Contract

**Contract ID:** AC-2026-014
**SBB Covered:** Reconciliation Service (05-phase-e-opportunities-and-solutions/solution-building-blocks.md)
**Delivery Team:** Platform Engineering — Reconciliation Squad
**Accountable Solution Architect:** Lead Solution Architect, Retailing Platform

### 1. Scope

Build and operate the service responsible for detecting and resolving state divergence between the Order domain (owned by Order Management Service) and the PNR domain (owned by PSS Reservations), for the duration of the dual-data-model transition period (see 06-phase-f-migration-planning/transition-architectures.md). Explicitly excludes: any business logic for offer construction or pricing (owned by Offer Construction Service); any direct customer-facing interface (this is a backend-only service).

### 2. Architecture Principles Alignment

| Principle | Status | Justification |
|---|---|---|
| 1 — PSS system of record | Aligned | Service only reads PSS state via approved API; never writes to PSS directly. |
| 5 — Eventual consistency | Aligned | Core purpose of this service is to manage eventual consistency explicitly. |
| 8 — Decisions recorded | Aligned | Divergence-handling rules documented in ADR-003. |
| 11 — Single data owner | Aligned | Service owns no domain data itself; it is a reconciliation/detection layer, holding only its own operational state (unmatched-record queue). |
| Others | Not applicable | No direct bearing on this component's scope. |

### 3. Reference Architecture Conformance

Must conform to the reconciliation pattern described in 03-phase-c-information-systems-architecture/data-architecture.md. No approved deviations at contract signing.

### 4. Data Ownership Statement

Owns: the divergence/unmatched-record queue only (operational, not commercial data). Reads: Order state (from Order Management), PNR state (from PSS, via event stream). Writes to no domain of record.

### 5. Integration Contracts

Consumes: PSS booking-state event stream (technology-standards.md event backbone standard); Order Management state-change events. Exposes: a divergence-flag API consumed by Order Management for manual-review queuing; an audit/read API for the Post-Implementation Conformance Audit.

### 6. Non-Functional Requirements

Reconciliation detection latency: within 10 minutes of a state change on either side under normal load. Manual-exception rate target: below 2% of reconciled transactions by end of Wave 2 (per transition-architectures.md exit criteria). Availability: 99.9%, consistent with its position as a dependency for Order Management's ability to confirm bookings.

### 7. Governance Checkpoints Applicable

Design Review (completed, see governance-framework.md worked example — an earlier, related design was rejected at this checkpoint, informing this contract's final scope), Production Readiness Review before Wave 1 go-live, Post-Implementation Conformance Audit at Wave 1 + 90 days.

### 8. Acceptance Criteria

Passes integration test suite against PSS staging environment with 100% of defined divergence scenarios correctly flagged; Production Readiness Review sign-off from CISO (data handling) and VP IT Operations (operational readiness); zero P1 incidents in a 2-week pre-production soak test.

### 9. Named Accountable Parties

Solution Architect: Lead Solution Architect, Retailing Platform (ongoing conformance accountability). Delivery Lead: Platform Engineering Reconciliation Squad Lead (build accountability).

## Why Contracts Are Written This Formally

A lighter-weight, verbal or Slack-thread-documented agreement model was used earlier in Halvern's history for smaller integration projects, and was explicitly rejected for this program: post-incident reviews of two prior integration failures traced root cause partly to ambiguity over which team owned ongoing conformance once a component moved from delivery into steady-state operation. The formal contract's "Named Accountable Parties" section exists specifically to close that gap.

*Fictional case study — see [README](../README.md) for full disclaimer.*
