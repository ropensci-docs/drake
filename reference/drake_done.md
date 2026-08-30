# List done targets. **\[stable\]**

List the targets that completed in the current or previous call to
[`make()`](https://docs.ropensci.org/drake/reference/make.md).

## Usage

``` r
drake_done(cache = drake::drake_cache(path = path), path = NULL)
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

[`drake_running()`](https://docs.ropensci.org/drake/reference/drake_running.md),
[`drake_failed()`](https://docs.ropensci.org/drake/reference/drake_failed.md),
[`drake_cancelled()`](https://docs.ropensci.org/drake/reference/drake_cancelled.md),
[`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
plan <- drake_plan(x = 1, y = x)
make(plan)
drake_done()
})
} # }
```
