# goodness-of-fit test for SPQR estimator

Performs a goodness-of-fit test for the estimated conditional
probability density function (PDF) using probability inverse
transformation method.

## Usage

``` r
plotGOF(object, getAll = FALSE)
```

## Arguments

- object:

  An object of class `SPQR`.

- getAll:

  If `TRUE` and SPQR is fitted with `method = "MCMC"`, plots all
  posterior samples of Q-Q lines. Default: `FALSE`.

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

## Goodness-of-fit test
plotGOF(fit)

# }
```
