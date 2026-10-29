# Find the drake dependencies of a dynamic knitr report target. **\[stable\]**

Dependencies in `knitr` reports are marked by
[`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md) in
active code chunks.

## Usage

``` r
deps_knitr(path)
```

## Arguments

- path:

  Encoded file path to the `knitr`/R Markdown document. Wrap paths in
  [`file_store()`](https://docs.ropensci.org/drake/reference/file_store.md)
  to encode.

## Value

A data frame of dependencies.

## See also

[`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md),
[`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
load_mtcars_example() # Get the code with drake_example("mtcars").
deps_knitr("report.Rmd")
})
} # }
```
