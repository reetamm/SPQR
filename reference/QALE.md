# quantile accumulated local effects (ALE)

Computes the quantile ALEs of a `SPQR` class object. The function plots
the ALE main effects across `tau` using line plots for a single
covariate, and the ALE interaction effects across `tau` using contour
plots for two covariates .

## Usage

``` r
QALE(
  object,
  var.index,
  tau = seq(0.1, 0.9, 0.1),
  n.bins = 40,
  ci.level = 0,
  getAll = FALSE,
  pred.fun = NULL
)
```

## Arguments

- object:

  An object of class `SPQR`.

- var.index:

  a numeric scalar or length-two vector of indices of the covariates for
  which the ALEs will be calculated. When `length(var.index) = 1`, the
  function computes the main effect for `X[,var.index]`. When
  `length(var.index) = 2`, the function computes the interaction effect
  between `X[,var.index[1]]` and `X[,var.index[2]]`.

- tau:

  The quantiles of interest.

- n.bins:

  the maximum number of intervals into which the covariate range is
  divided when calculating the ALEs. The actual number of intervals
  depends on the number of unique values in `X[,var.index]`. When
  `length(var.index) = 2`, `n.bins` is applied to both covariates.

- ci.level:

  The credible level for computing the pointwise credible intervals for
  ALE when `length(var.index) = 1`. The default is 0 indicating no
  credible intervals should be computed.

- getAll:

  If `TRUE` and `length(var.index) = 1`, extracts all posterior samples
  of ALE.

- pred.fun:

  A function that will be used instead of
  [`predict.SPQR()`](https://reetamm.github.io/SPQR/reference/predict.SPQR.md)
  for computing predicted quantiles given covariates. This can be useful
  when the user wants to compare the QALE calculated using SPQR to that
  using other quantile regression models, or maybe that using the true
  model in a simulation study.

## Value

- x:

  If `length(var.index) = 1`, a `(n.bins+1)`-length vector specifying
  the ordered predictor values at which the ALE plot function is
  calculated. These are the break points for the `n.bins` intervals into
  which the predictor range is divided, plus the lower boundary of the
  first interval and the upper boundary of the last interval. If
  `length(var.index) = 2`, a list of two such vectors, the first
  containing the `X[,var.index[1]]` values and the second containing the
  `X[,var.index[2]]` values at which the ALE plot function is
  calculated.

- ALE:

  If `length(var.index) = 1`, a `(n.bins+1)` by `length(tau)` matrix of
  predicted ALE values for every combination of `x` and `tau`. If
  `length(var.index) = 2`, a 3-dimensional array of predicted ALE
  values. Each slice corresponds to a quantile. Within each slice, the
  rows correspond to `X[,var.index[1]]` and the columns correspond to
  `X[,var.index[2]]`.

## Examples

``` r
# \donttest{
set.seed(919)
n <- 200
X <- runif(n,0,2)
Y <- rnorm(n,X^2,0.3+X/2)
control <- list(iter = 200, warmup = 150, thin = 1)
fit <- SPQR(X=X, Y=Y, n.knots=12, n.hidden=3, method="MCMC",
            control=control, normalize=TRUE, verbose = FALSE)

## compute quantile ALE main effect of X at tau = 0.2,0.5,0.8
ale <- QALE(fit, var.index=1, tau=c(0.2,0.5,0.8))
# }
```
