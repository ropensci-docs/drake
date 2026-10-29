# Predict the load balancing of the next call to `make()` for non-staged parallel backends. **\[stable\]**

Take the past recorded runtimes times from
[`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md)
and use them to predict how the targets will be distributed among the
available workers in the next
[`make()`](https://docs.ropensci.org/drake/reference/make.md).
Predictions only include the time it takes to run the targets, not
overhead/preprocessing from `drake` itself.

## Usage

``` r
predict_workers(
  ...,
  targets_predict = NULL,
  from_scratch = FALSE,
  targets_only = NULL,
  jobs_predict = 1L,
  known_times = numeric(0),
  default_time = 0,
  warn = TRUE,
  config = NULL
)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- targets_predict:

  Character vector, names of targets to include in the total runtime and
  worker predictions.

- from_scratch:

  Logical, whether to predict a
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) build
  from scratch or to take into account the fact that some targets may be
  already up to date and therefore skipped.

- targets_only:

  Deprecated.

- jobs_predict:

  The `jobs` argument of your next planned
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).

- known_times:

  A named numeric vector with targets/imports as names and values as
  hypothetical runtimes in seconds. Use this argument to overwrite any
  of the existing build times or the `default_time`.

- default_time:

  Number of seconds to assume for any target or import with no recorded
  runtime (from
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md))
  or anything in `known_times`.

- warn:

  Logical, whether to warn the user about any targets with no available
  runtime, either in `known_times` or
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md).
  The times for these targets default to `default_time`.

- config:

  Deprecated.

## Value

A data frame showing one likely arrangement of targets assigned to
parallel workers.

## See also

[`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md),
[`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
known_times <- rep(7200, nrow(my_plan))
names(known_times) <- my_plan$target
known_times
# Predict the runtime
if (requireNamespace("lubridate", quietly = TRUE)) {
predict_runtime(
  my_plan,
  jobs_predict = 7L,
  from_scratch = TRUE,
  known_times = known_times
)
predict_runtime(
  my_plan,
  jobs_predict = 8L,
  from_scratch = TRUE,
  known_times = known_times
)
balance <- predict_workers(
  my_plan,
  jobs_predict = 7L,
  from_scratch = TRUE,
  known_times = known_times
)
balance
}
}
})
} # }
```
