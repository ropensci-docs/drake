# Generate a flat text log file to represent the state of the cache. **\[deprecated\]**

Deprecated on 2019-03-09.

## Usage

``` r
drake_cache_log_file(
  file = "drake_cache.log",
  path = getwd(),
  search = TRUE,
  cache = drake::get_cache(path = path, search = search, verbose = verbose),
  verbose = 1L,
  jobs = 1L,
  targets_only = FALSE
)
```

## Arguments

- file:

  character scalar, name of the flat text log file.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- verbose:

  Deprecated on 2019-09-11.

- jobs:

  Number of jobs/workers for parallel processing.

- targets_only:

  Logical, whether to output information only on the targets in your
  workflow plan data frame. If `targets_only` is `FALSE`, the output
  will include the hashes of both targets and imports.

## Value

There is no return value, but a log file is generated.

## Details

Calling this function to create a log file and later calling
[`make()`](https://docs.ropensci.org/drake/reference/make.md) makes the
log file out of date. Therefore, we recommend using
[`make()`](https://docs.ropensci.org/drake/reference/make.md) with the
`cache_log_file` argument to create the cache log. This way ensures that
the log is always up to date with
[`make()`](https://docs.ropensci.org/drake/reference/make.md) results.

## See also

[`drake_cache_log()`](https://docs.ropensci.org/drake/reference/drake_cache_log.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md),
[`get_cache()`](https://docs.ropensci.org/drake/reference/get_cache.md)
