# ADR-004: Event-Sourced, Append-Only Loyalty Ledger Architecture

## Status

Accepted — ratified by the ARB during Phase C; implemented by Vendor D (SkyLedger Systems) per vendor-evaluation.md.

## Context

Halvern's current loyalty system stores only a current point balance per member, updated via nightly batch mutation. This has caused recurring, hard-to-resolve customer disputes (no way to reconstruct how a balance was derived), makes fraud investigation largely manual, and — most critically for this program — makes real-time redemption at point of sale architecturally infeasible, since there is no mechanism to safely check and decrement a balance in real time without risking race conditions on a mutable field under concurrent access. A new architecture is required to support real-time accrual and redemption as part of the offer/order flow (Architecture Principle 6).

## Decision

The Loyalty Ledger is implemented as an **append-only, event-sourced log** of every accrual and redemption transaction; current balance is always a derived, materialized projection computed from the event log, never a directly mutated field. Redemption eligibility checks read the real-time projection; every redemption itself is recorded as a new ledger event, not a decrement of an existing value.

## Alternatives Considered

1. **Mutable balance table with optimistic locking / row-level transactions.** A more familiar, lower-build-effort pattern: keep a single current-balance row per member, protected by database-level concurrency control to prevent race conditions on redemption. Rejected because it does not solve the auditability problem that is a stated business driver of this program (real-time capability *and* dispute/fraud resolution were both named requirements) — a mutable table with good concurrency control prevents double-spend but still cannot answer "how did we arrive at this balance" without a separate, bolted-on audit log, which effectively reconstructs event sourcing badly rather than adopting it deliberately.
2. **Third-party loyalty-as-a-service platform with a fully managed ledger, no Halvern-owned data store at all.** Considered as a way to avoid building any ledger infrastructure. Rejected primarily on data ownership and portability grounds: loyalty transaction history is commercially sensitive and, per Architecture Principle 11, Halvern requires an unambiguous owning system under its own governance; a fully externalized ledger with no local event log would make future migration or dual-sourcing materially harder and was assessed as a long-term strategic risk disproportionate to the build-effort savings, especially given Vendor D's viable event-sourcing product was already a strong fit (vendor-evaluation.md).

## Consequences

**Positive:** Every balance is fully reconstructable and auditable from the event log, directly resolving the dispute-resolution and fraud-investigation pain points; real-time redemption is architecturally sound because eligibility checks and redemption events are handled through well-understood event-sourcing concurrency patterns rather than ad hoc locking; supports future capability (e.g., point-expiry rules, tiered accrual multipliers) as new event types without restructuring existing data.

**Negative (accepted trade-offs):** Higher initial storage volume and query complexity than a simple balance table — the materialized balance projection must be actively maintained and kept consistent with the event log, adding an operational component (projection rebuild/repair tooling) that a simple mutable table would not require. Engineering team ramp-up on event-sourcing patterns was a real, if modest, training cost not present in the simpler alternative (reflected in the loyalty ledger build-out line item in business-case.md, and in the change-management-plan.md training scope for the platform engineering team, not just business stakeholders).

## Governance Impact

Directly implements Architecture Principle 6. Affects: ARB (approved the pattern), Head of Loyalty & Customer (accountable for business rules layered on the ledger), CISO (data retention and access-control review for an append-only store containing customer transaction history).

*Fictional case study — see [README](../README.md) for full disclaimer.*
