# List targets in the cache but not the plan. **\[stable\]**

Includes dynamic sub-targets as well. See examples for details.

## Usage

``` r
cached_unplanned(
  plan,
  path = NULL,
  cache = drake::drake_cache(path = path),
  namespace = NULL,
  jobs = 1
)
```

## Arguments

- plan:

  A drake plan.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- namespace:

  Character scalar, name of the storr namespace to use for listing
  objects.

- jobs:

  Number of jobs/workers for parallel processing.

## Value

A character vector of target and sub-target names.

## See also

[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[cached_planned](https://docs.ropensci.org/drake/reference/cached_planned.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("cache_unplanned() example", {
plan <- drake_plan(w = 1)
make(plan)
cached_unplanned(plan)
plan <- drake_plan(
  x = seq_len(2),
  y = target(x, dynamic = map(x))
)
cached_unplanned(plan)
make(plan)
cached_unplanned(plan)
# cached_unplanned() helps clean superfluous targets.
cached()
clean(list = cached_unplanned(plan))
cached()
})
} # }
```
