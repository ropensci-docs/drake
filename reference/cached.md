# List targets in the cache. **\[stable\]**

Tip: read/load a cached item with
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md) or
[`loadd()`](https://docs.ropensci.org/drake/reference/readd.md).

## Usage

``` r
cached(
  ...,
  list = character(0),
  no_imported_objects = FALSE,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  verbose = NULL,
  namespace = NULL,
  jobs = 1,
  targets_only = TRUE
)
```

## Arguments

- ...:

  Deprecated. Do not use. Objects to load from the cache, as names
  (unquoted) or character strings (quoted). Similar to `...` in
  [`remove()`](https://rdrr.io/r/base/rm.html).

- list:

  Deprecated. Do not use. Character vector naming objects to be loaded
  from the cache. Similar to the `list` argument of
  [`remove()`](https://rdrr.io/r/base/rm.html).

- no_imported_objects:

  Logical, deprecated. Use `targets_only` instead.

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

- namespace:

  Character scalar, name of the storr namespace to use for listing
  objects.

- jobs:

  Number of jobs/workers for parallel processing.

- targets_only:

  Logical. If `TRUE` just list the targets. If `FALSE`, list files and
  imported objects too.

## Value

Either a named logical indicating whether the given targets or cached or
a character vector listing all cached items, depending on whether any
targets are specified.

## See also

[`cached_planned()`](https://docs.ropensci.org/drake/reference/cached_planned.md),
[`cached_unplanned()`](https://docs.ropensci.org/drake/reference/cached_unplanned.md),
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
[`loadd()`](https://docs.ropensci.org/drake/reference/readd.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
if (requireNamespace("lubridate")) {
load_mtcars_example() # Load drake's canonical example.
make(my_plan) # Run the project, build all the targets.
cached()
cached(targets_only = FALSE)
}
}
})
} # }
```
