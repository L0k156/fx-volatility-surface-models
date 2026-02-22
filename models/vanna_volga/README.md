# Vanna-Volga Smile Construction — EUR/GBP

Implementation of the Vanna-Volga methodology following 
Castagna & Mercurio (2007) applied to FX market data.

## What This Notebook Does

1. Loads EUR/GBP market data — ATM, 25Δ and 10Δ RR and SSM quotes
2. Bootstraps EUR ESTR and GBP SONIA discount curves via PCHIP interpolation
3. Constructs the three-pillar VV smile across 25 tenors (ON to 25Y)
4. Validates out-of-sample against 10Δ market quotes
5. Checks butterfly arbitrage via Breeden-Litzenberger risk-neutral PDF

## Key Results

- Sub-20 bps 10Δ pricing error across 1M–10Y tenors
- Smile arbitrage-free across all short and medium tenors
- Full 2D and 3D volatility surface visualisation

## Key Implementation Decisions

**Exact VV inversion vs approximations**
Uses full numerical inversion of the VV price formula (Eq. 7) rather 
than the parabolic approximations (Eq. 11, 12). The approximations 
are inadmissible as pricing tools due to Lee moment formula violations.

**OTM-leg inversion**
Always inverts the out-of-the-money instrument — put for K≤F, call 
for K>F. Prevents Newton-Raphson floor bleed-through that produces 
spurious 0.1% vols on deep OTM call strikes.

**Long-tenor handling**
Exact VV method truncated at model breakdown boundary for 15Y+ tenors. 
10Δ quotes displayed as out-of-sample validation diamonds rather than 
connected to the smile curve, honestly communicating the model's 
domain of validity.

## Known Limitations

- Calibrated to 25Δ pillars only — 10Δ call wing errors grow for 15Y+
- Production extension: include 10Δ as calibration inputs for long tenors
- No calendar spread arbitrage enforcement across tenors

## Output Charts

| File | Description |
|---|---|
| `vv_eurgbp_discount_curves.png` | EUR ESTR and GBP SONIA curve visualisation |
| `vv_eurgbp_term_structure.png` | ATM and wing vol term structures |
| `vv_eurgbp_smile_3m_walkthrough.png` | Detailed 3M tenor smile construction |
| `vv_eurgbp_validation_10d.png` | 10Δ out-of-sample validation |
| `vv_eurgbp_vol_surface_2d.png` | Full 2D vol surface across all tenors |
| `vv_eurgbp_vol_surface_3d.png` | Interactive 3D volatility surface |
| `vv_eurgbp_price_decomposition.png` | Vega, Vanna, Volga contribution breakdown |
| `vv_eurgbp_pdf_arbitrage_check.png` | Breeden-Litzenberger PDF arbitrage check |

## Reference

Castagna, A. and Mercurio, F. (2007). 
*The Vanna-Volga method for implied volatilities*. Risk Magazine.