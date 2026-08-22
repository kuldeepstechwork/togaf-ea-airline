# Change Management Plan

## Why This Is an Architecture Deliverable, Not Just an HR Function

TOGAF's Phase H exists because an architecture that is technically correct but organizationally unadopted delivers none of the business case's projected value — the ancillary revenue uplift and distribution cost savings in business-case.md depend entirely on Revenue Management, Distribution/Commercial, and Loyalty & Customer actually using the new capabilities as designed. This plan treats organizational adoption as a first-class deliverable with the same governance rigor as the technical architecture.

## Organizational Change Impact

| Stakeholder Group | Nature of Change | Impact Severity |
|---|---|---|
| Revenue Management | Gains ownership of bundling/dynamic pricing *rules configuration* — a genuinely new skill (rules-engine literacy) replacing purely static fare-filing work | High |
| Distribution/Commercial | Shifts from IT-dependent bespoke channel projects to self-service partner onboarding — changes both workflow and required lead time expectations with partners | High |
| Loyalty & Customer | Gains real-time visibility and control via ledger rules engine; must retire dependency on vendor batch cycle mental model | Medium-High |
| Contact Center / Frontline Staff | New tools for real-time redemption and order-based booking lookups during the transition period, alongside legacy PNR-based tools (dual-path per transition-architectures.md) | Medium |
| IT/PSS Operations | Insulated from most channel-driven change going forward, but must operate a new reconciliation service and understand its exception-handling workflows | Medium |
| Finance/FP&A | New reporting model as Order becomes commercial source of truth, alongside continued PNR-based operational reporting during transition | Medium |

## Training Plan

- **Revenue Management rules-engine training:** a structured curriculum delivered in two parts — vendor-led product training (Vendor A, per vendor-evaluation.md) ahead of Wave 2 pilot go-live, followed by Halvern-specific scenario workshops run by the Solution Architecture team covering Halvern's actual bundling strategy use cases, not just generic product features.
- **Contact center dual-path training:** frontline staff are trained to recognize which booking path (legacy PNR-only vs. new Order-based) a given customer interaction falls into during the transition period, with a simple decision-tree job aid — avoiding the failure mode of staff attempting to use new tools on legacy-path bookings where they don't yet apply.
- **Distribution/Commercial self-service onboarding training:** hands-on workshops on the NDC Gateway partner configuration console, timed to precede Wave 3's scaled partner onboarding so the team is capable of self-service before volume ramps.
- **IT Operations reconciliation runbook training:** delivered ahead of each Production Readiness Review checkpoint (governance-framework.md), covering the specific divergence-handling scenarios the Reconciliation Service is built to flag.

## Communication Plan

| Audience | Message Focus | Channel | Cadence |
|---|---|---|---|
| Executive Committee / Program Steering Committee | Progress against wave gates, business case checkpoint results | Steering Committee reporting pack | Monthly |
| ARB and delivery teams | Architecture decisions, contract status, non-compliance handling outcomes | ARB minutes, internal architecture wiki | Biweekly (ARB cadence) |
| Revenue Management & Distribution/Commercial | Capability readiness, training schedule, what changes for their day-to-day work | Dedicated change champions network + town halls | Monthly, increasing to biweekly ahead of each wave go-live |
| Contact Center / Frontline Staff | Dual-path guidance, job aids, escalation paths for exceptions | Team briefings, job aid distribution via existing ops comms channel | Ahead of each wave go-live, then as-needed |
| Distribution Partners (external) | NDC onboarding readiness, certification timeline, legacy channel continuity assurance | Partner account management relationship | Per partner onboarding schedule (migration-roadmap.md) |

A **change champions network** — one nominated representative per affected business function (Revenue Management, Distribution/Commercial, Loyalty & Customer, Contact Center) — was established specifically to surface adoption friction early, rather than relying solely on top-down communication; this was modeled on a prior Halvern change program where the absence of such a network was identified as a contributing factor to slow adoption.

## Adoption Metrics

| Metric | Target | Measurement Point |
|---|---|---|
| Revenue Management rules-engine active usage (configuring at least one bundling/pricing rule per month) | 100% of assigned analysts by Wave 2 + 60 days | Platform usage analytics |
| Contact center dual-path job aid comprehension (post-training assessment) | ≥90% pass rate | Training assessment, pre-Wave 1 go-live |
| Distribution partner self-service onboarding completion (no IT escalation required) | ≥80% of Wave 3 partners | Onboarding console analytics |
| Change champion network engagement (monthly feedback submission rate) | ≥75% of champions submitting monthly | Change management tracking log |
| Employee sentiment on new tooling (pulse survey) | No more than a 10-point drop from pre-change baseline during any single wave transition | Quarterly pulse survey |

These adoption metrics are reviewed alongside the technical wave gate criteria (migration-roadmap.md) at each ARB wave gate review — a wave is not considered fully successful on adoption grounds alone if the technical criteria pass but adoption metrics lag, and the Program Steering Committee has authority to direct additional change management investment before authorizing the next wave's capital release.

*Fictional case study — see [README](../README.md) for full disclaimer.*
