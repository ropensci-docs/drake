# `drake_deps` constructor

List of class `drake_deps`.

## Usage

``` r
new_drake_deps(
  globals = character(0),
  namespaced = character(0),
  strings = character(0),
  loadd = character(0),
  readd = character(0),
  file_in = character(0),
  file_out = character(0),
  knitr_in = character(0)
)
```

## Arguments

- globals:

  Global symbols found in the expression

- namespaced:

  Namespaced objects, e.g.
  [`rmarkdown::render`](https://pkgs.rstudio.com/rmarkdown/reference/render.html).

- strings:

  Miscellaneous strings.

- loadd:

  Targets selected with
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md).

- readd:

  Targets selected with
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md).

- file_in:

  Literal static file paths enclosed in
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md).

- file_out:

  Literal static file paths enclosed in
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md).

- knitr_in:

  Literal static file paths enclosed in
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md).

## Value

A `drake_deps` object.

## Examples

``` r
if (FALSE) { # stronger than roxygen dontrun
new_drake_deps()
}
```
