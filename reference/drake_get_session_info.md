# Session info of the last call to [`make()`](https://docs.ropensci.org/drake/reference/make.md). **\[stable\]**

By default, session info is saved during
[`make()`](https://docs.ropensci.org/drake/reference/make.md) to ensure
reproducibility. Your loaded packages and their versions are recorded,
for example.

## Usage

``` r
drake_get_session_info(
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  verbose = 1L
)
```

## Arguments

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- verbose:

  Deprecated on 2019-09-11.

## Value

[`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) of the last
call to [`make()`](https://docs.ropensci.org/drake/reference/make.md)

## See also

[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md),
[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
drake_get_session_info() # Get the cached sessionInfo() of the last make().
}
})
} # }
```
