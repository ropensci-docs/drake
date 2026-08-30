# Get the cache at the exact file path specified. **\[deprecated\]**

This function does not apply to in-memory caches such as
`storr_environment()`.

## Usage

``` r
this_cache(
  path = NULL,
  force = FALSE,
  verbose = 1L,
  fetch_cache = NULL,
  console_log_file = NULL
)
```

## Arguments

- path:

  File path of the cache.

- force:

  Deprecated.

- verbose:

  Deprecated on 2019-09-11.

- fetch_cache:

  Deprecated.

- console_log_file:

  Deprecated in favor of `log_make`.

## Value

A drake/storr cache at the specified path, if it exists.
