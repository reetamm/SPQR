# print method for class `SPQR`

Summarizes and print the output produced by SPQR() in an organized way.

## Usage

``` r
# S3 method for class 'SPQR'
print(x, ...)
```

## Arguments

- x:

  An object of class `SPQR`

- ...:

  Arguments passed on to
  [`print.summary.SPQR`](https://reetamm.github.io/SPQR/reference/print.summary.SPQR.md)

  `showModel`

  :   If `TRUE`, prints the detailed NN architecture by layer.

## Value

No return value, called for side effects.

## Details

This is equivalent to the function call
`print.summary.SPQR(summary.SPQR(object), ...)`.

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
print(fit, showModel = TRUE)
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
#> Model specification:
#>     Layers
#>    Input Output Activation
#>        1     10       tanh
#>       10     10    softmax
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
