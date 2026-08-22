# Governance Framework Setup

## Purpose

Before any Phase A vision work began, Halvern Air's CIO chartered an Architecture Review Board (ARB) and a lightweight governance framework to ensure the Retailing & Distribution Modernization Program did not repeat the pattern that produced the current fragmented PSS landscape: multiple delivery teams making locally optimal, globally inconsistent integration decisions with no forum for cross-cutting review. This document describes how that governance body was constituted, how it operates, and how it enforces the architecture principles.

## ARB Constitution

The ARB is chaired by the **Head of Enterprise Architecture** and has seven standing voting members:

| Role | Represents |
|---|---|
| Head of Enterprise Architecture (Chair) | Overall architecture integrity, tie-breaking vote |
| VP Commercial / Revenue Management | Business outcomes — retailing, pricing, distribution economics |
| VP IT Operations | Production stability, operational supportability |
| Chief Information Security Officer (or delegate) | Security, PCI DSS, data protection |
| Head of Loyalty & Customer | Loyalty program impact and customer data integrity |
| Lead Solution Architect, PSS Domain | Legacy PSS constraints and integration feasibility |
| Lead Solution Architect, Retailing Platform | New platform design integrity |

Delivery team leads and vendor architects attend as non-voting contributors when their workstream is on the agenda. The Program Sponsor (Chief Commercial Officer) receives ARB minutes but does not sit on the board, preserving separation between program sponsorship and architecture governance.

Membership is reviewed annually; the Chair may add a temporary voting seat for a specific decision (e.g., Data Protection Officer for a data-residency decision) with majority board consent.

## Cadence

- **Standing ARB review:** biweekly, 90 minutes. Agenda is published 3 business days in advance; submissions require the standard ARB submission template (architecture summary, principles alignment, alternatives considered, risk).
- **Fast-track review:** a 48-hour asynchronous review path for low-risk changes (e.g., a configuration change within an already-approved solution building block). Chair plus two members can approve; any member may escalate to a full standing review.
- **Quarterly principles review:** the ARB revisits the architecture principles (00-preliminary/architecture-principles.md) and the ADR log each quarter to confirm continued validity as the program and the external NDC landscape evolve. A principle or ADR is never silently abandoned — a superseding decision is documented before an old one stops being enforced.
- **Program milestone gate reviews:** at each Phase F wave boundary (see 06-phase-f-migration-planning/migration-roadmap.md), the ARB conducts a formal go/no-go review before the next wave's build work begins.

## Escalation Path

1. **Delivery team level:** disagreements on implementation detail within an already-approved architecture contract are resolved by the assigned Solution Architect and delivery lead directly.
2. **ARB standing review:** any decision that touches a stated architecture principle, crosses a system-of-record boundary, or introduces a new external dependency must come to the ARB before implementation begins.
3. **Escalation to CIO:** a decision the ARB cannot resolve by majority vote (or a 3-3-1 split with the Chair unable to break tie without a conflict of interest) escalates to the CIO within 5 business days.
4. **Escalation to Program Steering Committee:** decisions with material budget or timeline impact (>10% of a wave's budget, or >4 weeks of schedule impact) escalate to the cross-functional Program Steering Committee chaired by the CCO, regardless of ARB outcome, per the RACI in 01-phase-a-vision-and-scope/stakeholder-map.md.

## Principles Enforcement

Every ARB submission is required to state, against each of the twelve architecture principles, whether the proposal is **Aligned**, **Aligned with exception requested**, or **Not applicable**, with a one-line justification for each. A proposal cannot proceed to implementation with an unresolved "exception requested" status — exceptions require explicit majority ARB approval and are logged in a running Exceptions Register reviewed at the quarterly principles review.

This structure — light enough to run biweekly without becoming a bottleneck, but with a documented escalation path all the way to executive sponsorship — was itself a deliberate trade-off. A heavier, weekly-review model was considered and rejected: with roughly 8-10 delivery workstreams active at peak (see migration-roadmap.md), a weekly cadence was projected to add an estimated 1.5 FTE-equivalent of coordination overhead across delivery teams for marginal additional risk reduction, based on comparable governance loads observed in prior Halvern change programs of similar scale.

*Fictional case study — see [README](../README.md) for full disclaimer.*
