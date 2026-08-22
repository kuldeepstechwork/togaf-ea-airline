# Migration Roadmap

## Sequencing Rationale

The roadmap is organized into four waves over 24 months, sequenced by the priority and lead-time analysis in gap-analysis.md: the highest-risk, longest-lead-time, most Halvern-specific components (Reconciliation Service, core Offer Construction) start earliest, even though they will not be user-visible until later waves, because their build risk — not their business value — is the schedule-critical factor. Vendor-dependent components (Order Management, NDC Gateway configuration) are sequenced to follow vendor contracting, which itself follows the vendor-evaluation.md recommendation and Program Steering Committee approval.

An alternative sequencing was considered and rejected: front-loading the customer/partner-visible NDC Gateway capability first, to show early external progress against the deadline. This was rejected by the ARB because standing up channel-facing NDC connectivity before the Reconciliation Service exists would create a period where confirmed NDC orders have no mechanism to reconcile against PSS bookings — an unacceptable operational risk under Architecture Principle 5, even though it would have looked better on an external-facing status report.

## Wave Overview

| Wave | Duration | Primary Focus | Gate Criteria to Proceed |
|---|---|---|---|
| Wave 0 — Foundation | Months 1-3 | ARB/governance stood up (already complete), vendor contracting (Vendor A, Vendor D), environments, security architecture baseline | Vendor contracts signed; security architecture reviewed; ARB operating cadence established |
| Wave 1 — Core Platform Build | Months 3-9 | Reconciliation Service build, Offer Construction Service core, Order Management configuration, initial PSS integration | Reconciliation Service passes integration test against PSS staging; ARB go/no-go gate review |
| Wave 2 — Loyalty & Pilot Distribution | Months 8-15 | Loyalty Ledger Service build, first NDC-conformant pilot channel (single OTA partner), dynamic pricing rules engine configuration | Pilot partner completes NDC certification; real-time loyalty accrual live in pilot; business case checkpoint (ancillary attach-rate actuals review) |
| Wave 3 — Scaled Distribution | Months 14-20 | Remaining channel partner onboarding (NDC Gateway), legacy protocol adapter hardening, Customer Profile consolidated view | 70% of indirect-channel booking volume on NDC (per vision-and-scope.md success metric); no forced legacy channel outage recorded |
| Wave 4 — Stabilization & Optimization | Months 19-24 | Performance/scale hardening, reconciliation exception-rate reduction, handover to steady-state run team, Change Management adoption metrics review | 90% NDC adoption target met; reconciliation manual-exception rate below defined SLA; steady-state run team fully staffed and trained |

Waves overlap deliberately — Wave 2 begins before Wave 1 fully closes, since Loyalty Ledger build has no hard dependency on Offer Construction completion, only on the event backbone standard (technology-standards.md) being in place.

## Roadmap Gantt

```mermaid
gantt
    title Retailing & Distribution Modernization — Migration Roadmap
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y
    section Wave 0 - Foundation
    Vendor contracting (A & D)         :w0a, 2026-09-01, 60d
    Security architecture baseline     :w0b, 2026-09-01, 75d
    Environments & CI/CD setup         :w0c, 2026-10-01, 60d
    section Wave 1 - Core Platform
    Reconciliation Service build       :w1a, 2026-12-01, 150d
    Offer Construction Service core    :w1b, 2026-12-15, 150d
    Order Mgmt configuration           :w1c, 2027-01-15, 120d
    Wave 1 ARB gate review             :milestone, 2027-06-01, 0d
    section Wave 2 - Loyalty & Pilot
    Loyalty Ledger Service build       :w2a, 2027-04-01, 180d
    Dynamic pricing rules config       :w2b, 2027-05-01, 120d
    Pilot NDC partner onboarding       :w2c, 2027-06-01, 150d
    Business case checkpoint review    :milestone, 2027-10-15, 0d
    section Wave 3 - Scaled Distribution
    Remaining partner onboarding       :w3a, 2027-10-15, 180d
    Legacy protocol adapter hardening  :w3b, 2027-10-15, 90d
    Customer profile consolidated view :w3c, 2027-11-15, 120d
    section Wave 4 - Stabilization
    Performance & scale hardening      :w4a, 2028-03-01, 90d
    Reconciliation exception reduction :w4b, 2028-03-01, 120d
    Run-team handover & training       :w4c, 2028-05-01, 90d
    Program close-out gate             :milestone, 2028-08-15, 0d
```

## Risk Buffer

Each wave carries an implicit schedule buffer of approximately 10-15% not shown as separate line items in the Gantt above but reflected in the contingency capex line (business-case.md); this follows Halvern's standard capital program practice for initiatives with external dependency risk (vendor delivery, partner certification timelines) outside the program's direct control.

*Fictional case study — see [README](../README.md) for full disclaimer.*
