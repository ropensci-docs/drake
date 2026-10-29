# Return the file path where the cache is stored, if applicable. **\[deprecated\]**

Deprecated on 2019-01-12.

## Usage

``` r
cache_path(cache = NULL)
```

## Arguments

- cache:

  The cache whose file path you want to know.

## Value

File path where the cache is stored.

## Details

Currently only works with
[`storr::storr_rds()`](https://richfitz.github.io/storr/reference/storr_rds.html)
file system caches.
