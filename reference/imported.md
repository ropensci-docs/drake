# List all the imports in the drake cache. **\[deprecated\]**

Deprecated on 2019-01-08.

## Usage

``` r
imported(
  files_only = FALSE,
  path = getwd(),
  search = TRUE,
  cache = drake::get_cache(path = path, search = search, verbose = verbose),
  verbose = 1L,
  jobs = 1
)
```

## Arguments

- files_only:

  Logical, whether to show imported files only and ignore imported
  objects. Since all your functions and all their global variables are
  imported, the full list of imported objects could get really
  cumbersome.

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

Character vector naming the imports in the cache.

## Details

An import is a non-target object processed by
[`make()`](https://docs.ropensci.org/drake/reference/make.md). Targets
in the workflow plan data frame (see
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
may depend on imports.

## See also

[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
