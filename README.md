# FX Volatility Surface Models — EUR/GBP

Construction and comparison of implied volatility surface models 
applied to EUR/GBP market data (30 January 2026).

## Models

| Model | Status | Description |
|---|---|---|
| Vanna-Volga | ✅ Complete | Castagna & Mercurio (2007) |
| Reiswich & Wystup | ✅ Complete/Finalizing| Reiswich & Wystup (2012) |
| SABR | 🔄 In progress | Hagan et al. (2002) |
| SSVI | 🔄 In progress | Gatheral & Jacquier (2014) |
| Heston | 🔄 In progress | Heston (1993) |

## Methodology Comparison

| | Vanna-Volga | SABR | SSVI | Heston |
|---|---|---|---|---|
| Inputs | 3 market quotes | 4 parameters | 2 parameters per slice | 5 parameters |
| Calibration | Closed-form | Nonlinear least squares | Nonlinear least squares | Nonlinear least squares |
| Arbitrage-free | In practice | Approximate | Yes | Yes |
| Extrapolation | Weak beyond 25Δ | Good | Good | Good |
| FX market use | Standard vanilla | Common | Growing | Less common |

## Data
- `FX data.xlsx` — EUR/GBP vol surface quotes (ATM, RR, SSM across tenors)
- `discount_curves.xlsx` — EUR ESTR and GBP SONIA zero coupon curves

## Repository Structure
```
fx-volatility-surface-models/
├── models/
│   ├── vanna_volga/
│   ├── reiswich_wystup/
│   ├── sabr/
│   ├── ssvi/
│   └── heston/
├── shared/
├── data/
└── outputs/
```

## Requirements
```
numpy pandas scipy matplotlib plotly openpyxl
```

## References

- Castagna, A. and Mercurio, F. (2007). *The Vanna-Volga method for implied volatilities*. Risk Magazine.
- Hagan, P. et al. (2002). *Managing smile risk*. Wilmott Magazine.
- Gatheral, J. and Jacquier, A. (2014). *Arbitrage-free SVI volatility surfaces*. Quantitative Finance.
- Heston, S. (1993). *A closed-form solution for options with stochastic volatility*. Review of Financial Studies.
- Reiswich, D. and Wystup, U. (2012). *FX volatility smile construction*. Wilmott Magazine.