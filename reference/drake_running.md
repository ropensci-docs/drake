# List running targets. **\[stable\]**

List the targets that either

1.  Are currently being built during a call to
    [`make()`](https://docs.ropensci.org/drake/reference/make.md), or

2.  Were in progress when
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) was
    interrupted.

## Usage

``` r
drake_running(cache = drake::drake_cache(path = path), path = NULL)
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
[`drake_failed()`](https://docs.ropensci.org/drake/reference/drake_failed.md),
[`drake_cancelled()`](https://docs.ropensci.org/drake/reference/drake_cancelled.md),
[`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
drake_running() # Everything should be done.
# nolint start
# Run make() in one R session...
# slow_plan <- drake_plan(x = Sys.sleep(2))
# make(slow_plan)
# and see the progress in another session.
# drake_running()
# nolint end
}
})
} # }
```
