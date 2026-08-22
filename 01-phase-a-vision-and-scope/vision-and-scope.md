# Architecture Vision — Retailing & Distribution Modernization Program

## Problem Statement

Halvern Air distributes and prices its product using a Passenger Service System (PSS) landscape assembled over roughly 15 years: separate reservations, inventory, and departure control systems, integrated point-to-point, with no shared offer or order data model. This architecture supports traditional filed fares — a fixed fare class sold through a GDS — but cannot express bundled fares, ancillary-inclusive offers, or dynamically priced propositions, which is now the baseline expectation for airline retailing set by network carriers and low-cost competitors alike.

Three forces converge to make this an urgent architecture problem rather than a backlog item:

1. **Commercial:** Halvern's ancillary revenue per passenger is estimated at roughly 60% of the industry benchmark for comparable regional carriers, attributable in large part to the inability to merchandise ancillaries as part of a bundled offer at the point of sale.
2. **Loyalty:** Halvern's loyalty program runs on a bolt-on system with batch-only point accrual (typically a 24-48 hour posting delay) and no real-time redemption capability, which excludes Halvern from partner and co-brand integrations that require real-time balance checks.
3. **Regulatory/channel deadline:** Halvern's two largest distribution partners (a major OTA and a leading travel-agency consolidator, representing an estimated 38% of indirect-channel bookings) have communicated that non-NDC content will be deprioritized in search ranking and, in one case, phased out of direct integration within 24 months.

## Target-State Vision

By the end of the program, Halvern Air will:

- Distribute NDC-conformant, dynamically priced, bundled offers through a retailing platform that sits in front of the existing PSS, without requiring a PSS replacement.
- Support real-time loyalty point accrual and redemption as a first-class part of the offer and order flow.
- Retire direct point-to-point channel integrations against PSS fare tables in favor of a single internal offer construction service consumed by all channels.
- Maintain full backward compatibility with existing GDS/EDIFACT distribution throughout the transition, so no existing revenue channel is put at risk during migration.

The vision is deliberately **evolutionary, not revolutionary**: the PSS continues to do what it does reliably today (book, ticket, check in passengers) while a new retailing layer is built alongside it and progressively takes over offer construction and distribution logic.

## Scope Boundaries

### In Scope

- Design and delivery of a retailing platform (offer construction, bundling, dynamic pricing hooks) positioned in front of the PSS.
- NDC API distribution to travel agents and OTAs, conformant with IATA NDC schema (see 04-phase-d-technology-architecture/technology-standards.md for versioning).
- Real-time loyalty ledger architecture supporting accrual and redemption at point of sale.
- Reconciliation architecture between the new offer/order data model and the legacy PNR model during the transition period.
- Governance, migration planning, and change management for the above.

### Explicitly Out of Scope

- **Full PSS replacement.** A wholesale reservations/inventory/departure-control system replacement was evaluated (see ADR-001) and explicitly rejected for this program. It remains a candidate for a future, separately chartered program once the retailing layer has proven the operating model.
- **Codeshare and interline systems modernization.** Halvern's codeshare partnerships run through existing Type A/Type B messaging that is out of scope; NDC-based interline (IATA ONE Order interline) is a recognized future capability but is not committed in this program's roadmap.
- **Revenue management / pricing science overhaul.** This program builds the *distribution mechanism* for dynamic and bundled pricing; the pricing algorithms and revenue management optimization logic themselves belong to a separate Commercial function initiative and are treated as a consuming stakeholder, not a deliverable, of this program.
- **Airport departure control hardware/kiosk refresh.** Physical check-in infrastructure is unaffected; departure control system *software* interfaces are touched only where required for order-based check-in.
- **Full loyalty program redesign (tier structure, partner network expansion).** Only the *technical* real-time ledger capability is in scope; commercial redesign of the loyalty program itself is a Marketing-led initiative that will consume the new ledger capability once available.

These exclusions were set deliberately to keep the program deliverable within the NDC compliance deadline. Each excluded item was evaluated and rejected specifically because bundling it into this program's critical path would extend the timeline beyond the 24-month channel deadline (see business-case.md for the cost of a missed deadline).

## Success Metrics

| Metric | Baseline (Today) | Target (Program End) |
|---|---|---|
| NDC-conformant offers as % of indirect channel bookings | 0% | 70% within 6 months of GA, 90% within 12 months |
| Ancillary revenue per passenger vs. industry benchmark | ~60% of benchmark | ≥90% of benchmark |
| Loyalty point posting latency | 24-48 hours (batch) | <5 seconds (real-time) at point of sale |
| Distribution cost per indirect booking (GDS/OTA fees) | Baseline fee schedule | ≥15% reduction via NDC direct-connect fee avoidance |
| Retained legacy channel availability during migration | N/A | 100% — zero forced channel outage during any migration wave |
| Architecture principle exception rate | N/A | <10% of ARB submissions requiring a principles exception by program end |

*Fictional case study — see [README](../README.md) for full disclaimer.*
