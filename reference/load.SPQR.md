# load saved SPQR model

Load saved SPQR model from a designated path. The function first loads
the `.SPQR` file that stores the `SPQR` object. It then checks whether
the SPQR model is fitted with `method = "MCMC"`. If not, it also loads
the `.pt` file storing the `torch` model with the same `name` and attach
it to the `SPQR` object.

## Usage

``` r
load.SPQR(name = stop("`name` must be specified"), path = NULL)
```

## Arguments

- name:

  The name of the saved object excluding extension.

- path:

  The path to look for the saved object. Default is the current working
  directory.

## Value

An object of class `SPQR`.

## Examples

``` r
# \donttest{
set.seed(919)
n <- 200
X <- rbinom(n, 1, 0.5)
Y <- rnorm(n, X, 0.8)
fit <- SPQR(X = X, Y = Y, method = "MCMC", normalize = TRUE, verbose = FALSE)
# save.SPQR(fit, name = "mcmc_fit")
# fit <- load.SPQR("mcmc_fit")
# }
```
