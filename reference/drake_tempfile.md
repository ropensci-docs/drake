# drake tempfile **\[stable\]**

Create the path to a temporary file inside drake's cache.

## Usage

``` r
drake_tempfile(path = NULL, cache = drake::drake_cache(path = path))
```

## Arguments

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

## Details

This function is just like the
[`tempfile()`](https://rdrr.io/r/base/tempfile.html) function in base R
except that the path points to a special location inside `drake`'s
cache. This ensures that if the file needs to be copied to persistent
storage in the cache, `drake` does not need to copy across physical
storage media. Example: the `"diskframe"` format. See the "Formats" and
"Columns" sections of the
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
help file. Unless you supply the cache or the path to the cache (see
[`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md))
`drake` will assume the cache folder is named `.drake/` and it is
located either in your working directory or an ancestor of your working
directory.

## See also

[`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md),
[`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md)

## Examples

``` r
cache <- new_cache(tempfile())
# No need to supply a cache if a .drake/ folder exists.
drake_tempfile(cache = cache)
#> [1] "/tmp/RtmpI7oeBj/file61016693411/drake/tmp/file6107fcb725b"
drake_plan(
  x = target(
    as.disk.frame(large_data, outdir = drake_tempfile()),
    format = "diskframe"
  )
)
#> # A tibble: 1 × 3
#>   target command                                              format   
#>   <chr>  <expr_lst>                                           <chr>    
#> 1 x      as.disk.frame(large_data, outdir = drake_tempfile()) diskframe
```
