# plrd

> **Paper-specific MOSEK fork.** This repository is a minimal fork of the
> [main `plrd` package](https://github.com/ghoshadi/plrd), based on upstream
> commit [`aa23041`](https://github.com/ghoshadi/plrd/commit/aa23041c1cc9dc46eb85974167b22c88df6587a3).

The original package implements Partially Linear Regression Discontinuity
inference proposed by Ghosh, Imbens and Wager (2025). This fork retains the
upstream implementation and attribution, changing only the internal quadratic
program from `quadprog` to the MOSEK conic optimizer through `Rmosek`.

This version was used for Michalik et al. (2026), *The population-level impact
of herpes zoster vaccination on dementia, cerebrovascular, and all-cause
mortality: Evidence from country-wide death certificate data for England*.

A working MOSEK installation and license are required. After installing
`Rmosek`, install this fork with:

```r
remotes::install_github("FelixMichalik/plrd@paper-2026-mosek")
```

## Upstream package documentation

Partially Linear Regression Discontinuity Inference, as proposed by Ghosh, Imbens and Wager (2025).

The development version of this package can be installed using devtools:

```R
devtools::install_github("ghoshadi/plrd")
```
Replication files for Ghosh, Imbens and Wager (2025) are available in
the directory `Experiments`.

Example usage:

```R
library(plrd)
# Simple example of regression discontinuity design
set.seed(42)
n = 1000; threshold = 0
X = runif(n, -1, 1)
W = as.numeric(X >= threshold)
Y = (1 + 2*W)*(1 + X^2) + 1 / (1 + exp(X)) + rnorm(n, sd = .5)
out = plrd(Y, X, threshold)
print(out)
plot(out)
plot(out, type = "weights")
```

#### References
Aditya Ghosh, Guido Imbens and Stefan Wager.
<b>PLRD : Partially Linear Regression Discontinuity Inference.</b>, [arXiv preprint arXiv:2503.09907](https://arxiv.org/abs/2503.09907).


#### Funding
Development of this software was supported by the National Science Foundation under grant number SES-2242876.
