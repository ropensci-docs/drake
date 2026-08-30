# Do garbage collection on the drake cache. **\[stable\]**

Garbage collection removes obsolete target values from the cache.

## Usage

``` r
drake_gc(
  path = NULL,
  search = NULL,
  verbose = NULL,
  cache = drake::drake_cache(path = path),
  force = FALSE
)
```

## Arguments

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- verbose:

  Deprecated on 2019-09-11.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- force:

  Logical, whether to load the cache despite any back compatibility
  issues with the running version of drake.

## Value

`NULL`

## Details

Caution: garbage collection *actually* removes data so it is no longer
recoverable with
[`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md)
or `make(recover = TRUE)`. You cannot undo this operation. Use at your
own risk.

## See also

[`clean()`](https://docs.ropensci.org/drake/reference/clean.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
# At this point, check the size of the '.drake/' cache folder.
# Clean without garbage collection.
clean(garbage_collection = FALSE)
# The '.drake/' cache folder is still about the same size.
drake_gc() # Do garbage collection on the cache.
# The '.drake/' cache folder should have gotten much smaller.
}
})
} # }
```
