# List the dependencies of a target **\[stable\]**

Intended for debugging and checking your project. The dependency
structure of the components of your analysis decides which targets are
built and when.

## Usage

``` r
deps_target(target, ..., character_only = FALSE, config = NULL)
```

## Arguments

- target:

  A symbol denoting a target name, or if `character_only` is TRUE, a
  character scalar denoting a target name.

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- character_only:

  Logical, whether to assume target is a character string rather than a
  symbol.

- config:

  Deprecated.

## Value

A data frame with the dependencies listed by type (globals, files, etc).

## See also

[`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md),
[`deps_knitr()`](https://docs.ropensci.org/drake/reference/deps_knitr.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
load_mtcars_example() # Get the code with drake_example("mtcars").
deps_target(regression1_small, my_plan)
})
} # }
```
