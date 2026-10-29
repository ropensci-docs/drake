# Which targets will `clean()` invalidate? **\[stable\]**

`which_clean()` is a safety check for
[`clean()`](https://docs.ropensci.org/drake/reference/clean.md). It
shows you the targets that
[`clean()`](https://docs.ropensci.org/drake/reference/clean.md) will
invalidate (or remove if `garbage_collection` is `TRUE`). It helps you
avoid accidentally removing targets you care about.

## Usage

``` r
which_clean(
  ...,
  list = character(0),
  path = NULL,
  cache = drake::drake_cache(path = path)
)
```

## Arguments

- ...:

  Targets to remove from the cache: as names (symbols) or character
  strings. If the `tidyselect` package is installed, you can also supply
  `dplyr`-style `tidyselect` commands such as
  [`starts_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  [`ends_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  and [`one_of()`](https://tidyselect.r-lib.org/reference/one_of.html).

- list:

  Character vector naming targets to be removed from the cache. Similar
  to the `list` argument of
  [`remove()`](https://rdrr.io/r/base/rm.html).

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

## See also

[`clean()`](https://docs.ropensci.org/drake/reference/clean.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
plan <- drake_plan(x = 1, y = 2, z = 3)
make(plan)
cached()
which_clean(x, y) # [1] "x" "y"
clean(x, y)       # Invalidates targets x and y.
cached()          # [1] "z"
})
} # }
```
