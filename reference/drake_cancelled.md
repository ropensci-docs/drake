# List cancelled targets. **\[stable\]**

List the targets that were cancelled in the current or previous call to
[`make()`](https://docs.ropensci.org/drake/reference/make.md) using
[`cancel()`](https://docs.ropensci.org/drake/reference/cancel.md) or
[`cancel_if()`](https://docs.ropensci.org/drake/reference/cancel_if.md).

## Usage

``` r
drake_cancelled(cache = drake::drake_cache(path = path), path = NULL)
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
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
plan <- drake_plan(x = 1, y = cancel_if(x > 0))
make(plan)
drake_cancelled()
})
} # }
```
