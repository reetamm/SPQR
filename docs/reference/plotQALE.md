# plot accumulated local effects (ALE)

Computes and plots the quantile ALEs of a `SPQR` class object. The
function plots the ALE main effects across `tau` for a single covariate
using line plots, and the ALE interaction effects between two covariates
across `tau` using contour plots.

## Usage

``` r
plotQALE(object, ...)
```

## Arguments

- object:

  An object of class `"SPQR"`.

- ...:

  Arguments passed on to
  [`QALE`](https://reetamm.github.io/SPQR/reference/QALE.md)

  `var.index`

  :   a numeric scalar or length-two vector of indices of the covariates
      for which the ALEs will be calculated. When
      `length(var.index) = 1`, the function computes the main effect for
      `X[,var.index]`. When `length(var.index) = 2`, the function
      computes the interaction effect between `X[,var.index[1]]` and
      `X[,var.index[2]]`.

  `tau`

  :   The quantiles of interest.

  `n.bins`

  :   the maximum number of intervals into which the covariate range is
      divided when calculating the ALEs. The actual number of intervals
      depends on the number of unique values in `X[,var.index]`. When
      `length(var.index) = 2`, `n.bins` is applied to both covariates.

  `ci.level`

  :   The credible level for computing the pointwise credible intervals
      for ALE when `length(var.index) = 1`. The default is 0 indicating
      no credible intervals should be computed.

  `getAll`

  :   If `TRUE` and `length(var.index) = 1`, extracts all posterior
      samples of ALE.

  `pred.fun`

  :   A function that will be used instead of
      [`predict.SPQR()`](https://reetamm.github.io/SPQR/reference/predict.SPQR.md)
      for computing predicted quantiles given covariates. This can be
      useful when the user wants to compare the QALE calculated using
      SPQR to that using other quantile regression models, or maybe that
      using the true model in a simulation study.

## Value

A `ggplot` object.

## Examples

``` r
# \donttest{
set.seed(919)
n <- 200
X <- runif(n,0,2)
Y <- rnorm(n,X^2,0.3+X/2)
control <- list(iter = 200, warmup = 150, thin = 1)
fit <- SPQR(X=X, Y=Y, n.knots=12, n.hidden=3, method="MCMC",
            control=control, normalize=TRUE)
#> 
#> Starting NUTS at 2026-02-13 20:13:09.197497
#> Error in globalCallingHandlers(condition = global_progression_handler): should not be called with handlers on the stack

## compute quantile ALE main effect of X at tau = 0.2,0.5,0.8
plotQALE(fit, var.index=1, tau=c(0.2,0.5,0.8))
#> Error: object 'fit' not found
# }
```
