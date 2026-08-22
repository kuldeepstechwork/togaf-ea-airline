# ADR-003: Asynchronous Event-Driven Reconciliation Between Order and PNR

## Status

Accepted — ratified by the ARB during Phase C; implementation scoped in architecture-contracts.md's worked example (Contract AC-2026-014).

## Context

Given ADR-001 (PSS remains system of record, retailing platform sits in front) and ADR-002 (Order and PNR are separately owned domains), Halvern must decide *how* these two domains are kept consistent with each other during the transition period. Divergence between Order state and PNR state — a cancelled order whose PSS booking wasn't cancelled, or a PSS-side schedule change not reflected in the Order — has direct customer and revenue impact if not caught and resolved.

## Decision

Reconciliation is implemented as an **asynchronous, event-driven service** that consumes state-change events from both the PSS (booking status) and Order Management (order status), detects divergence against defined business rules, and either auto-resolves within a bounded window or flags for manual review. No synchronous, single-transaction consistency mechanism is used across the PSS/Order boundary (Architecture Principle 5).

## Alternatives Considered

1. **Synchronous two-phase commit across PSS and Order Management.** Technically the "cleanest" consistency model — no divergence would ever be observable. Rejected because the PSS vendor's API does not support participation in a distributed transaction protocol, and even if it did, coupling Order confirmation latency to PSS transaction completion would introduce a hard availability dependency: any PSS slowdown or outage would directly block new order confirmation across all channels, including legacy ones unaffected by the PSS issue. This directly violates Architecture Principle 5's rejection of single-transaction-boundary assumptions.
2. **Batch nightly reconciliation** (mirroring the pattern already used for legacy loyalty accrual). Rejected because a 24-hour detection window for divergence is operationally unacceptable for confirmed commercial orders — an unresolved cancellation mismatch left open for up to a day risks customer-facing errors (e.g., a customer shown a cancelled order as still active) and directly undermines the real-time capability the program exists to deliver. It would also simply reproduce, in the new architecture, the exact batch-latency failure mode of the legacy loyalty system that this program is meant to fix.

## Consequences

**Positive:** No hard availability coupling between Order confirmation and PSS responsiveness; reconciliation detection window (target: within 10 minutes, per architecture-contracts.md) is a dramatic improvement over the batch alternative while remaining technically achievable against the PSS's actual API characteristics; the manual-exception queue provides an auditable, governable mechanism for the residual divergence that any eventually-consistent system will produce.

**Negative (accepted trade-offs):** A window of observable inconsistency (up to the 10-minute target, longer under degraded conditions) is an accepted, permanent characteristic of the architecture for the life of the dual-model period — not a bug to be eliminated, but a designed trade-off that downstream consumers (contact center tooling, Finance reporting) must be built to tolerate. This requires the Reconciliation Service itself to be highly available (99.9% target) since it becomes a single point of failure for order confirmation reliability if it goes down for an extended period — a new operational dependency that did not exist in the legacy architecture. Building and tuning the divergence-detection business rules required more calendar time in Wave 1 than initially estimated, since edge cases (irregular operations, partial cancellations, schedule changes) only fully surfaced once real PSS production event patterns were observed (see transition-architectures.md's Transition State 1 rationale).

## Governance Impact

Directly implements Architecture Principle 5. Affects: ARB (approved the pattern and the specific divergence-handling rules as part of Contract AC-2026-014), VP IT Operations (owns the operational runbook for the manual-exception queue), CISO (data handling review, since reconciliation touches both booking and order-level customer data).

*Fictional case study — see [README](../README.md) for full disclaimer.*
