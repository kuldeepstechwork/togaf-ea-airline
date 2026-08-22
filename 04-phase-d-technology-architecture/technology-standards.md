# Technology Standards

## Purpose

This document lists the approved technology stack and standards for the Retailing & Distribution Modernization Program, and the process for requesting an exception. It operationalizes Architecture Principles 4, 7, 9, and 12 for delivery teams.

## Approved Standards

### Distribution / Messaging Standards

| Standard | Version / Profile | Status |
|---|---|---|
| IATA NDC Schema | 21.3 (baseline), with a committed upgrade path to 23.1 within 12 months of GA | Mandatory floor — non-negotiable per Architecture Principle 9 |
| IATA ONE Order | Aligned conceptually for Order Management data model; full ONE Order interline messaging is out of scope (vision-and-scope.md) | Mandatory for Order domain model shape |
| EDIFACT / Type A (legacy GDS) | Current PSS vendor-supported version | Maintained, not upgraded, for legacy channel duration |
| PCI DSS | v4.0 | Mandatory, applies to all new components touching the payment boundary |

### Platform & Infrastructure

| Layer | Approved Standard | Notes |
|---|---|---|
| API Gateway / Channel Edge | Commercial API gateway product, OpenAPI 3.x contract-first design | Must support schema versioning and canary routing per channel |
| Event Backbone | Managed cloud event streaming service (durable, at-least-once delivery) | Required for all event-driven integrations (Offer→Loyalty, PSS→Reconciliation) |
| Retailing Platform Hosting | Cloud-hosted, single-region (see reference-architecture.md scale rationale) | Multi-region is an explicit future exception path, not a default |
| Data Storage — Loyalty Ledger | Append-only event store + materialized balance projection store | Must support point-in-time replay for audit (Architecture Principle 6) |
| Identity & Access | Existing enterprise IdP, OAuth2/OIDC for all new service-to-service and partner-facing auth | No new identity provider introduced by this program |
| Observability | Existing enterprise logging/monitoring stack, extended to new components | New components must not introduce a parallel, unintegrated monitoring toolchain |

### Integration & Interoperability

- All new inter-service communication uses REST/JSON over HTTPS or the approved event backbone; no new point-to-point proprietary protocols.
- All external partner-facing APIs are versioned using semantic-style versioning with a minimum 12-month deprecation notice for breaking changes (see ADR-005 for the full NDC API versioning strategy).
- No new component may write directly to a PSS database; all PSS interaction is via the PSS vendor's supported API layer only (reinforcing Architecture Principle 1 and the rejected anti-pattern in reference-architecture.md).

## Exceptions Process

An exception to any standard in this document requires:

1. A written exception request submitted to the ARB using the standard submission template, citing the specific standard, the proposed deviation, and the business or technical justification.
2. Explicit evaluation against Architecture Principle 9 (compliance vs. implementation distinction) — an exception to a regulatory/standards-conformance item (NDC schema version, PCI DSS) is **not grantable**; exceptions apply only to implementation-layer standards (e.g., choice of event backbone product, hosting region).
3. A stated expiry or review date — no exception is permanent by default; it is reviewed at the next quarterly principles review (00-preliminary/governance-framework-setup.md) and either formalized as a standards update or retired.
4. Majority ARB vote to approve, logged in the Exceptions Register.

As of the most recent quarterly review, the Exceptions Register contains one active exception: the Loyalty Ledger Service's event store product was approved as a temporary deviation from the enterprise-standard event streaming service, because the enterprise standard's managed offering did not yet support the replay-for-audit requirement at the time of Wave 1 build; this exception is scheduled for re-review at the Wave 3 gate once the enterprise platform's roadmap delivers that capability.

## Deliberately Not Standardized (Yet)

Multi-region hosting topology and a formal API rate-limiting/quota framework for partner-tier differentiation are recognized as needing standards but are deferred to a post-Wave-2 technology standards revision, once real partner integration volume data is available to inform the design rather than guessing ahead of evidence.

*Fictional case study — see [README](../README.md) for full disclaimer.*
