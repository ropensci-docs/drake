# Create a drake plan for the `plan` argument of [`make()`](https://docs.ropensci.org/drake/reference/make.md). **\[stable\]**

A `drake` plan is a data frame with columns `"target"` and `"command"`.
Each target is an R object produced in your workflow, and each command
is the R code to produce it.

## Usage

``` r
drake_plan(
  ...,
  list = NULL,
  file_targets = NULL,
  strings_in_dots = NULL,
  tidy_evaluation = NULL,
  transform = TRUE,
  trace = FALSE,
  envir = parent.frame(),
  tidy_eval = TRUE,
  max_expand = NULL
)
```

## Arguments

- ...:

  A collection of symbols/targets with commands assigned to them. See
  the examples for details.

- list:

  Deprecated

- file_targets:

  Deprecated.

- strings_in_dots:

  Deprecated.

- tidy_evaluation:

  Deprecated. Use `tidy_eval` instead.

- transform:

  Logical, whether to transform the plan into a larger plan with more
  targets. Requires the `transform` field in
  [`target()`](https://docs.ropensci.org/drake/reference/target.md). See
  the examples for details.

- trace:

  Logical, whether to add columns to show what happens during target
  transformations.

- envir:

  Environment for tidy evaluation.

- tidy_eval:

  Logical, whether to use tidy evaluation (e.g. unquoting/`!!`) when
  resolving commands. Tidy evaluation in transformations is always
  turned on regardless of the value you supply to this argument.

- max_expand:

  Positive integer, optional. `max_expand` is the maximum number of
  targets to generate in each
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  transform. Useful if you have a massive plan and you want to test and
  visualize a strategic subset of targets before scaling up. Note: the
  `max_expand` argument of `drake_plan()` and
  [`transform_plan()`](https://docs.ropensci.org/drake/reference/transform_plan.md)
  is for static branching only. The dynamic branching `max_expand` is an
  argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

## Value

A data frame of targets, commands, and optional custom columns.

## Details

Besides `"target"` and `"command"`, `drake_plan()` understands a special
set of optional columns. For details, visit
`https://books.ropensci.org/drake/plans.html#special-custom-columns-in-your-plan`
\# nolint

## Columns

`drake_plan()` creates a special data frame. At minimum, that data frame
must have columns `target` and `command` with the target names and the R
code chunks to build them, respectively.

You can add custom columns yourself, either with
[`target()`](https://docs.ropensci.org/drake/reference/target.md) (e.g.
`drake_plan(y = target(f(x), transform = map(c(1, 2)), format = "fst"))`)
or by appending columns post-hoc (e.g. `plan$col <- vals`).

Some of these custom columns are special. They are optional, but `drake`
looks for them at various points in the workflow.

- `transform`: a call to
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  to create and manipulate large collections of targets. Details:
  (`https://books.ropensci.org/drake/plans.html#large-plans`). \# nolint

- `format`: set a storage format to save big targets more efficiently.
  See the "Formats" section of this help file for more details.

- `trigger`: rule to decide whether a target needs to run. It is
  recommended that you define this one with
  [`target()`](https://docs.ropensci.org/drake/reference/target.md).
  Details: `https://books.ropensci.org/drake/triggers.html`.

- `hpc`: logical values (`TRUE`/`FALSE`/`NA`) whether to send each
  target to parallel workers. Visit
  `https://books.ropensci.org/drake/hpc.html#selectivity` to learn more.

- `resources`: target-specific lists of resources for a computing
  cluster. See
  `https://books.ropensci.org/drake/hpc.html#advanced-options` for
  details.

- `caching`: overrides the `caching` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) for each
  target individually. Possible values:

  - "main": tell the main process to store the target in the cache.

  - "worker": tell the HPC worker to store the target in the cache.

  - NA: default to the `caching` argument of
    [`make()`](https://docs.ropensci.org/drake/reference/make.md).

- `elapsed` and `cpu`: number of seconds to wait for the target to build
  before timing out (`elapsed` for elapsed time and `cpu` for CPU time).

- `retries`: number of times to retry building a target in the event of
  an error.

- `seed`: an optional pseudo-random number generator (RNG) seed for each
  target. `drake` usually comes up with its own unique reproducible
  target-specific seeds using the global seed (the `seed` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md))
  and the target names, but you can overwrite these automatic seeds.
  `NA` entries default back to `drake`'s automatic seeds.

- `max_expand`: for dynamic branching only. Same as the `max_expand`
  argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), but on
  a target-by-target basis. Limits the number of sub-targets created for
  a given target.

## Formats

Specialized target formats increase efficiency and flexibility. Some
allow you to save specialized objects like `keras` models, while others
increase the speed while conserving storage and memory. You can declare
target-specific formats in the plan (e.g.
`drake_plan(x = target(big_data_frame, format = "fst"))`) or supply a
global default `format` for all targets in
[`make()`](https://docs.ropensci.org/drake/reference/make.md). Either
way, most formats have specialized installation requirements (e.g. R
packages) that are not installed with `drake` by default. You will need
to install them separately yourself. Available formats:

- `"file"`: Dynamic files. To use this format, simply create local files
  and directories yourself and then return a character vector of paths
  as the target's value. Then, `drake` will watch for changes to those
  files in subsequent calls to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). This is
  a more flexible alternative to
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  and
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
  and it is compatible with dynamic branching. See
  `https://github.com/ropensci/drake/pull/1178` for an example.

- `"fst"`: save big data frames fast. Requires the `fst` package. Note:
  this format strips non-data-frame attributes such as the

- `"fst_tbl"`: Like `"fst"`, but for `tibble` objects. Requires the
  `fst` and `tibble` packages. Strips away non-data-frame non-tibble
  attributes.

- `"fst_dt"`: Like `"fst"` format, but for `data.table` objects.
  Requires the `fst` and `data.table` packages. Strips away
  non-data-frame non-data-table attributes.

- `"diskframe"`: Stores `disk.frame` objects, which could potentially be
  larger than memory. Requires the `fst` and `disk.frame` packages.
  Coerces objects to `disk.frame`s. Note: `disk.frame` objects get moved
  to the `drake` cache (a subfolder of `.drake/` for most workflows). To
  ensure this data transfer is fast, it is best to save your
  `disk.frame` objects to the same physical storage drive as the `drake`
  cache, `as.disk.frame(your_dataset, outdir = drake_tempfile())`.

- `"keras"`: save Keras models as HDF5 files. Requires the `keras`
  package.

- `"qs"`: save any R object that can be properly serialized with the
  `qs` package. Requires the `qs` package. Uses `qsave()` and `qread()`.
  Uses the default settings in `qs` version 0.20.2.

- `"rds"`: save any R object that can be properly serialized. Requires R
  version \>= 3.5.0 due to ALTREP. Note: the `"rds"` format uses gzip
  compression, which is slow. `"qs"` is a superior format.

## Keywords

`drake_plan()` understands special keyword functions for your commands.
With the exception of
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

- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md):
  get the environment where drake builds targets. Intended for advanced
  custom memory management.

## Transformations

`drake` has special syntax for generating large plans. Your code will
look something like
`drake_plan(y = target(f(x), transform = map(x = c(1, 2, 3)))` You can
read about this interface at
`https://books.ropensci.org/drake/plans.html#large-plans`. \# nolint

## Static branching

In static branching, you define batches of targets based on information
you know in advance. Overall usage looks like
`drake_plan(<x> = target(<...>, transform = <call>)`, where

- `<x>` is the name of the target or group of targets.

- `<...>` is optional arguments to
  [`target()`](https://docs.ropensci.org/drake/reference/target.md).

- `<call>` is a call to one of the transformation functions.

Transformation function usage:

- `map(..., .data, .names, .id, .tag_in, .tag_out)`

- `split(..., slices, margin = 1L, drop = FALSE, .names, .tag_in, .tag_out)`
  \# nolint

- `cross(..., .data, .names, .id, .tag_in, .tag_out)`

- `combine(..., .by, .names, .id, .tag_in, .tag_out)`

## Dynamic branching

- `map(..., .trace)`

- `cross(..., .trace)`

- `group(..., .by, .trace)`

[`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
and
[`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
create dynamic sub-targets from the variables supplied to the dots. As
with static branching, the variables supplied to
[`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
must all have equal length. `group(f(data), .by = x)` makes new dynamic
sub-targets from `data`. Here, `data` can be either static or dynamic.
If `data` is dynamic,
[`group()`](https://docs.ropensci.org/drake/reference/transformations.md)
aggregates existing sub-targets. If `data` is static,
[`group()`](https://docs.ropensci.org/drake/reference/transformations.md)
splits `data` into multiple subsets based on the groupings from `.by`.

Differences from static branching:

- `...` must contain *unnamed* symbols with no values supplied, and they
  must be the names of targets.

- Arguments `.id`, `.tag_in`, and `.tag_out` no longer apply.

## See also

make, drake_config, transform_plan, map, split, cross, combine

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
# For more examples, visit
# https://books.ropensci.org/drake/plans.html.

# Create drake plans:
mtcars_plan <- drake_plan(
  write.csv(mtcars[, c("mpg", "cyl")], file_out("mtcars.csv")),
  value = read.csv(file_in("mtcars.csv"))
)
if (requireNamespace("visNetwork", quietly = TRUE)) {
  plot(mtcars_plan) # fast simplified call to vis_drake_graph()
}
mtcars_plan
make(mtcars_plan) # Makes `mtcars.csv` and then `value`
head(readd(value))
# You can use knitr inputs too. See the top command below.

load_mtcars_example()
head(my_plan)
if (requireNamespace("knitr", quietly = TRUE)) {
  plot(my_plan)
}
# The `knitr_in("report.Rmd")` tells `drake` to dive into the active
# code chunks to find dependencies.
# There, `drake` sees that `small`, `large`, and `coef_regression2_small`
# are loaded in with calls to `loadd()` and `readd()`.
deps_code("report.Rmd")

# Formats are great for big data: https://github.com/ropensci/drake/pull/977
# Below, each target is 1.6 GB in memory.
# Run make() on this plan to see how much faster fst is!
n <- 1e8
plan <- drake_plan(
  data_fst = target(
    data.frame(x = runif(n), y = runif(n)),
    format = "fst"
  ),
  data_old = data.frame(x = runif(n), y = runif(n))
)

# Use transformations to generate large plans.
# Read more at
# `https://books.ropensci.org/drake/plans.html#create-large-plans-the-easy-way`. # nolint
drake_plan(
  data = target(
    simulate(nrows),
    transform = map(nrows = c(48, 64)),
    custom_column = 123
  ),
  reg = target(
    reg_fun(data),
   transform = cross(reg_fun = c(reg1, reg2), data)
  ),
  summ = target(
    sum_fun(data, reg),
   transform = cross(sum_fun = c(coef, residuals), reg)
  ),
  winners = target(
    min(summ),
    transform = combine(summ, .by = c(data, sum_fun))
  )
)

# Split data among multiple targets.
drake_plan(
  large_data = get_data(),
  slice_analysis = target(
    analyze(large_data),
    transform = split(large_data, slices = 4)
  ),
  results = target(
    rbind(slice_analysis),
    transform = combine(slice_analysis)
  )
)

# Set trace = TRUE to show what happened during the transformation process.
drake_plan(
  data = target(
    simulate(nrows),
    transform = map(nrows = c(48, 64)),
    custom_column = 123
  ),
  reg = target(
    reg_fun(data),
   transform = cross(reg_fun = c(reg1, reg2), data)
  ),
  summ = target(
    sum_fun(data, reg),
   transform = cross(sum_fun = c(coef, residuals), reg)
  ),
  winners = target(
    min(summ),
    transform = combine(summ, .by = c(data, sum_fun))
  ),
  trace = TRUE
)

# You can create your own custom columns too.
# See ?triggers for more on triggers.
drake_plan(
  website_data = target(
    command = download_data("www.your_url.com"),
    trigger = "always",
    custom_column = 5
  ),
  analysis = analyze(website_data)
)

# Tidy evaluation can help generate super large plans.
sms <- rlang::syms(letters) # To sub in character args, skip this.
drake_plan(x = target(f(char), transform = map(char = !!sms)))

# Dynamic branching
# Get the mean mpg for each cyl in the mtcars dataset.
plan <- drake_plan(
  raw = mtcars,
  group_index = raw$cyl,
  munged = target(raw[, c("mpg", "cyl")], dynamic = map(raw)),
  mean_mpg_by_cyl = target(
    data.frame(mpg = mean(munged$mpg), cyl = munged$cyl[1]),
    dynamic = group(munged, .by = group_index)
  )
)
make(plan)
readd(mean_mpg_by_cyl)
})
} # }
```
