# See the time it took to build each target. **\[stable\]**

Applies to targets in your plan, not imports or files.

## Usage

``` r
build_times(
  ...,
  path = NULL,
  search = NULL,
  digits = 3,
  cache = drake::drake_cache(path = path),
  targets_only = NULL,
  verbose = NULL,
  jobs = 1,
  type = c("build", "command"),
  list = character(0)
)
```

## Arguments

- ...:

  Targets to load from the cache: as names (symbols) or character
  strings. If the `tidyselect` package is installed, you can also supply
  `dplyr`-style `tidyselect` commands such as
  [`starts_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  [`ends_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  and [`one_of()`](https://tidyselect.r-lib.org/reference/one_of.html).

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- digits:

  How many digits to round the times to.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- targets_only:

  Deprecated.

- verbose:

  Deprecated on 2019-09-11.

- jobs:

  Number of jobs/workers for parallel processing.

- type:

  Type of time you want: either `"build"` for the full build time
  including the time it took to store the target, or `"command"` for the
  time it took just to run the command.

- list:

  Character vector of targets to select.

## Value

A data frame of times, each from
[`system.time()`](https://rdrr.io/r/base/system.time.html).

## Details

Times for dynamic targets
(`https://books.ropensci.org/drake/dynamic.html`) only reflect the time
it takes to post-process the sub-targets (typically very fast) and
exclude the time it takes to build the sub-targets themselves.
Sub-targets build times are listed individually.

## See also

[`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
if (requireNamespace("lubridate")) {
# Show the build times for the mtcars example.
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Build all the targets.
print(build_times()) # Show how long it took to build each target.
}
}
})
} # }
```
