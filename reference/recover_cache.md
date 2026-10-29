# Load or create a drake cache **\[deprecated\]**

Deprecated on 2019-01-13.

## Usage

``` r
recover_cache(
  path = NULL,
  hash_algorithm = NULL,
  short_hash_algo = NULL,
  long_hash_algo = NULL,
  force = FALSE,
  verbose = 1L,
  fetch_cache = NULL,
  console_log_file = NULL
)
```

## Arguments

- path:

  File path of the cache.

- hash_algorithm:

  Name of a hash algorithm to use. See the `algo` argument of the
  `digest` package for your options.

- short_hash_algo:

  Deprecated on 2018-12-12. Use `hash_algorithm` instead.

- long_hash_algo:

  Deprecated on 2018-12-12. Use `hash_algorithm` instead.

- force:

  Logical, whether to load the cache despite any back compatibility
  issues with the running version of drake.

- verbose:

  Deprecated on 2019-09-11.

- fetch_cache:

  Deprecated.

- console_log_file:

  Deprecated on 2019-09-11.

## Value

A drake/storr cache.

## Details

Does not work with in-memory caches such as
[`storr::storr_environment()`](https://richfitz.github.io/storr/reference/storr_environment.html).

## See also

[`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md),
[`get_cache()`](https://docs.ropensci.org/drake/reference/get_cache.md)
