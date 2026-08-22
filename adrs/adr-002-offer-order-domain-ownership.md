# ADR-002: Offer and Order Are First-Class Domains Owned by the Retailing Platform, Not the PSS

## Status

Accepted — ratified by the ARB during Phase C, referenced in every subsequent architecture contract touching the Order or Offer domains.

## Context

Once ADR-001 established that a new retailing platform would sit in front of the PSS, a further decision was required: where does the "Offer" (a priced, bundled proposition) and "Order" (a confirmed commercial agreement) actually live as data — inside the PSS's existing PNR structure (extended with new fields), or as genuinely new, separately owned domains in the new platform?

## Decision

Offer and Order are modeled as first-class domain entities **owned by the Retailing Platform**, structurally independent of the PNR, aligned to the IATA ONE Order model shape for Order. The PSS PNR remains the operational booking/ticketing record, owned by the PSS, and is kept consistent with Order via the Reconciliation Service (see ADR-003) rather than by merging the two data models into one.

## Alternatives Considered

1. **Extend the PNR schema with NDC/offer fields.** The PSS vendor's product does support some degree of custom field extension. This was seriously evaluated as the lowest-integration-effort path. Rejected because: (a) the PNR's underlying structure (largely free-text/segment-based, EDIFACT-era design) cannot cleanly express a bundled offer with multiple ancillary components and dynamic pricing breakdown — any extension would be a workaround, not a real model; (b) it would tie Halvern's retailing capability permanently to the PSS vendor's schema evolution roadmap and contract terms, reducing future architectural flexibility; (c) it directly conflicts with Architecture Principle 2, ratified specifically to prevent this pattern.
2. **A fully separate, PSS-independent booking flow for NDC channels only** (i.e., NDC bookings never touch the PSS at all, with the PSS reserved solely for legacy-channel bookings). Rejected because it would require duplicating departure control, check-in, and ticketing capability outside the PSS — effectively a partial, uncontrolled PSS replacement by another name, contradicting Architecture Principle 1 and reintroducing the very cutover-risk problem ADR-001 was written to avoid. It would also fragment operational visibility: airport and departure control staff would need to look in two entirely separate systems depending on which channel a passenger booked through.

## Consequences

**Positive:** Offer/Order data model can evolve independently of the PSS vendor's release cycle; Order becomes a clean, IATA-aligned source of commercial truth for downstream systems (Finance, Loyalty) without waiting for a PSS-side change; avoids permanent lock-in to PSS vendor schema decisions.

**Negative (accepted trade-offs):** Requires building and operating the Reconciliation Service (ADR-003) as ongoing infrastructure, not a one-time migration task — this is new, Halvern-specific software with real operating cost (business-case.md opex line items) for the life of the dual-model period, and potentially longer if full PSS replacement is never pursued. Any system consuming "commercial truth" data must be updated to know which domain (Order vs. PNR) is authoritative for which attribute, adding a documentation and onboarding burden for every new downstream integration (addressed via architecture-contracts.md's Data Ownership Statement section).

## Governance Impact

Directly implements Architecture Principles 2 and 11. Affects: ARB (data domain ownership approval per Principle 11), Lead Solution Architect for PSS Domain and for Retailing Platform (joint accountability for the reconciliation boundary), Finance/FP&A (eventual consumer of Order as commercial source of truth).

*Fictional case study — see [README](../README.md) for full disclaimer.*
