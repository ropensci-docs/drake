# Run a single target's command in debug mode.' **\[questioning\]**

Not valid for dynamic branching. `drake_debug()` loads a target's
dependencies and then runs its command in debug mode (see
[`browser()`](https://rdrr.io/r/base/browser.html),
[`debug()`](https://rdrr.io/r/base/debug.html), and
[`debugonce()`](https://rdrr.io/r/base/debug.html)). This function does
not store the target's value in the cache (see
`https://github.com/ropensci/drake/issues/587`).

## Usage

``` r
drake_debug(
  target = NULL,
  ...,
  character_only = FALSE,
  replace = FALSE,
  verbose = TRUE,
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

- character_only:

  Logical, whether `name` should be treated as a character or a symbol
  (just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html)).

- replace:

  Logical. If `FALSE`, items already in your environment will not be
  replaced.

- verbose:

  Logical, whether to print out the target you are debugging.

- config:

  Deprecated 2019-12-22.

## Value

The value of the target right after it is built.

## See also

[`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
# This example is not really a user-side demonstration.
# It just walks through a dive into the internals.
# Populate your workspace and write 'report.Rmd'.
load_mtcars_example() # Get the code with drake_example("mtcars").
# out <- drake_debug(small, my_plan)
# `small` was invisibly returned.
# head(out)
}
})
} # }
```
