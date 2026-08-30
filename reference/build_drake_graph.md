# Function `build_drake_graph` **\[deprecated\]**

Use
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
instead.

## Usage

``` r
build_drake_graph(
  plan,
  targets = plan$target,
  envir = parent.frame(),
  verbose = 1L,
  jobs = 1,
  console_log_file = NULL,
  trigger = drake::trigger(),
  cache = NULL
)
```

## Arguments

- plan:

  Workflow plan data frame. A workflow plan data frame is a data frame
  with a `target` column and a `command` column. (See the details in the
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  help file for descriptions of the optional columns.) Targets are the
  objects that drake generates, and commands are the pieces of R code
  that produce them. You can create and track custom files along the way
  (see
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md),
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
  and
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)).
  Use the function
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  to generate workflow plan data frames.

- targets:

  Character vector, names of targets to build. Dependencies are built
  too. You may supply static and/or whole dynamic targets, but no
  sub-targets.

- envir:

  Environment to use. Defaults to the current workspace, so you should
  not need to worry about this most of the time. A deep copy of `envir`
  is made, so you don't need to worry about your workspace being
  modified by `make`. The deep copy inherits from the global
  environment. Wherever necessary, objects and functions are imported
  from `envir` and the global environment and then reproducibly tracked
  as dependencies.

- verbose:

  Integer, control printing to the console/terminal.

  - `0`: print nothing.

  - `1`: print target-by-target messages as
    [`make()`](https://docs.ropensci.org/drake/reference/make.md)
    progresses.

  - `2`: show a progress bar to track how many targets are done so far.

- jobs:

  Maximum number of parallel workers for processing the targets. You can
  experiment with
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)
  to help decide on an appropriate number of jobs. For details, visit
  `https://books.ropensci.org/drake/time.html`.

- console_log_file:

  Deprecated in favor of `log_make`.

- trigger:

  Name of the trigger to apply to all targets. Ignored if `plan` has a
  `trigger` column. See
  [`trigger()`](https://docs.ropensci.org/drake/reference/trigger.md)
  for details.

- cache:

  drake cache as created by
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  See also
  [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md).

## Value

An `igraph` object.

## Details

Deprecated on 2018-11-02.
