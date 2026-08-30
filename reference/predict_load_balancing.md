# Predict parallel computing behavior **\[deprecated\]**

Deprecated on 2019-02-14.

## Usage

``` r
predict_load_balancing(
  config,
  targets = NULL,
  from_scratch = FALSE,
  targets_only = NULL,
  jobs = 1,
  known_times = numeric(0),
  default_time = 0,
  warn = TRUE
)
```

## Arguments

- config:

  Deprecated.

- from_scratch:

  Logical, whether to predict a
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) build
  from scratch or to take into account the fact that some targets may be
  already up to date and therefore skipped.

- targets_only:

  Deprecated.

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

## Value

A data frame showing one likely arrangement of targets assigned to
parallel workers.
