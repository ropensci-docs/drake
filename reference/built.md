# List all the built targets (non-imports) in the cache. **\[deprecated\]**

Deprecated on 2019-01-08.

## Usage

``` r
built(
  path = getwd(),
  search = TRUE,
  cache = drake::get_cache(path = path, search = search, verbose = verbose),
  verbose = 1L,
  jobs = 1
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

## Value

Character vector naming the built targets in the cache.

## Details

Targets are listed in the workflow plan data frame (see
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).

## See also

[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
