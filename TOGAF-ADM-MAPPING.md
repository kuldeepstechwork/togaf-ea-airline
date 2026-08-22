# TOGAF ADM Phase Mapping

This table maps each phase of the TOGAF Architecture Development Method (ADM) to the folder in this repository that contains its artifacts, and summarizes what each phase produced for the Halvern Air Retailing & Distribution Modernization Program.

| ADM Phase | Folder | What's In It |
|---|---|---|
| Preliminary Phase | [00-preliminary/](00-preliminary/) | Architecture principles that govern all subsequent decisions, and how the Architecture Review Board (ARB) and governance framework were established before design work began. |
| Phase A — Architecture Vision | [01-phase-a-vision-and-scope/](01-phase-a-vision-and-scope/) | Problem statement, target-state vision, explicit scope boundaries, stakeholder map with RACI, the business case with full cost math, and a CxO-facing executive summary. |
| Phase B — Business Architecture | [02-phase-b-business-architecture/](02-phase-b-business-architecture/) | As-is and to-be business process and capability views for retailing, distribution, and loyalty, plus a capability map with maturity ratings. |
| Phase C — Information Systems Architecture | [03-phase-c-information-systems-architecture/](03-phase-c-information-systems-architecture/) | As-is and to-be data architecture (PNR, offer, order, loyalty ledger) and application architecture, including integration patterns. |
| Phase D — Technology Architecture | [04-phase-d-technology-architecture/](04-phase-d-technology-architecture/) | The reference architecture pattern selected for NDC/retailing delivery, including when *not* to use it, and the approved technology standards. |
| Phase E — Opportunities & Solutions | [05-phase-e-opportunities-and-solutions/](05-phase-e-opportunities-and-solutions/) | Decomposition of target capabilities into solution building blocks, the vendor evaluation and recommendation, and the prioritized gap analysis. |
| Phase F — Migration Planning | [06-phase-f-migration-planning/](06-phase-f-migration-planning/) | The phased, wave-based migration roadmap with a Gantt view, and named transition architectures between as-is and to-be. |
| Phase G — Implementation Governance | [07-phase-g-implementation-governance/](07-phase-g-implementation-governance/) | The implementation governance model (compliance checkpoints, non-compliance handling) and the architecture contract template with a worked example. |
| Phase H — Architecture Change Management | [08-phase-h-change-management/](08-phase-h-change-management/) | The organizational change management plan: impact analysis, training, communications, and adoption metrics. |
| Cross-cutting — Requirements Management | Embedded throughout each phase folder | TOGAF treats Requirements Management as a continuous activity at the center of the ADM cycle rather than a discrete phase; requirements traceability is carried inline in Phase A scope, Phase E gap analysis, and Phase G contracts rather than as a separate folder. |
| Cross-cutting — Architecture Decision Records | [adrs/](adrs/) | Five architecturally significant decisions recorded independently of the phase they originated in, since each decision was revisited and reaffirmed across multiple ADM cycles as delivery progressed. |

*Fictional case study — see [README](README.md) for full disclaimer.*
