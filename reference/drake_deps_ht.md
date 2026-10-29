# `drake_deps_ht` helper

Static code analysis.

## Usage

``` r
drake_deps_ht(expr, exclude = character(0), restrict = NULL)
```

## Arguments

- expr:

  An R expression

- exclude:

  Character vector of the names of symbols to exclude from the code
  analysis.

- restrict:

  Optional character vector of allowable names of globals. If `NULL`,
  all global symbols are detectable. If a character vector, only the
  variables in `restrict` will count as global variables.

## Value

A `drake_deps_ht` object.

## Examples

``` r
if (FALSE) { # stronger than roxygen dontrun
expr <- quote({
  a <- base::list(1)
  b <- seq_len(10)
  file_out("abc")
  file_in("xyz")
  x <- "123"
  loadd(abc)
  readd(xyz)
})
drake_deps_ht(expr)
}
```
