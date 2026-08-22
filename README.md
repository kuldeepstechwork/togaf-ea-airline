# TOGAF Enterprise Architecture Case Study — Halvern Air

**Disclaimer:** This is an illustrative TOGAF Enterprise Architecture case study modeling common, publicly known challenges in airline digital retailing — not a real engagement. Halvern Air is an invented name, not affiliated with any real company, and nothing here is based on confidential information from any real employer or client. All figures, vendor names, and technical details are constructed for this exercise.

---

## Program Overview

This repository documents a complete TOGAF Architecture Development Method (ADM) cycle for a modernization program at **Halvern Air**, a fictional regional airline operating roughly 120 aircraft and carrying approximately 9 million passengers a year. The program — internally referred to as the **Retailing & Distribution Modernization Program** — was chartered by Halvern's executive committee to move the airline from a legacy, filed-fare distribution model to a modern retailing capability built on IATA's New Distribution Capability (NDC) standard, without triggering a disruptive, multi-year replacement of the core Passenger Service System (PSS).

## The Business Problem

Halvern Air's PSS landscape — separate, loosely integrated systems for reservations, inventory, and departure control, none of which share a common data model — was built for an era of filed fares distributed almost exclusively through Global Distribution Systems (GDSs). That architecture cannot express bundled fares, ancillary upsells, or dynamic, personalized pricing, all of which are now table stakes for airline retailing. The airline's loyalty program runs on a bolt-on system that cannot accrue or redeem points in real time, which increasingly disqualifies Halvern from partner and co-brand card integrations that competitors already offer. Compounding the commercial pressure, Halvern faces a regulatory and channel deadline: major distribution partners are moving to require NDC-based connections, and Halvern's largest OTA and travel-agency channels have signaled they will deprioritize non-NDC content within 24 months. Leadership's mandate was explicit: modernize distribution and retailing, hit the NDC deadline, and do it without a "big bang" PSS cutover that would put nine-figure annual revenue at risk during a single, high-stakes migration weekend.

This repository is the architecture function's response to that mandate, developed using the TOGAF ADM as the governing method from Preliminary Phase through Phase H.

## How to Read This Repository

Every document here is written in **decision voice**, not build voice. You will not find narration of code written or servers configured — this is not an implementation log. Instead, each document states a decision, the alternatives that were seriously evaluated and rejected, the quantified trade-offs accepted (cost, risk, timeline, complexity — all illustrative but arithmetically real), and which governance body owns that decision. The intent is to demonstrate how an architect reasons under real constraints: incomplete information, competing stakeholder priorities, and a mandate to reduce risk rather than simply to build.

Start with [TOGAF-ADM-MAPPING.md](TOGAF-ADM-MAPPING.md) for a one-page map of every ADM phase to its folder. From there:

- [00-preliminary/](00-preliminary/) — Architecture principles and how governance was stood up before any design work began.
- [01-phase-a-vision-and-scope/](01-phase-a-vision-and-scope/) — Why this program exists, for whom, and what it explicitly will not do.
- [02-phase-b-business-architecture/](02-phase-b-business-architecture/) — As-is and to-be business capability and process views.
- [03-phase-c-information-systems-architecture/](03-phase-c-information-systems-architecture/) — Data and application architecture, as-is and to-be.
- [04-phase-d-technology-architecture/](04-phase-d-technology-architecture/) — The reference architecture pattern and the technology standards that govern it.
- [05-phase-e-opportunities-and-solutions/](05-phase-e-opportunities-and-solutions/) — Solution building blocks, vendor evaluation, and the gap analysis that drives the roadmap.
- [06-phase-f-migration-planning/](06-phase-f-migration-planning/) — The phased roadmap and named transition architectures between as-is and to-be.
- [07-phase-g-implementation-governance/](07-phase-g-implementation-governance/) — How the Architecture Review Board governs delivery, and what an architecture contract looks like.
- [08-phase-h-change-management/](08-phase-h-change-management/) — The organizational change plan that makes the target architecture stick.
- [adrs/](adrs/) — Five architecturally significant decisions recorded in standard ADR format.

Every figure in this repository — costs, timelines, vendor scores, maturity ratings — is invented for illustrative purposes and clearly framed as such throughout.

---
*Fictional case study — see disclaimer above for full context.*
