# Launch a drake function in a fresh new R process **\[stable\]**

The `r_*()` functions, such as `r_make()`, enhance reproducibility by
launching a `drake` function in a separate R process.

## Usage

``` r
r_make(source = NULL, r_fn = NULL, r_args = list())

r_drake_build(
  target,
  character_only = FALSE,
  ...,
  source = NULL,
  r_fn = NULL,
  r_args = list()
)

r_outdated(..., source = NULL, r_fn = NULL, r_args = list())

r_recoverable(..., source = NULL, r_fn = NULL, r_args = list())

r_missed(..., source = NULL, r_fn = NULL, r_args = list())

r_deps_target(
  target,
  character_only = FALSE,
  ...,
  source = NULL,
  r_fn = NULL,
  r_args = list()
)

r_drake_graph_info(..., source = NULL, r_fn = NULL, r_args = list())

r_vis_drake_graph(..., source = NULL, r_fn = NULL, r_args = list())

r_sankey_drake_graph(..., source = NULL, r_fn = NULL, r_args = list())

r_drake_ggraph(..., source = NULL, r_fn = NULL, r_args = list())

r_text_drake_graph(..., source = NULL, r_fn = NULL, r_args = list())

r_predict_runtime(..., source = NULL, r_fn = NULL, r_args = list())

r_predict_workers(..., source = NULL, r_fn = NULL, r_args = list())
```

## Arguments

- source:

  Path to an R script file that loads packages, functions, etc. and
  returns a
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object. There are 3 ways to set this path.

  1.  Pass an explicit file path.

  2.  Call `options(drake_source = "path_to_your_script.R")`.

  3.  Just create a file called "\_drake.R" in your working directory
      and supply nothing to `source`.

- r_fn:

  A `callr` function such as
  [`callr::r`](https://callr.r-lib.org/reference/r.html) or
  [`callr::r_bg`](https://callr.r-lib.org/reference/r_bg.html). Example:
  `r_make(r_fn = callr::r)`.

- r_args:

  List of arguments to `r_fn`, not including `func` or `args`. Example:
  `r_make(r_fn = callr::r_bg, r_args = list(stdout = "stdout.log"))`.

- target:

  Name of the target.

- character_only:

  Logical, whether `name` should be treated as a character or a symbol
  (just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html)).

- ...:

  Arguments to the inner function. For example, if you want to call
  `r_vis_drake_graph()`, the inner function is
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
  and `selfcontained` is an example argument you could supply to the
  ellipsis.

## Details

`drake` searches your environment to detect dependencies, so functions
like [`make()`](https://docs.ropensci.org/drake/reference/make.md),
[`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md),
etc. are designed to run in fresh clean R sessions. Wrappers `r_make()`,
`r_outdated()`, etc. run reproducibly even if your current R session is
old and stale.

`r_outdated()` runs the four steps below. `r_make()` etc. are similar.

1.  Launch a new
    [`callr::r()`](https://callr.r-lib.org/reference/r.html) session.

2.  In that fresh session, run the R script from the `source` argument.
    This script loads packages, functions, global options, etc. and
    calls
    [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
    at the very end.
    [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
    is the preprocessing step of
    [`make()`](https://docs.ropensci.org/drake/reference/make.md), and
    it accepts all the same arguments as
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) (e.g.
    `plan` and `targets`).

3.  In that same session, run
    [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
    with the `config` argument from step 2.

4.  Return the result back to main process (e.g. your interactive R
    session).

## Recovery

`make(recover = TRUE, recoverable = TRUE)` powers automated data
recovery. The default of `recover` is `FALSE` because targets recovered
from the distant past may have been generated with earlier versions of R
and earlier package environments that no longer exist.

How it works: if `recover` is `TRUE`, `drake` tries to salvage old
target values from the cache instead of running commands from the plan.
A target is recoverable if

1.  There is an old value somewhere in the cache that shares the
    command, dependencies, etc. of the target about to be built.

2.  The old value was generated with `make(recoverable = TRUE)`.

If both conditions are met, `drake` will

1.  Assign the most recently-generated admissible data to the target,
    and

2.  skip the target's command.

## See also

[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("quarantine side effects", {
if (requireNamespace("knitr", quietly = TRUE)) {
writeLines(
  c(
    "library(drake)",
    "load_mtcars_example()",
    "drake_config(my_plan, targets = c(\"small\", \"large\"))"
  ),
  "_drake.R" # default value of the `source` argument
)
cat(readLines("_drake.R"), sep = "\n")
r_outdated()
r_make()
r_outdated()
}
})
} # }
```
