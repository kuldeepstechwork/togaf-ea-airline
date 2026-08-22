# Business Case

All figures in this document are illustrative, invented for this fictional case study, and do not represent real financial data. They are constructed to be internally consistent and arithmetically sound so the reasoning pattern is transparent, not to represent any real airline's economics.

## Cost Basis

### Capex / One-Time Investment (Program Duration: 24 Months)

| Line Item | Basis | Estimated Cost |
|---|---|---|
| Retailing platform licensing — implementation & configuration | One-time setup fee per vendor contract (see vendor-evaluation.md) | $2,400,000 |
| Integration effort — PSS reconciliation layer | 42 person-months @ blended rate $16,500/person-month (mix of internal + contracted architects/engineers) | $6,930,000 |
| Integration effort — NDC API layer & channel onboarding | 30 person-months @ $16,500/person-month | $4,950,000 |
| Loyalty ledger platform build-out | 24 person-months @ $16,500/person-month | $3,960,000 |
| Security/PCI architecture review & remediation | Fixed-scope engagement | $850,000 |
| Data migration & reconciliation tooling | 12 person-months @ $16,500/person-month | $1,980,000 |
| Test environments, NDC certification (IATA conformance testing) | Fixed vendor + internal effort | $620,000 |
| Change management & training (see 08-phase-h-change-management/) | Program allocation | $1,100,000 |
| Contingency (15% of above, per Halvern capital program policy) | 15% × $22,790,000 | $3,418,500 |
| **Total Capex** | | **$26,208,500** |

### Opex — Incremental Annual Run Cost (Post Go-Live, Steady State)

| Line Item | Basis | Estimated Annual Cost |
|---|---|---|
| Retailing platform subscription/licensing | Per-transaction + platform fee, vendor contract | $3,100,000 |
| Incremental cloud infrastructure (offer service, loyalty ledger, reconciliation layer) | Estimated compute/storage/data transfer at ~9M pax/year offer volume | $1,450,000 |
| Additional platform engineering headcount (steady-state run team) | 6 FTE @ fully loaded $185,000/year | $1,110,000 |
| NDC certification maintenance & schema version upgrades | Annual vendor + internal effort | $310,000 |
| **Total Incremental Annual Opex** | | **$5,970,000** |

### Offsetting Annual Savings (Steady State, From Year 2 Onward)

| Line Item | Basis | Estimated Annual Value |
|---|---|---|
| GDS/OTA distribution fee avoidance via NDC direct-connect | 15% reduction target (vision-and-scope.md) on estimated $18M annual indirect-channel distribution fees | $2,700,000 |
| Ancillary revenue uplift from bundled/dynamic offers | Closing gap from ~60% to ~90% of industry ancillary-revenue-per-passenger benchmark, applied to 9M passengers at an estimated $4.50 average benchmark gap per passenger | $8,100,000 |
| Loyalty program cost avoidance (retiring bolt-on batch system license) | Existing vendor contract retirement | $780,000 |
| **Total Annual Offsetting Value** | | **$11,580,000** |

## 3-Year TCO Comparison — As-Is vs. To-Be

**As-Is (do nothing) — 3-year cost of standing still:**

- No new capex.
- Opex: continued GDS/OTA fee schedule at current levels (~$18M/year distribution cost, no reduction) plus continued loyalty bolt-on license (~$780K/year) plus estimated cost of non-compliance risk (see below).
- 3-year as-is opex: ($18,000,000 + $780,000) × 3 = **$56,340,000**, before accounting for the revenue-at-risk from losing NDC-required distribution channels.
- **Revenue-at-risk (not a hard cost, but material to the case):** the two partners flagging NDC deprecation represent an estimated 38% of indirect-channel bookings. If even half of that volume is lost to declining search ranking / phased deprecation over the 3-year window, and indirect-channel bookings represent an estimated $210M of annual revenue, the exposure is on the order of $210M × 19% × an assumed 3-year weighted average erosion factor of 40% ≈ **$16,000,000+ in at-risk revenue** — illustrative, but directionally the reason this program has executive sponsorship.

**To-Be (program delivered) — 3-year cost:**

- Capex (Year 1-2, spread across the 24-month program): $26,208,500
- Opex Year 1 (partial year post-go-live, assume 4 months at run rate): $5,970,000 × (4/12) = $1,990,000
- Opex Year 2 (full run rate, savings begin): $5,970,000 − $11,580,000 = **−$5,610,000** (net positive)
- Opex Year 3 (full run rate, full savings): $5,970,000 − $11,580,000 = **−$5,610,000** (net positive)
- 3-year to-be net cost: $26,208,500 + $1,990,000 − $5,610,000 − $5,610,000 = **$16,978,500**

**3-Year TCO Delta:** As-Is opex-only baseline of $56,340,000 (excluding revenue-at-risk) vs. To-Be net cost of $16,978,500 — a 3-year net position improvement of approximately **$39,361,500**, before counting avoided revenue-at-risk.

## Payback Period / ROI

Using the incremental capex ($26,208,500) against net annual benefit once savings exceed incremental opex:

- Net annual benefit at steady state = Offsetting value − incremental opex = $11,580,000 − $5,970,000 = **$5,610,000/year**
- Simple payback period = Capex ÷ Net annual benefit = $26,208,500 ÷ $5,610,000 ≈ **4.7 years** on capex alone at steady-state run rate.
- However, savings ramp in during Year 1 partial year and reach full run rate from Year 2; a more realistic cumulative payback, using the Year 1 partial benefit (4 months × $5,610,000/12 ≈ $1,870,000) plus full Year 2 and Year 3 benefit ($5,610,000 each), is:
  - Cumulative benefit by end of Year 3: $1,870,000 + $5,610,000 + $5,610,000 = $13,090,000 against $26,208,500 capex — payback is **not fully achieved within the 3-year TCO window on capex alone**, but the revenue-at-risk avoidance ($16M+ illustrative exposure) and the compounding ancillary-revenue uplift beyond Year 3 (not discounted further here) bring the qualitative payback inside the 3-4 year range that Halvern's capital program threshold (5 years for strategic infrastructure) accepts.
- **3-Year ROI** (net benefit ÷ capex) = ($39,361,500 − $16,978,500... using the TCO delta directly): ROI is better read as the TCO delta of ~$39.4M in avoided/reduced spend over 3 years against $26.2M capex, i.e., a **~150% return on capital deployed within the 3-year window**, before counting revenue-at-risk avoidance.

The Program Steering Committee reviewed this case with the explicit caveat that the ancillary revenue uplift figure is the single largest and least certain line item; the business case was approved with a condition that the Wave 2 gate review (see 06-phase-f-migration-planning/migration-roadmap.md) include an actuals-vs-projection check on early ancillary attach-rate data before Wave 3 capital is released.

*Fictional case study — see [README](../README.md) for full disclaimer.*
