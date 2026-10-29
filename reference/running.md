# List running targets. **\[deprecated\]**

Deprecated on 2020-03-23. Use
[`drake_running()`](https://docs.ropensci.org/drake/reference/drake_running.md)
instead.

## Usage

``` r
running(
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
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
