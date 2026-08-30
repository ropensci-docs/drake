# Report any import objects required by your drake_plan plan but missing from your workspace or file system. **\[stable\]**

Checks your workspace/environment and file system.

## Usage

``` r
missed(..., config = NULL)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- config:

  Deprecated.

## Value

Character vector of names of missing objects and files.

## See also

[`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
plan <- drake_plan(x = missing::fun(arg))
missed(plan)
}
})
} # }
```
