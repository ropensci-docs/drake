# Write an example `_drake.R` script to the current working directory.

A `_drake.R` file is required for
[`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) and
friends. See the
[`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) help
file for details.

## Usage

``` r
drake_script(code = NULL)
```

## Arguments

- code:

  R code to put in `_drake.R` in the current working directory. If
  `NULL`, an example script is written.

## Value

Nothing.

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side-effects", {
drake_script({
  library(drake)
  plan <- drake_plan(x = 1)
  drake_config(plan, lock_cache = FALSE)
})
cat(readLines("_drake.R"), sep = "\n")
r_make()
})
} # }
```
