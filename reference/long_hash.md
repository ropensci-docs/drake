# `drake` now has just one hash algorithm per cache. **\[deprecated\]**

Deprecated on 2018-12-12

## Usage

``` r
long_hash(cache = drake::get_cache(verbose = verbose), verbose = 1L)
```

## Arguments

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- verbose:

  Deprecated on 2019-09-11.

## Value

A character vector naming a hash algorithm.
