# Fitting SPQR models

Main function of the package. Fits SPQR using the maximum likelihood
estimation (MLE), maximum *a posterior* (MAP) or Markov chain Monte
Carlo (MCMC) method. Returns an object of S3 class `SPQR`.

## Usage

``` r
SPQR(
  X,
  Y,
  n.knots = 10,
  n.hidden = 10,
  activation = c("tanh", "relu", "sigmoid"),
  method = c("MLE", "MAP", "MCMC"),
  prior = c("ARD", "GP", "GSM"),
  hyperpar = list(),
  control = list(),
  normalize = FALSE,
  verbose = TRUE,
  seed = NULL,
  ...
)
```

## Arguments

- X:

  The covariate matrix (without intercept column)

- Y:

  The response vector.

- n.knots:

  The number of basis functions. Default: 10.

- n.hidden:

  A vector specifying the number of hidden neurons in each hidden layer.
  Default: 10.

- activation:

  The hidden layer activation. Either `"tanh"` (default) or `"relu"`.

- method:

  Method for estimating SPQR. One of `"MLE"`, `"MAP"` (default) or
  `"MCMC"`.

- prior:

  The prior model for variance hyperparameters. One of `"GP"`, `"ARD"`
  (default) or `"GSM"`.

- hyperpar:

  A list of named hyper-prior hyperparameters to use instead of the
  default values, including `a_lambda`, `b_lambda`, `a_sigma` and
  `b_sigma`. The default value is 0.001 for all four hyperparameters.

- control:

  A list of named and method-dependent parameters that allows finer
  control of the behavior of the computational approaches.

  1\. Parameters for MLE and MAP methods

  - `use.GPU` If `TRUE` GPU computing will be used if
    [`torch::cuda_is_available()`](https://torch.mlverse.org/docs/reference/cuda_is_available.html)
    returns `TRUE`. Default: `FALSE`.

  - `lr` The learning rate used by the Adam optimizer, i.e.,
    [`torch::optim_adam()`](https://torch.mlverse.org/docs/reference/optim_adam.html).

  - `dropout` A length two vector specifying the dropout probabilities
    in the input and hidden layers respectively. The default is `c(0,0)`
    indicating no dropout.

  - `batchnorm` If `TRUE` batch normalization will be used after each
    hidden activation.

  - `epochs` The number of passes of the entire training dataset in
    gradient descent optimization. If `early.stopping.epochs` is used
    then this is the maximum number of passes. Default: 200.

  - `batch.size` The size of mini batches for gradient calculation.
    Default: 128.

  - `valid.pct` The fraction of data used as validation set. Default:
    0.2.

  - `early.stopping.epochs` The number of epochs before stopping if the
    validation loss does not decrease. Default: 10.

  - `print.every.epochs` The number of epochs before next training
    progress in printed. Default: 10.

  - `save.path` The path to save the fitted torch model. By default a
    folder named `"SPQR_model"` is created in the current working
    directory to store the model.

  - `save.name` The name of the file to save the fitted torch model.
    Default is `"SPQR.model.pt"`.

  2\. Parameters for MCMC method

  These parameters are similar to those in
  [`rstan::stan()`](https://mc-stan.org/rstan/reference/stan.html).
  Detailed explanations can be found in the Stan reference manual.

  - `algorithm` The sampling algorithm; `"HMC"`: Hamiltonian Monte Carlo
    with dual-averaging, `"NUTS"`: No-U-Turn sampler (default).

  - `iter` The number of MCMC iterations (including warmup). Default:
    2000.

  - `warmup` The number of warm-up/burn-in iterations for step-size and
    mass matrix adaptation. Default: 500.

  - `thin` The number of iterations before saving next post-warmup
    samples. Default: 1.

  - `stepsize` The discretization interval/step-size \\\epsilon\\ of
    leap-frog integrator. Default is `NULL` which indicates that it will
    be adaptively selected during warm-up iterations.

  - `metric` The type of mass matrix; `"unit"`: diagonal matrix of ones,
    `"diag"`: diagonal matrix with positive diagonal entries estimated
    during warmup iterations (default), `"dense"`: a dense, symmetric
    positive definite matrix with entries estimated during warm-up
    iterations.

  - `delta` The target Metropolis acceptance rate. Default: 0.9.

  - `max.treedepth` The maximum tree depth in NUTS. Default: 6.

  - `int.time` The integration time in HMC. The number of leap-frog
    steps is calculated as \\L\_{\epsilon}=\lfloor t/\epsilon\rfloor\\.
    Default: 0.3.

- normalize:

  If `TRUE`, all covariates will be normalized to take values between
  \[0,1\].

- verbose:

  If `TRUE` (default), training progress will be printed.

- seed:

  Random number generation seed.

- ...:

  other parameters to pass to `control`.

## Value

An object of class `SPQR`. A list containing mostly internal model
fitting information to be used by helper functions.

## References

Xu SG, Reich BJ (2021). *Bayesian Nonparametric Quantile Process
Regression and Estimation of Marginal Quantile Effects.* Biometrics.
[doi:10.1111/biom.13576](https://doi.org/10.1111/biom.13576)

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
#> 
#> SPQR fitted using MCMC approach with ARD prior🚀
#> 
#> MCMC diagnostics:
#>   Final acceptance ratio is 0.95 and target is 0.9
#> 
#> Expected log pointwise predictive density (elpd) estimates:
#>   elpd.LOO = 90.10687,  elpd.WAIC = 89.59815
#> 
#> Elapsed time: 0.02 minutes

## plot estimated PDF
plotEstimator(fit, type = "PDF", X = 0)

# }
```
