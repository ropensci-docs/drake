# Get the build progress of your targets **\[deprecated\]**

Deprecated on 2020-03-23. Use
[`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md)
instead.

## Usage

``` r
progress(
  ...,
  list = character(0),
  no_imported_objects = NULL,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  verbose = 1L,
  jobs = 1,
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

- no_imported_objects:

  Logical, whether to only return information about imported files and
  targets with commands (i.e. whether to ignore imported objects that
  are not files).

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

- jobs:

  Number of jobs/workers for parallel processing.

- progress:

  Character vector for filtering the build progress results. Defaults to
  `NULL` (no filtering) to report progress of all objects. Supported
  filters are `"done"`, `"running"`, and `"failed"`.

## Value

The build progress of each target reached by the current
[`make()`](https://docs.ropensci.org/drake/reference/make.md) so far.
