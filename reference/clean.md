# Invalidate and deregister targets. **\[stable\]**

Force targets to be out of date and remove target names from the data in
the cache. Be careful and run
[`which_clean()`](https://docs.ropensci.org/drake/reference/which_clean.md)
before `clean()`. That way, you know beforehand which targets will be
compromised.

## Usage

``` r
clean(
  ...,
  list = character(0),
  destroy = FALSE,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  verbose = NULL,
  jobs = NULL,
  force = FALSE,
  garbage_collection = FALSE,
  purge = FALSE
)
```

## Arguments

- ...:

  Symbols, individual targets to remove.

- list:

  Character vector of individual targets to remove.

- destroy:

  Logical, whether to totally remove the drake cache. If `destroy` is
  `FALSE`, only the targets from
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) are
  removed. If `TRUE`, the whole cache is removed, including session
  metadata, etc.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- verbose:

  Deprecated

- jobs:

  Deprecated.

- force:

  Logical, whether to try to clean the cache even though the project may
  not be back compatible with the current version of drake.

- garbage_collection:

  Logical, whether to call `cache$gc()` to do garbage collection. If
  `TRUE`, cached data with no remaining references will be removed. This
  will slow down `clean()`, but the cache could take up far less space
  afterwards. See the [`gc()`](https://rdrr.io/r/base/gc.html) method
  for `storr` caches.

- purge:

  Logical, whether to remove objects from metadata namespaces such as
  "meta", "build_times", and "errors".

## Value

Invisibly return `NULL`.

## Details

By default, `clean()` invalidates **all** targets, so be careful.
`clean()` always:

1.  Forces targets to be out of date so the next
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) does
    not skip them.

2.  Deregisters targets so `loadd(your_target)` and `readd(your_target)`
    no longer work.

By default, `clean()` does not actually remove the underlying data. Even
old targets from the distant past are still in the cache and recoverable
via
[`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md)
and `make(recover = TRUE)`. To actually remove target data from the
cache, as well as any
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
files from any targets you are currently cleaning, run
`clean(garbage_collection = TRUE)`. Garbage collection is slow, but it
reduces the storage burden of the cache.

## See also

[`which_clean()`](https://docs.ropensci.org/drake/reference/which_clean.md),
[`drake_gc()`](https://docs.ropensci.org/drake/reference/drake_gc.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
# Show all registered targets in the cache.
cached()
# Deregister 'summ_regression1_large' and 'small' in the cache.
clean(summ_regression1_large, small)
# Those objects are no longer registered as targets.
cached()
# Rebuild the invalidated/outdated targets.
make(my_plan)
# Clean everything.
clean()
# But the data objects and files are not actually gone!
file.exists("report.md")
drake_history()
make(my_plan, recover = TRUE)
# You need garbage collection to actually remove the data
# and any file_out() files of any uncleaned targets.
clean(garbage_collection = TRUE)
drake_history()
make(my_plan, recover = TRUE)
}
})
} # }
```
