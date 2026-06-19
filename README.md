# gepwreg — Percentile Weights Regression for AURA

AURA port of the official Stata **`gepwreg`** package (Percentile Weights
Regression, PWR), by **Abdelkrim Araar** (Université Laval / PEP).

`gepwreg` estimates the local marginal effect ∂y/∂x at a target percentile *τ*
of the outcome (or a ranking variable) distribution, using Gaussian kernel
weights in rank space and weighted least squares, with **closed-form analytical
standard errors** that account for the sampling variability of the estimated
kernel weights.

## Features
- **MSE-optimal bandwidth** (two-step plug-in) by default; `silverman` rule or
  manual `band()` available.
- **Analytical IF-corrected standard errors** (Deville 1999); **Taylor
  linearisation** under complex survey design (`vce(svy)`); naive WLS SE for
  reference.
- **Generalised ranking** on any variable `z ≠ y` (`rankvar()`).
- Factor variables `i.var`; `fweight`/`aweight`/`pweight`.

Validated to reproduce the Stata `gepwreg` v1.3 results on the Burkina Faso
1998 survey (`bkf98I.dta`).

## Installation (from AURA)
```
pkg from "https://raw.githubusercontent.com/aabbdd12/gepwreg-aura/main/"
pkg install gepwreg
```
The command, help (`help gepwreg`), and the **Statistics → Econometrics →
Percentile Weights Regression** menu entry become available immediately.

## Quick start
```
use bkf98I
gen lexp = log(exppc)
gen fw   = size*weight
gepwreg lexp size i.gse [pw=fw], per(0.5)              // MSE-optimal (default)
gepwreg lexp size i.gse [pw=fw], per(0.5) silverman    // Silverman rule
svyset psu [pw=fw], strata(strata)
gepwreg lexp size i.gse, per(0.5) vce(svy)             // Taylor SE
```

## Citation
Araar, Abdelkrim. (2026). *Exploring Heterogeneous Effects: Quantile Models and
Percentile Weights Regression.* Zenodo. https://doi.org/10.5281/zenodo.20315684

## References
- Araar, A. (2016). *Percentile weights regression.* PEP Technical Note.
- Deville, J.-C. (1999). Variance estimation for complex statistics and
  estimators. *Survey Methodology*, 25(2):193–203.

## License
GPL-3.0-or-later. © 2026 Abdelkrim Araar.
