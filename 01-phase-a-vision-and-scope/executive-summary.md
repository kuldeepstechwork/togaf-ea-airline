# Executive Summary — Retailing & Distribution Modernization Program

## The Problem

Halvern Air sells seats the way the industry sold them twenty years ago: fixed fares, filed through travel agencies and online agents, with no ability to bundle bags, seats, or upgrades into a single attractive offer, and a loyalty program that takes up to two days to post a point. Two of our largest distribution partners have told us plainly that they will deprioritize — and in one case, phase out — content that isn't delivered through the industry's modern NDC standard, within 24 months. Our ancillary revenue per passenger runs at roughly 60% of what comparable regional carriers achieve, largely because our systems cannot merchandise the way theirs do.

## The Recommendation

We recommend building a new retailing layer in front of our existing reservations and departure control systems — not replacing those systems. This layer will construct modern, bundled, dynamically priced offers and distribute them via NDC to travel agents and online agents, while our current systems continue doing what they already do reliably: booking, ticketing, and getting passengers on aircraft. We evaluated a full core-system replacement and rejected it — it would take three to five years and put revenue-critical operations at risk during a single high-stakes cutover. The approach we recommend can be delivered in waves, with no forced outage of any existing sales channel at any point.

## Cost and Timeline

The program is estimated at **$26.2M in one-time investment** over 24 months, with incremental annual operating cost of roughly **$6.0M** once live, offset by an estimated **$11.6M in annual savings and revenue uplift** at steady state — from reduced distribution fees, ancillary revenue growth, and retiring our current loyalty system's license. On a strict 3-year cash basis this does not fully pay back the capital investment through savings alone; it becomes economically compelling once the estimated **$16M+ in revenue at risk** from losing NDC-required distribution channels is weighed in. The Program Steering Committee has approved the business case with a checkpoint at the halfway mark to validate early ancillary revenue results before committing the second half of the capital.

## Risk

The principal risk is running two parallel data models — our legacy booking model and the new NDC offer/order model — for an estimated 18-24 months during transition, which requires a reconciliation layer and adds complexity to support operations during that window. We consider this an acceptable, actively managed risk in exchange for avoiding the far larger risk of a single, disruptive core-system replacement. A dedicated Architecture Review Board governs every material decision in this program biweekly, with a documented escalation path to this committee for anything with material budget or timeline impact.

## The Ask

Approval to proceed to Phase B (detailed business and technical architecture) on the funding and governance model described in the full business case, with the first go/no-go capital release gate at the end of Wave 1 (see migration-roadmap.md).

*Fictional case study — see [README](../README.md) for full disclaimer.*
