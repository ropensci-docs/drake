# Ignore code **\[stable\]**

Ignore sections of commands and imported functions.

## Usage

``` r
ignore(x = NULL)
```

## Arguments

- x:

  Code to ignore.

## Value

The argument.

## Details

In user-defined functions and
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
commands, you can wrap code chunks in `ignore()` to

1.  Tell `drake` to not search for dependencies (targets etc. mentioned
    in the code) and

2.  Ignore changes to the code so downstream targets remain up to date.
    To enforce (1) without (2), use
    [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md).

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

- [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md):
  declare a `knitr` file dependency such as an R Markdown (`*.Rmd`) or R
  LaTeX (`*.Rnw`) file.

- `ignore()`: force `drake` to entirely ignore a piece of code: do not
  track it for changes and do not analyze it for dependencies.

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
[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md),
[`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Contain side effects", {
# Normally, `drake` reacts to changes in dependencies.
x <- 4
make(plan = drake_plan(y = sqrt(x)))
x <- 5
make(plan = drake_plan(y = sqrt(x)))
make(plan = drake_plan(y = sqrt(4) + x))
# But not with ignore().
make(plan = drake_plan(y = sqrt(4) + ignore(x))) # Builds y.
x <- 6
make(plan = drake_plan(y = sqrt(4) + ignore(x))) # Skips y.
make(plan = drake_plan(y = sqrt(4) + ignore(x + 1))) # Skips y.

# ignore() works with functions and multiline code chunks.
f <- function(x) {
  ignore({
    x <- x + 1
    x <- x + 2
  })
  x # Not ignored.
}
make(plan = drake_plan(y = f(2)))
readd(x)
# Changes the content of the ignore() block:
f <- function(x) {
  ignore({
    x <- x + 1
  })
  x # Not ignored.
}
make(plan = drake_plan(x = f(2)))
readd(x)
})
} # }
```
