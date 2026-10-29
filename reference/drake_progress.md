# Get the build progress of your targets **\[stable\]**

Objects that drake imported, built, or attempted to build are listed as
`"done"` or `"running"`. Skipped objects are not listed.

## Usage

``` r
drake_progress(
  ...,
  list = character(0),
  cache = drake::drake_cache(path = path),
  path = NULL,
  progress = NULL
)
```

## Arguments

- ...:

  Objects to load from the cache, as names (unquoted) or character
  strings (quoted). If the `tidyselect` package is installed, you can
  also supply `dplyr`-style `tidyselect` commands such as
  [`starts_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  [`ends_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  and [`one_of()`](https://tidyselect.r-lib.org/reference/one_of.html).

- list:

  Character vector naming objects to be loaded from the cache. Similar
  to the `list` argument of
  [`remove()`](https://rdrr.io/r/base/rm.html).

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- progress:

  Character vector for filtering the build progress results. Defaults to
  `NULL` (no filtering) to report progress of all objects. Supported
  filters are `"done"`, `"running"`, and `"failed"`.

## Value

The build progress of each target reached by the current
[`make()`](https://docs.ropensci.org/drake/reference/make.md) so far.

## See also

[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md),
[`drake_get_session_info()`](https://docs.ropensci.org/drake/reference/drake_get_session_info.md),
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
# Watch the changing drake_progress() as make() is running.
drake_progress() # List all the targets reached so far.
drake_progress(small, large) # Just see the progress of some targets.
drake_progress(list = c("small", "large")) # Same as above.
}
})
} # }
```
