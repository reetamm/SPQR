# save fitted SPQR model

Save `SPQR` object in a designated directory. If SPQR is fitted with
`method = "MCMC"` then only a `.SPQR` file is saved; otherwise, a `.pt`
file storing the fitted `torch` model is also saved.

## Usage

``` r
save.SPQR(object, name = stop("`name` must be specified"), path = NULL)
```

## Arguments

- object:

  An object of class `SPQR`.

- name:

  The name of the saved object excluding extension.

- path:

  The path to save the object. Default is the current working directory.

## Value

No return value, called for side effects.

## Examples

``` r
# \donttest{
set.seed(919)
n <- 200
X <- rbinom(n, 1, 0.5)
Y <- rnorm(n, X, 0.8)
fit <- SPQR(X = X, Y = Y, method = "MCMC", normalize = TRUE, verbose = FALSE)
# save.SPQR(fit, name = "mcmc_fit")
# }
```
