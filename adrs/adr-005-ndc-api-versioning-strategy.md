# ADR-005: NDC API Versioning Strategy — Parallel-Version Support, Not Forced Migration

## Status

Accepted — ratified by the ARB during Phase D; enforced by the API Gateway layer defined in reference-architecture.md.

## Context

Halvern's NDC (New Distribution Capability) offer/order APIs are consumed externally by travel agents, OTAs, and metasearch aggregators — parties Halvern does not control the release schedules of. IATA's NDC schema itself evolves (minor and major schema versions), and Halvern's own retailing platform will iterate on offer construction logic faster than its slowest external consumers can re-certify their integrations. Without an explicit versioning strategy, any schema change risks either breaking existing distribution partners (unacceptable — NDC adoption is a regulatory/commercial deadline, not optional) or freezing Halvern's own ability to iterate on offer construction to whatever pace its slowest partner can absorb.

## Decision

Halvern's NDC API Gateway supports **N and N-1 major schema versions concurrently**, with a minimum 12-month deprecation notice period before any version is retired, and additive-only changes permitted within a major version (new optional fields, never breaking changes to existing required fields or response shapes). Each distribution partner pins to a specific major version at integration time; the gateway performs response shaping to serve the correct version-specific contract from a single internal canonical offer/order model, so Halvern's core retailing logic is not duplicated per API version.

## Alternatives Considered

1. **Single current version only, with a hard cutover date per schema change.** Simplest to build and operate — no version-shaping logic needed in the gateway. Rejected because it puts the entire distribution channel's continuity at the mercy of every partner's re-certification speed; a single slow OTA partner would either force Halvern to delay a schema change indefinitely or force that partner offline, both of which were assessed as unacceptable commercial risk given NDC distribution revenue is a named business driver in vision-and-scope.md.
2. **Per-partner custom contracts (bespoke integration per distribution partner rather than versioned but standard NDC contracts).** Maximizes flexibility for large partners with specific needs. Rejected because it reintroduces exactly the point-to-point integration sprawl this program's To-Be architecture is designed to eliminate (see application-architecture.md) — every bespoke contract becomes a permanent, individually-maintained liability rather than a governed, finite set of versions.

## Consequences

**Positive:** Distribution partners get a predictable, published deprecation runway instead of unplanned breaking changes; Halvern's internal retailing platform can iterate on offer construction without being gated by the slowest external partner's re-certification cycle; a single canonical internal offer/order model (with version-shaping at the edge) avoids duplicating core business logic per API version.

**Negative (accepted trade-offs):** The API Gateway must carry response-shaping logic for at least two concurrent major versions at all times, adding an estimated 10-15% ongoing maintenance overhead to the gateway layer versus a single-version design. Running N and N-1 concurrently for a minimum 12 months means some distribution partners will, for a period, be receiving offers constructed under a schema version Halvern's product team considers legacy — this was accepted as a bounded, governed cost rather than an open-ended one, precisely because the 12-month retirement clock is fixed and published at the time a new version ships, not decided reactively.

## Governance Impact

Directly implements Architecture Principle 4 (interoperability over point-to-point coupling) and Architecture Principle 9 (backward-compatible change by default). Affects: ARB (owns the deprecation-window policy and any exception requests to shorten it), Head of Distribution & Partnerships (accountable for partner communication and re-certification tracking), API Gateway platform team (owns the version-shaping implementation and its inclusion in every schema change's definition of done, per architecture-contracts.md).

*Fictional case study — see [README](../README.md) for full disclaimer.*
