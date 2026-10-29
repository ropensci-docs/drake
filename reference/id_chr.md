# Name of the current target **\[stable\]**

`id_chr()` gives you the name of the current target while
[`make()`](https://docs.ropensci.org/drake/reference/make.md) is
running. For static branching in
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
use the `.id_chr` symbol instead. See the examples for details.

## Usage

``` r
id_chr()
```

## Value

The name of the current target.

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

- [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md):
  force `drake` to entirely ignore a piece of code: do not track it for
  changes and do not analyze it for dependencies.

- [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md):
  tell `drake` to not track the dependencies of a piece of code. `drake`
  still tracks the code itself for changes.

- `id_chr()`: Get the name of the current target.

- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md):
  get the environment where drake builds targets. Intended for advanced
  custom memory management.

## Examples

``` r
try(id_chr()) # Do not use outside the plan.
#> Error : Could not find the environment where drake builds targets. Functions drake_envir(), id_chr(), cancel(), and cancel_if() can only be invoked through make().
if (FALSE) { # \dontrun{
isolate_example("id_chr()", {
plan <- drake_plan(x = id_chr())
make(plan)
readd(x)
# Dynamic branching
plan <- drake_plan(
  x = seq_len(4),
  y = target(id_chr(), dynamic = map(x))
)
make(plan)
readd(y, subtargets = 1)
# Static branching
plan <- drake_plan(
  y = target(c(x, .id_chr), transform = map(x = !!seq_len(4)))
)
plan
})
} # }
```
