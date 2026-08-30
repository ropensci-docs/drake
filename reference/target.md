# Customize a target in [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md). **\[stable\]**

The `target()` function is a way to configure individual targets in a
`drake` plan. Its most common use is to invoke static branching and
dynamic branching, and it can also set the values of custom columns such
as `format`, `elapsed`, `retries`, and `max_expand`. Details are at
`https://books.ropensci.org/drake/plans.html#special-columns`. Note:
`drake_plan(my_target = my_command())` is equivalent to
`drake_plan(my_target = target(my_command())`.

## Usage

``` r
target(command = NULL, transform = NULL, dynamic = NULL, ...)
```

## Arguments

- command:

  The command to build the target.

- transform:

  A call to
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  to apply a *static* transformation. Details:
  `https://books.ropensci.org/drake/static.html`

- dynamic:

  A call to
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md)
  to apply a *dynamic* transformation. Details:
  `https://books.ropensci.org/drake/dynamic.html`

- ...:

  Optional columns of the plan for a given target. See the Columns
  section of this help file for a selection of special columns that
  `drake` understands.

## Value

A one-row workflow plan data frame with the named arguments as columns.

## Details

`target()` must be called inside
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
It is invalid otherwise.

## Columns

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
creates a special data frame. At minimum, that data frame must have
columns `target` and `command` with the target names and the R code
chunks to build them, respectively.

You can add custom columns yourself, either with `target()` (e.g.
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
  recommended that you define this one with `target()`. Details:
  `https://books.ropensci.org/drake/triggers.html`.

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

## Keywords

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
understands special keyword functions for your commands. With the
exception of `target()`, each one is a proper function with its own help
file.

- `target()`: give the target more than just a command. Using
  `target()`, you can apply a transformation (examples:
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

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
# Use target() to create your own custom columns in a drake plan.
# See ?triggers for more on triggers.
drake_plan(
  website_data = target(
    download_data("www.your_url.com"),
    trigger = "always",
    custom_column = 5
  ),
  analysis = analyze(website_data)
)
#> # A tibble: 2 × 4
#>   target       command                           trigger       custom_column
#>   <chr>        <expr_lst>                        <expr_lst>            <dbl>
#> 1 website_data download_data("www.your_url.com") "always"                  5
#> 2 analysis     analyze(website_data)             NA_character_            NA
models <- c("glm", "hierarchical")
plan <- drake_plan(
  data = target(
    get_data(x),
    transform = map(x = c("simulated", "survey"))
  ),
  analysis = target(
    analyze_data(data, model),
    transform = cross(data, model = !!models, .id = c(x, model))
  ),
  summary = target(
    summarize_analysis(analysis),
    transform = map(analysis, .id = c(x, model))
  ),
  results = target(
    bind_rows(summary),
    transform = combine(summary, .by = data)
  )
)
plan
#> # A tibble: 12 × 2
#>    target                          command                                      
#>    <chr>                           <expr_lst>                                   
#>  1 analysis_simulated_glm          analyze_data(data_simulated, "glm")         …
#>  2 analysis_simulated_hierarchical analyze_data(data_simulated, "hierarchical")…
#>  3 analysis_survey_glm             analyze_data(data_survey, "glm")            …
#>  4 analysis_survey_hierarchical    analyze_data(data_survey, "hierarchical")   …
#>  5 data_simulated                  get_data("simulated")                       …
#>  6 data_survey                     get_data("survey")                          …
#>  7 results_data_simulated          bind_rows(summary_simulated_glm, summary_sim…
#>  8 results_data_survey             bind_rows(summary_survey_glm, summary_survey…
#>  9 summary_simulated_glm           summarize_analysis(analysis_simulated_glm)  …
#> 10 summary_simulated_hierarchical  summarize_analysis(analysis_simulated_hierar…
#> 11 summary_survey_glm              summarize_analysis(analysis_survey_glm)     …
#> 12 summary_survey_hierarchical     summarize_analysis(analysis_survey_hierarchi…
if (requireNamespace("styler", quietly = TRUE)) {
  print(drake_plan_source(plan))
}
#> drake_plan(
#>   analysis_simulated_glm = analyze_data(data_simulated, "glm"),
#>   analysis_simulated_hierarchical = analyze_data(data_simulated, "hierarchical"),
#>   analysis_survey_glm = analyze_data(data_survey, "glm"),
#>   analysis_survey_hierarchical = analyze_data(data_survey, "hierarchical"),
#>   data_simulated = get_data("simulated"),
#>   data_survey = get_data("survey"),
#>   results_data_simulated = bind_rows(summary_simulated_glm, summary_simulated_hierarchical),
#>   results_data_survey = bind_rows(summary_survey_glm, summary_survey_hierarchical),
#>   summary_simulated_glm = summarize_analysis(analysis_simulated_glm),
#>   summary_simulated_hierarchical = summarize_analysis(analysis_simulated_hierarchical),
#>   summary_survey_glm = summarize_analysis(analysis_survey_glm),
#>   summary_survey_hierarchical = summarize_analysis(analysis_survey_hierarchical)
#> )
```
