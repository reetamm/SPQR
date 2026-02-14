# coef method for class `SPQR`

Computes the estimated spline coefficients of a `SPQR` class object

## Usage

``` r
# S3 method for class 'SPQR'
coef(object, X, ...)
```

## Arguments

- object:

  An object of class `SPQR`.

- X:

  The covariate vector/matrix for which the coefficient is calculated.

- ...:

  Other arguments.

## Value

A `NROW(X)` by K matrix containing values of the estimated coefficient,
where K is the number of basis functions.

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
coef(fit, X = 0)
#>       Coefs
#> X       theta[1]   theta[2]   theta[3] theta[4]  theta[5]  theta[6]   theta[7]
#>   [1,] 0.0148705 0.01241067 0.08595322 0.356902 0.3471123 0.1392085 0.03044411
#>       Coefs
#> X         theta[8]    theta[9]   theta[10]
#>   [1,] 0.004286563 0.002801199 0.006010941
# }
```
