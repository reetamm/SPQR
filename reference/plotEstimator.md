# plot SPQR estimators

Computes and plots the estimated PDF/CDF/QF curves.

## Usage

``` r
plotEstimator(object, X, ...)
```

## Arguments

- object:

  An object of class `"SPQR"`

- X:

  A row vector indicating covariate values for which the conditional
  PDF/CDF/QF is computed and plotted.

- ...:

  Arguments passed on to
  [`predict.SPQR`](https://reetamm.github.io/SPQR/reference/predict.SPQR.md)

  `nY`

  :   An integer number indicating length of grid when `Y` is not
      specified. Default: 101.

  `type`

  :   The function to be predicted; `"PDF"`: probability density
      function, `"CDF"`: cumulative distribution function, and `"QF"`:
      the quantile function (default).

  `tau`

  :   The grid of quantiles for which the quantile function is computed.
      Default: `seq(0.1,0.9,0.1)`.

  `ci.level`

  :   The credible level for computing the pointwise credible intervals.
      The default is 0 indicating no credible intervals should be
      computed.

  `getAll`

  :   If `TRUE`, extracts all posterior samples of the prediction.
      Default: `FALSE`.

## Value

A `ggplot` object.

## Examples

``` r
# \donttest{
set.seed(919)
n <- 200
X <- rbinom(n, 1, 0.5)
Y <- rnorm(n, X, 0.8)
control <- list(iter = 200, warmup = 150, thin = 1)
fit <- SPQR(X = X, Y = Y, method = "MCMC", control = control,
            normalize = TRUE, verbose = FALSE)


## plot estimated PDF
plotEstimator(fit, type = "PDF", X = 0)

# }
```
