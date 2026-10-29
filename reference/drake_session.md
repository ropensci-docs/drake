# Session info of the last call to [`make()`](https://docs.ropensci.org/drake/reference/make.md). **\[deprecated\]**

Deprecated. Use
[`drake_get_session_info()`](https://docs.ropensci.org/drake/reference/drake_get_session_info.md)
instead.

## Usage

``` r
drake_session(
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

[`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) of the last
call to [`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Details

Deprecated on 2018-12-06.
