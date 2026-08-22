# Implementation Governance Framework

## Purpose

Phase G governance ensures that what gets built during Waves 0-4 actually conforms to the architecture decided in Phases A-E, rather than drifting under delivery pressure. This document describes the compliance checkpoints, the architecture contract mechanism, and how non-compliance is handled — distinct from the Preliminary Phase governance setup (00-preliminary/governance-framework-setup.md), which established the ARB itself; this document is about governing *delivery against* the architecture the ARB has already approved.

## Compliance Checkpoints

| Checkpoint | When | What Is Checked | Owner |
|---|---|---|---|
| Architecture Contract Sign-Off | Before any delivery team begins build on an SBB | Contract scope matches approved solution building block; principles alignment stated (see architecture-contracts.md) | ARB Chair + assigned Solution Architect |
| Design Review | At detailed design completion, before implementation | Component design conforms to reference architecture pattern and technology standards | Assigned Solution Architect (fast-track path available per governance-framework-setup.md cadence rules) |
| Wave Gate Review | End of each migration wave | Gate criteria met (migration-roadmap.md); architecture conformance across all SBBs delivered in the wave | Full ARB |
| Production Readiness Review | Before any component goes live to real channel/customer traffic | Security/PCI sign-off, operational runbook, reconciliation exception handling tested | CISO + VP IT Operations + ARB Chair |
| Post-Implementation Conformance Audit | 90 days after each wave's go-live | Sampled check that delivered components still match their architecture contract; catches drift introduced during stabilization/bug-fixing | Head of Enterprise Architecture |

## Non-Compliance Handling

Non-compliance is classified into three severities, each with a distinct response:

- **Minor deviation** (e.g., an implementation detail differs from the contract but does not affect an architecture principle or cross-system contract): logged in the delivery team's architecture contract as an addendum, reviewed at the next standing ARB cadence, generally accepted retroactively unless it sets a problematic precedent.
- **Material deviation** (e.g., a component bypasses the reconciliation service, or writes directly to a system it does not own per Architecture Principle 11): build work on the affected component is paused pending an emergency ARB review within 5 business days; the team must present a remediation plan or a formal exception request (technology-standards.md exceptions process) before resuming.
- **Principle violation with production impact** (e.g., a shipped component is found to persist raw cardholder data, violating Architecture Principle 7): treated as a Sev-1 governance incident — immediate escalation to CISO and CIO, mandatory hotfix or rollback, and a blameless post-implementation review presented to the full ARB, distinct from a standard non-compliance log entry given the regulatory exposure.

## How This Was Tested — A Worked Example

During Wave 1, a delivery team building the Order Management configuration proposed writing order-completion status directly back into a PSS custom field to simplify a reporting requirement from Commercial. This was flagged at Design Review as a material deviation: it would create a second write path into the PSS from outside the approved Order Management orchestration flow, violating Architecture Principle 1 (PSS as PNR system of record with a single orchestration path) and Architecture Principle 11 (single owning system per domain). The ARB rejected the shortcut and directed the team to satisfy the Commercial reporting need via the Reconciliation Service's existing event stream instead — a one-week delay to the specific reporting feature, against an estimated multi-month cost of unwinding an undocumented second PSS write path had it shipped and been discovered later. This example is now used as a reference case in new delivery-team onboarding (08-phase-h-change-management/change-management-plan.md).

## Relationship to Architecture Contracts

Every compliance checkpoint above is scoped against an underlying architecture contract (architecture-contracts.md) — the contract is the unit of governance; checkpoints verify conformance to it at defined points rather than continuously auditing all delivery activity, which the ARB judged an unsustainable governance load at Halvern's team size (consistent with the cadence trade-off reasoning in the Preliminary Phase governance setup).

*Fictional case study — see [README](../README.md) for full disclaimer.*
