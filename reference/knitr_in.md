# Declare `knitr`/`rmarkdown` source files as dependencies. **\[stable\]**

`knitr_in()` marks individual `knitr`/R Markdown reports as
dependencies. In `drake`, these reports are pieces of the pipeline. R
Markdown is a great tool for *displaying* precomputed results, but not
for running a large workflow from end to end. These reports should do as
little computation as possible.

## Usage

``` r
knitr_in(...)
```

## Arguments

- ...:

  Character strings. File paths of `knitr`/`rmarkdown` source files
  supplied to a command in your workflow plan data frame.

## Value

A character vector of declared input file paths.

## Details

Unlike
[`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md) and
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
`knitr_in()` does not work with entire directories.

## Keywords

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
understands special keyword functions for your commands. With the
exception of
[`target()`](https://docs.ropensci.org/drake/reference/target.md), each
one is a proper function with its own help file.

- [`target()`](https://docs.ropensci.org/drake/reference/target.md):
  give the target more than just a command. Using
  [`target()`](https://docs.ropensci.org/drake/reference/target.md), you
  can apply a transformation (examples:
  `https://books.ropensci.org/drake/plans.html#large-plans`), \# nolint
  supply a trigger (`https://books.ropensci.org/drake/triggers.html`),
  \# nolint or set any number of custom columns.

- [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md):
  declare an input file dependency.

- [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md):
  declare an output file to be produced when the target is built.

- `knitr_in()`: declare a `knitr` file dependency such as an R Markdown
  (`*.Rmd`) or R LaTeX (`*.Rnw`) file.

- [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md):
  force `drake` to entirely ignore a piece of code: do not track it for
  changes and do not analyze it for dependencies.

- [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md):
  tell `drake` to not track the dependencies of a piece of code. `drake`
  still tracks the code itself for changes.

- [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md): Get
  the name of the current target.

- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md):
  get the environment where drake builds targets. Intended for advanced
  custom memory management.

## See also

[`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md),
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
[`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md),
[`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
if (requireNamespace("knitr", quietly = TRUE)) {
# `knitr_in()` is like `file_in()`
# except that it analyzes active code chunks in your `knitr`
# source file and detects non-file dependencies.
# That way, updates to the right dependencies trigger rebuilds
# in your report.
# The mtcars example (`drake_example("mtcars")`)
# already has a demonstration

load_mtcars_example()
make(my_plan)

# Now how did drake magically know that
# `small`, `large`, and `coef_regression2_small` were
# dependencies of the output file `report.md`?
# because the command in the workflow plan had
# `knitr_in("report.Rmd")` in it, so drake knew
# to analyze the active code chunks. There, it spotted
# where `small`, `large`, and `coef_regression2_small`
# were read from the cache using calls to `loadd()` and `readd()`.
}
})
} # }
```
