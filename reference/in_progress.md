# List the targets in progress **\[deprecated\]**

Deprecated on 2019-01-13.

## Usage

``` r
in_progress(
  path = getwd(),
  search = TRUE,
  cache = drake::get_cache(path = path, search = search, verbose = verbose),
  verbose = 1L
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

## Value

A character vector of target names.

## Details

Similar to
[`progress()`](https://docs.ropensci.org/drake/reference/progress.md).

## See also

[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md),
[`drake_get_session_info()`](https://docs.ropensci.org/drake/reference/drake_get_session_info.md),
[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)
