# Get the environment where drake builds targets **\[questioning\]**

Call this function inside the commands in your plan to get the
environment where `drake` builds targets. Advanced users can use it to
strategically remove targets from memory while
[`make()`](https://docs.ropensci.org/drake/reference/make.md) is
running.

## Usage

``` r
drake_envir(which = c("targets", "dynamic", "subtargets", "imports"))
```

## Arguments

- which:

  Character of length 1, which environment to select. See the details of
  this help file.

## Value

The environment where `drake` builds targets.

## Details

`drake` manages in-memory targets in 4 environments: one with
sub-targets, one with whole dynamic targets, one with static targets,
and one with imported global objects and functions. This last
environment is usually the environment from which you call
[`make()`](https://docs.ropensci.org/drake/reference/make.md). Select
the appropriate environment for your use case with the `which` argument
of `drake_envir()`.

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

- [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md): Get
  the name of the current target.

- `drake_envir()`: get the environment where drake builds targets.
  Intended for advanced custom memory management.

## See also

[`from_plan()`](https://docs.ropensci.org/drake/reference/from_plan.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
plan <- drake_plan(
  large_data_1 = sample.int(1e4),
  large_data_2 = sample.int(1e4),
  subset = c(large_data_1[seq_len(10)], large_data_2[seq_len(10)]),
  summary = {
    print(ls(envir = parent.env(drake_envir())))
    # We don't need the large_data_* targets in memory anymore.
    rm(large_data_1, large_data_2, envir = drake_envir("targets"))
    print(ls(envir = drake_envir("targets")))
    mean(subset)
  }
)
make(plan, cache = storr::storr_environment(), session_info = FALSE)
})
} # }
```
