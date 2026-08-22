# ADR-001: Retailing Platform in Front of PSS, Not Full PSS Replacement

## Status

Accepted — ratified by the ARB during Phase A, reaffirmed at the Wave 1 gate review.

## Context

Halvern Air needs to adopt NDC-conformant, bundled, dynamically priced retailing within a 24-month distribution partner deadline. The existing PSS (reservations, inventory, departure control) cannot express these constructs natively. Two architecturally distinct paths exist to close this gap: replace the PSS core with a modern system that natively supports offer/order retailing, or build a new retailing capability that sits in front of the existing PSS and leaves it in place for what it already does well.

## Decision

Halvern will build a **retailing platform positioned in front of the existing PSS**, which remains system of record for booking, ticketing, and departure control. The new platform owns offer construction and order management; a reconciliation layer keeps Order and PNR state consistent during a defined transition period. Full details of the pattern are in 04-phase-d-technology-architecture/reference-architecture.md.

## Alternatives Considered

1. **Full PSS Replacement.** A modern, offer/order-native PSS would eliminate the dual-data-model problem entirely and is the architecturally "cleaner" end state. Rejected for this program because: (a) estimated delivery timeline of 3-5 years for a full reservations/inventory/departure-control cutover at Halvern's scale, which does not meet the 24-month NDC deadline; (b) cutover risk — a single, high-stakes migration weekend for the system underpinning all active bookings and check-ins carries revenue and safety-adjacent operational risk that the ARB assessed as disproportionate to the retailing-capability gap being solved; (c) estimated cost of a full PSS replacement, based on comparable industry transformation programs, in the range of 3-5x this program's $26.2M capex estimate (business-case.md). Not rejected permanently — flagged as a candidate for a future, separately chartered program once PSS end-of-life or a different business driver justifies it.
2. **NDC API Layer Bolted Directly onto Existing PSS (minimal integration approach).** A lighter-weight alternative: add NDC-schema translation directly at the PSS's existing integration layer, without a separate retailing platform or offer/order domain model. Rejected because it does not solve the underlying data model constraint (Architecture Principle 2) — bundled, dynamic offers still cannot be expressed if the PSS's own fare/inventory model is the source of truth for the offer. This approach would meet the NDC schema-conformance letter of the requirement while failing the actual business goal of bundled, dynamic retailing.

## Consequences

**Positive:** Decouples the retailing/distribution timeline from full PSS replacement risk; delivers NDC conformance and bundled retailing within the required deadline; PSS operational stability is preserved since it is not being replaced.

**Negative (accepted trade-offs):** Halvern operates two parallel data models (legacy PNR and Order/Offer) for an estimated 18-24 months, requiring a reconciliation layer that adds an estimated 12% to program integration cost (reflected in business-case.md's reconciliation-layer line item) and ongoing operational complexity (governance-framework.md's non-compliance handling reflects real incidents from this complexity). The dual-model period is a genuine, not merely theoretical, source of operational risk, actively managed via the transition architecture states (06-phase-f-migration-planning/transition-architectures.md) rather than eliminated.

## Governance Impact

This decision anchors Architecture Principle 1 and is the primary input to the reference architecture (04-phase-d-technology-architecture/reference-architecture.md). Affects: ARB (architecture governance), CIO and CCO (Program Steering Committee — capital allocation), VP IT Operations (PSS operational stability accountability).

*Fictional case study — see [README](../README.md) for full disclaimer.*
