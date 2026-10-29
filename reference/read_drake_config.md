# Read a config object from the cache **\[deprecated\]**

drake no longer stores the config object, the plan, etc. in the cache
during [`make()`](https://docs.ropensci.org/drake/reference/make.md).
This change improves speed.

## Usage

``` r
read_drake_config(
  path = getwd(),
  search = TRUE,
  cache = NULL,
  verbose = 1L,
  jobs = 1,
  envir = parent.frame()
)
```

## Arguments

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

## Details

2019-01-06
