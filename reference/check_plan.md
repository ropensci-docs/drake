# Check a workflow plan data frame for obvious errors. **\[deprecated\]**

Deprecated on 2019-01-12.

## Usage

``` r
check_plan(
  plan = NULL,
  targets = NULL,
  envir = parent.frame(),
  cache = drake::get_cache(verbose = verbose),
  verbose = 1L,
  jobs = 1
)
```

## Arguments

- plan:

  Workflow plan data frame, possibly from
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).

- targets:

  Character vector of targets to make.

- envir:

  Environment containing user-defined functions.

- cache:

  Optional drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).

- verbose:

  Deprecated on 2019-09-11.

- jobs:

  Number of jobs/workers for parallel processing.

## Value

Invisibly return `plan`.

## Details

Possible obvious errors include circular dependencies and missing input
files.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)
