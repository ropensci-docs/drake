# Search up the file system for the nearest drake cache. **\[stable\]**

Only works if the cache is a file system in a hidden folder named
`.drake/` (default).

## Usage

``` r
find_cache(path = getwd(), dir = NULL, directory = NULL)
```

## Arguments

- path:

  Starting path for search back for the cache. Should be a subdirectory
  of the drake project.

- dir:

  Character, name of the folder containing the cache.

- directory:

  Deprecated. Use `dir`.

## Value

File path of the nearest drake cache or `NULL` if no cache is found.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md),

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the target.
# Find the file path of the project's cache.
# Search up through parent directories if necessary.
find_cache()
}
})
} # }
```
