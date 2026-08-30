# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
predict_workers_impl(
  config,
  targets_predict = NULL,
  from_scratch = FALSE,
  targets_only = NULL,
  jobs_predict = 1,
  known_times = numeric(0),
  default_time = 0,
  warn = TRUE
)
```

## Arguments

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.
