# Stakeholder Map

## Stakeholder Concerns

| Stakeholder | Primary Concern | Power/Interest |
|---|---|---|
| Chief Commercial Officer (Program Sponsor) | Ancillary revenue growth, NDC deadline compliance, competitive parity | High / High |
| CIO | Delivery risk, integration with existing IT estate, total cost of ownership | High / High |
| VP Commercial / Revenue Management | Ability to launch bundled/dynamic offers on the timeline commercial strategy requires | High / High |
| Head of Loyalty & Customer | Real-time accrual/redemption, data quality, partner integration readiness | Medium / High |
| CISO | PCI DSS scope, data protection, new attack surface from external-facing NDC API | High / Medium |
| VP IT Operations | Production stability of PSS during transition, operational supportability of new platform | High / Medium |
| Head of Enterprise Architecture (ARB Chair) | Architectural integrity, principle adherence, technical debt avoidance | Medium / High |
| Lead Solution Architect, PSS Domain | Feasibility of reconciliation approach without destabilizing PSS | Medium / High |
| Distribution Partners (OTAs, GDSs, travel agencies) | Timely, stable NDC connectivity; minimal integration burden on their side | Low (direct) / High |
| Frontline Contact Center & Airport Staff | Usability of new tools, adequacy of training, no increase in exception handling | Low / Medium |
| Finance / FP&A | Capex/opex profile, ROI realization against business case | Medium / Medium |
| Data Protection Officer | Regulatory compliance for customer/loyalty data across jurisdictions | Medium / Medium |
| Regulatory/Compliance (external — IATA, national aviation/consumer authorities) | NDC schema conformance, consumer protection in dynamic pricing display | Low (direct influence) / High |
| Existing Loyalty Platform Vendor | Contract continuity, integration scope, potential displacement | Low / Medium |

## RACI — Program-Level Decisions

R = Responsible, A = Accountable, C = Consulted, I = Informed

| Decision Area | CCO (Sponsor) | CIO | Head of EA / ARB | VP Commercial | Head of Loyalty | CISO | VP IT Ops | Finance |
|---|---|---|---|---|---|---|---|---|
| Program charter & business case approval | A | R | C | C | C | I | I | C |
| Architecture principles ratification | I | A | R | C | C | C | C | I |
| Reference architecture / pattern selection | I | A | R | C | I | C | C | I |
| Vendor selection (retailing platform) | C | A | R | R | C | C | C | C |
| Data domain ownership assignment | I | A | R | C | C | I | I | I |
| Migration wave sequencing | C | A | R | C | I | I | C | C |
| Go/no-go at each wave gate | A | R | R | C | C | C | C | I |
| PCI / security architecture sign-off | I | C | C | I | I | A | I | I |
| Loyalty ledger architecture | I | C | R | C | A | I | I | I |
| Change management & training plan | C | I | C | C | C | I | R | I |
| Program budget reallocation (>10%) | A | R | C | C | I | I | I | C |

Note: The ARB (00-preliminary/governance-framework-setup.md) is Responsible for architecture governance decisions listed above; escalations beyond ARB authority route to the CIO and, for budget/timeline-material items, to the Program Steering Committee chaired by the CCO, per the escalation path defined there.

*Fictional case study — see [README](../README.md) for full disclaimer.*
