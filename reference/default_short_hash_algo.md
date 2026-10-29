# Return the default short hash algorithm for `make()`. **\[deprecated\]**

Deprecated. drake now only uses one hash algorithm per cache.

## Usage

``` r
default_short_hash_algo(cache = NULL)
```

## Arguments

- cache:

  Optional drake cache. When you
  [`configure_cache()`](https://docs.ropensci.org/drake/reference/configure_cache.md)
  without supplying a short hash algorithm,
  `default_short_hash_algo(cache)` is the short hash algorithm that
  drake picks for you.

## Value

A character vector naming a hash algorithm.

## Details

Deprecated on 2018-12-12
