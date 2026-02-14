# print method for `"summary.SPQR"`

Print the output produced by summary.SPQR().

## Usage

``` r
# S3 method for class 'summary.SPQR'
print(x, showModel = FALSE, ...)
```

## Arguments

- x:

  An object of class `summary.SPQR`

- showModel:

  If `TRUE`, prints the detailed NN architecture by layer.

- ...:

  Other arguments.

## Value

No return value, called for side effects.

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

## summarize output
summary(fit)
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> Warning: The ESS has been capped to avoid unstable estimates.
#> 
#> SPQR fitted using MCMC approach with ARD prior🚀
#> 
#> MCMC diagnostics:
#>   Final acceptance ratio is 0.90 and target is 0.9
#> 
#> Expected log pointwise predictive density (elpd) estimates:
#>   elpd.LOO = 90.65508,  elpd.WAIC = 90.01237
#> 
#> Elapsed time: 0.04 minutes
# }
```
