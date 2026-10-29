# List failed targets. **\[stable\]**

List the targets that quit in error during
[`make()`](https://docs.ropensci.org/drake/reference/make.md).

## Usage

``` r
drake_failed(cache = drake::drake_cache(path = path), path = NULL)
```

## Arguments

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

## Value

A character vector of target names.

## See also

[`drake_done()`](https://docs.ropensci.org/drake/reference/drake_done.md),
[`drake_running()`](https://docs.ropensci.org/drake/reference/drake_running.md),
[`drake_cancelled()`](https://docs.ropensci.org/drake/reference/drake_cancelled.md),
[`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
if (suppressWarnings(require("knitr"))) {
# Build a plan doomed to fail:
bad_plan <- drake_plan(x = function_doesnt_exist())
cache <- storr::storr_environment() # optional
try(
  make(bad_plan, cache = cache, history = FALSE),
  silent = TRUE
) # error
drake_failed(cache = cache) # "x"
e <- diagnose(x, cache = cache) # Retrieve the cached error log of x.
names(e)
e$error
names(e$error)
}
})
} # }
```
