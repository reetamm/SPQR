# generate cross-validation folds

Helper function to generate cross-validation folds that can be used by
`cv.SPQR`.

## Usage

``` r
createFolds.SPQR(Y, nfold, stratified = FALSE)
```

## Arguments

- Y:

  The response vector.

- nfold:

  The number of cross-validation folds.

- stratified:

  If `TRUE`, stratified folds based on quantiles of `Y` are generated.

## Value

A list of size `nfold` containing indices of the observations for each
fold.

## Examples

``` r
set.seed(919)
n <- 1000
X <- rbinom(n, 1, 0.5)
Y <- rnorm(n, X, 0.8)
folds <- createFolds.SPQR(Y, nfold = 5)
```
