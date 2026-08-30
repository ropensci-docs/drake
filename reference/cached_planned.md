# List targets in both the plan and the cache. **\[stable\]**

Includes dynamic sub-targets as well. See examples for details.

## Usage

``` r
cached_planned(
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
[cached_unplanned](https://docs.ropensci.org/drake/reference/cached_unplanned.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("cache_planned() example", {
plan <- drake_plan(w = 1)
make(plan)
cached_planned(plan)
plan <- drake_plan(
  x = seq_len(2),
  y = target(x, dynamic = map(x))
)
cached_planned(plan)
make(plan)
cached_planned(plan)
cached()
})
} # }
```
