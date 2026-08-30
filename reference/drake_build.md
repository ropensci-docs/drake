# Build/process a single target or import. **\[questioning\]**

Not valid for dynamic branching.

## Usage

``` r
drake_build(
  target,
  ...,
  meta = NULL,
  character_only = FALSE,
  replace = FALSE,
  config = NULL
)
```

## Arguments

- target:

  Name of the target.

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  the plan and environment.

- meta:

  Deprecated.

- character_only:

  Logical, whether `name` should be treated as a character or a symbol
  (just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html)).

- replace:

  Logical. If `FALSE`, items already in your environment will not be
  replaced.

- config:

  Deprecated 2019-12-22.

## Value

The value of the target right after it is built.

## See also

[`drake_debug()`](https://docs.ropensci.org/drake/reference/drake_debug.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
# This example is not really a user-side demonstration.
# It just walks through a dive into the internals.
# Populate your workspace and write 'report.Rmd'.
load_mtcars_example() # Get the code with drake_example("mtcars").
out <- drake_build(small, my_plan)
# Now includes `small`.
cached()
head(readd(small))
# `small` was invisibly returned.
head(out)
}
})
} # }
```
