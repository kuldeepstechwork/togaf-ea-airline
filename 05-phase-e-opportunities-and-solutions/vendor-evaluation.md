# Vendor Evaluation — Retailing Platform

## Scope

This evaluation covers the core retailing platform (offer construction core, order management module, NDC API gateway capability) — the primary "buy" decision identified in solution-building-blocks.md. All vendor names below are invented for this fictional case study and do not refer to any real product or company.

## Candidates Evaluated

- **Vendor A — "Aeronova Retail Suite"**: An airline-specific retailing platform vendor with existing regional-carrier customers, offered as a managed cloud service with a per-transaction pricing model.
- **Vendor B — "Farepoint Distribution Cloud"**: A newer entrant focused specifically on NDC gateway and order management, with a lighter-weight offer construction module positioned as extensible via customer-built rules.
- **Vendor C — "Meridian Commerce Platform"**: A general-purpose retail commerce/order-management platform (not airline-specific) with an airline vertical accelerator package, offered as self-hosted or managed.
- **Vendor D — "SkyLedger Systems"**: A smaller, specialist vendor focused narrowly on loyalty ledger and real-time accrual/redemption, evaluated as a potential best-of-breed complement rather than a full retailing platform.

## Weighted Evaluation Criteria

Scores are 1 (poor fit) to 5 (excellent fit); weights reflect priority set jointly by the ARB and Commercial stakeholders during Phase E.

| Criterion | Weight | Vendor A | Vendor B | Vendor C | Vendor D |
|---|---|---|---|---|---|
| NDC schema conformance & certification track record | 20% | 5 | 4 | 2 | 1 |
| Order management maturity (IATA ONE Order alignment) | 15% | 4 | 4 | 3 | 1 |
| Loyalty/real-time ledger capability | 15% | 3 | 2 | 2 | 5 |
| Integration flexibility with legacy PSS | 15% | 4 | 5 | 3 | 2 |
| Total cost of ownership (license + integration effort) | 15% | 3 | 4 | 2 | 4 |
| Vendor stability / airline-domain references | 10% | 5 | 2 | 3 | 2 |
| Implementation timeline fit (NDC deadline pressure) | 5% | 4 | 5 | 2 | 3 |
| Extensibility for Halvern-specific bundling/pricing rules | 5% | 3 | 4 | 4 | 2 |

### Weighted Scores

| Vendor | Weighted Total |
|---|---|
| **Vendor A — Aeronova Retail Suite** | **4.05** |
| Vendor B — Farepoint Distribution Cloud | 3.80 |
| Vendor C — Meridian Commerce Platform | 2.55 |
| Vendor D — SkyLedger Systems | 2.35 |

*Weighted total = Σ(criterion score × weight). Example calculation for Vendor A: (5×0.20)+(4×0.15)+(3×0.15)+(4×0.15)+(3×0.15)+(5×0.10)+(4×0.05)+(3×0.05) = 1.00+0.60+0.45+0.60+0.45+0.50+0.20+0.15 = 4.05.*

## Recommendation

**Vendor A (Aeronova Retail Suite)** is recommended as the core retailing platform, covering NDC API gateway, offer construction core, and order management. Its combined strength on NDC conformance, order management maturity, and vendor stability — the three criteria the ARB weighted highest given the compliance deadline and multi-year operating horizon — outweighs Vendor B's edge on integration flexibility and timeline.

**Vendor D (SkyLedger Systems)** is recommended as a **complementary, best-of-breed selection specifically for the Loyalty Ledger Service**, notwithstanding its low overall weighted score as a full retailing platform. Its loyalty-specific capability (5/5) is the strongest of any candidate, and Solution Building Blocks decomposition (solution-building-blocks.md) already treats the Loyalty Ledger as a separately buildable/buyable component — the low overall score reflects its unsuitability as a *full platform* replacement for Vendor A, not unsuitability for its specific scope. This is a deliberate best-of-breed decision rather than a single-vendor consolidation, accepted with the trade-off of an additional vendor integration and contract to manage.

## Why the Runners-Up Lost

- **Vendor B (Farepoint)** scored competitively and was the strongest alternative to Vendor A — it was rejected primarily on vendor stability and airline-domain reference risk (score 2/5): as a newer entrant, Halvern's Legal and Procurement functions flagged concentration risk in relying on a vendor with fewer than three multi-year airline production references at the scale this program requires. Vendor B remains the ARB's documented fallback option should Vendor A contract negotiations fail (see architecture-contracts.md for how this contingency is reflected in the delivery contract).
- **Vendor C (Meridian)** was rejected primarily on NDC schema conformance (2/5) — as a general-purpose commerce platform, its airline accelerator package requires substantially more Halvern-side customization to reach NDC conformance than a purpose-built airline retailing vendor, which the ARB assessed as disproportionate integration risk and cost for a program under deadline pressure.
- **Vendor D (SkyLedger)**, evaluated as a full platform, was rejected for the reasons above but selected for its narrower, specialist scope — illustrating that a low overall weighted score does not disqualify a vendor from a scoped role where its specific strength dominates the decision.

## Procurement Note

This selection was presented to the Program Steering Committee alongside the vendor-evaluation scoring matrix and the business case (01-phase-a-vision-and-scope/business-case.md); the retailing platform licensing capex line item in that business case reflects Vendor A's quoted implementation fee structure.

*Fictional case study — see [README](../README.md) for full disclaimer.*
