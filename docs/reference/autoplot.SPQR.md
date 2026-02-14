# autoplot method for class `SPQR`

The function calls one of the following functions:
[`plotEstimator()`](https://reetamm.github.io/SPQR/reference/plotEstimator.md),
[`plotGOF()`](https://reetamm.github.io/SPQR/reference/plotGOF.md),
[`plotMCMCtrace()`](https://reetamm.github.io/SPQR/reference/plotMCMCtrace.md),
[`plotQALE()`](https://reetamm.github.io/SPQR/reference/plotQALE.md),
[`plotQVI()`](https://reetamm.github.io/SPQR/reference/plotQVI.md)

## Usage

``` r
# S3 method for class 'SPQR'
autoplot(object, output = c("GOF", "estimator", "trace", "QALE", "QVI"), ...)
```

## Arguments

- object:

  An object of class `SPQR`.

- output:

  A character indicating the type of plot to be returned.

  - `"GOF"`: goodness of fit test by comparing the quantiles of
    probability integral transform (PIT) to that of uniform
    distribution.

  - `"estimator"`: visualization of various estimates, including
    probability density function (PDF), cumulative density function
    (CDF) and quantile function (QF).

  - `"trace"`: diagnostic trace plots for SPQR fitted with
    `method = "MCMC"`.

  - `"QALE"`: quantile accumulative local effects (ALE) for visualizing
    covariate effects on predicted quantiles.

  - `"QVI"`: quantile variable importance comparison.

- ...:

  arguments passed into specific plot function, see
  [`plotEstimator()`](https://reetamm.github.io/SPQR/reference/plotEstimator.md),
  [`plotGOF()`](https://reetamm.github.io/SPQR/reference/plotGOF.md),
  [`plotMCMCtrace()`](https://reetamm.github.io/SPQR/reference/plotMCMCtrace.md),
  [`plotQALE()`](https://reetamm.github.io/SPQR/reference/plotQALE.md)
  or [`plotQVI()`](https://reetamm.github.io/SPQR/reference/plotQVI.md)
  for required arguments.

## Value

a `ggplot` object

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

## Goodness-of-fit test
autoplot(fit, output = "GOF")

# }
```
