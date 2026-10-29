# Read and return a drake target/import from the cache. **\[stable\]**

`readd()` returns an object from the cache, and `loadd()` loads one or
more objects from the cache into your environment or session. These
objects are usually targets built by
[`make()`](https://docs.ropensci.org/drake/reference/make.md). If
`target` is dynamic, `readd()` and `loadd()` retrieve a list of
sub-target values. You can restrict which sub-targets to include using
the `subtargets` argument.

## Usage

``` r
readd(
  target,
  character_only = FALSE,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  namespace = NULL,
  verbose = 1L,
  show_source = FALSE,
  subtargets = NULL,
  subtarget_list = FALSE
)

loadd(
  ...,
  list = character(0),
  imported_only = NULL,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  namespace = NULL,
  envir = parent.frame(),
  jobs = 1,
  verbose = 1L,
  deps = FALSE,
  lazy = "eager",
  graph = NULL,
  replace = TRUE,
  show_source = FALSE,
  tidyselect = !deps,
  config = NULL,
  subtargets = NULL,
  subtarget_list = FALSE
)
```

## Arguments

- target:

  If `character_only` is `TRUE`, then `target` is a character string
  naming the object to read. Otherwise, `target` is an unquoted symbol
  with the name of the object.

- character_only:

  Logical, whether `name` should be treated as a character or a symbol
  (just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html)).

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- namespace:

  Optional character string, name of the `storr` namespace to read from.

- verbose:

  Deprecated on 2019-09-11.

- show_source:

  Logical, option to show the command that produced the target or
  indicate that the object was imported (using
  [`show_source()`](https://docs.ropensci.org/drake/reference/show_source.md)).

- subtargets:

  A numeric vector of indices. If `target` is dynamic, `loadd()` and
  `readd()` retrieve a list of sub-targets. You can restrict which
  sub-targets to retrieve with the `subtargets` argument. For example,
  `readd(x, subtargets = seq_len(3))` only retrieves the first 3
  sub-targets of dynamic target `x`.

- subtarget_list:

  Logical, for dynamic targets only. If `TRUE`, the dynamic target is
  loaded as a named list of sub-target values. If `FALSE`, `drake`
  attempts to concatenate the sub-targets with
  [`vctrs::vec_c()`](https://vctrs.r-lib.org/reference/vec_c.html) (and
  returns an unnamed list if such concatenation is not possible).

- ...:

  Targets to load from the cache: as names (symbols) or character
  strings. If the `tidyselect` package is installed, you can also supply
  `dplyr`-style `tidyselect` commands such as
  [`starts_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  [`ends_with()`](https://tidyselect.r-lib.org/reference/starts_with.html),
  and [`one_of()`](https://tidyselect.r-lib.org/reference/one_of.html).

- list:

  Character vector naming targets to be loaded from the cache. Similar
  to the `list` argument of
  [`remove()`](https://rdrr.io/r/base/rm.html).

- imported_only:

  Logical, deprecated.

- envir:

  Environment to load objects into. Defaults to the calling environment
  (current workspace).

- jobs:

  Number of parallel jobs for loading objects. On non-Windows systems,
  the loading process for multiple objects can be lightly parallelized
  via
  [`parallel::mclapply()`](https://rdrr.io/r/parallel/mclapply.html).
  just set jobs to be an integer greater than 1. On Windows, `jobs` is
  automatically demoted to 1.

- deps:

  Logical, whether to load any cached dependencies of the targets
  instead of the targets themselves.

  Important note: `deps = TRUE` disables `tidyselect` functionality. For
  example, `loadd(starts_with("model_"), config = config, deps = TRUE)`
  does not work. For the selection mechanism to work, the `model_*`
  targets to need to already be in the cache, which is not always the
  case when you are debugging your projects. To help `drake` understand
  what you mean, you must name the targets *explicitly* when `deps` is
  `TRUE`, e.g. `loadd(model_A, model_B, config = config, deps = TRUE)`.

- lazy:

  Either a string or a logical. Choices:

  - `"eager"`: no lazy loading. The target is loaded right away with
    [`assign()`](https://rdrr.io/r/base/assign.html).

  - `"promise"`: lazy loading with
    [`delayedAssign()`](https://rdrr.io/r/base/delayedAssign.html)

  - `"bind"`: lazy loading with active bindings:
    [`bindr::populate_env()`](https://krlmlr.github.io/bindr/reference/create_env.html).

  - `TRUE`: same as `"promise"`.

  - `FALSE`: same as `"eager"`.

- graph:

  Deprecated.

- replace:

  Logical. If `FALSE`, items already in your environment will not be
  replaced.

- tidyselect:

  Logical, whether to enable `tidyselect` expressions in `...` like
  `starts_with("prefix")` and `ends_with("suffix")`.

- config:

  Optional
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object. You should supply one if `deps` is `TRUE`.

## Value

The cached value of the `target`.

## Details

There are three uses for the `loadd()` and `readd()` functions:

1.  Exploring the results outside the
    `drake`/[`make()`](https://docs.ropensci.org/drake/reference/make.md)
    pipeline. When you call
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) to run
    your project, `drake` puts the targets in a cache, usually a folder
    called `.drake`. You may want to inspect the targets afterwards,
    possibly in an interactive R session. However, the files in the
    `.drake` folder are organized in a special format created by the
    `storr` package, which is not exactly human-readable. To retrieve a
    target for manual viewing, use `readd()`. To load one or more
    targets into your session, use `loadd()`.

2.  In `knitr` / R Markdown reports. You can borrow `drake` targets in
    your active code chunks if you have the right calls to `loadd()` and
    `readd()`. These reports can either run outside the `drake`
    pipeline, or better yet, as part of the pipeline itself. If you call
    `knitr_in("your_report.Rmd")` inside a
    [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
    command, then
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) will
    scan `"your_report.Rmd"` for calls to `loadd()` and `readd()` in
    active code chunks, and then treat those loaded targets as
    dependencies. That way,
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) will
    automatically (re)run the report if those dependencies change.

3.  If you are using `make(memory_strategy = "none")` or
    `make(memory_strategy = "unload")`, `loadd()` and `readd()` can
    manually load dependencies into memory for the target that is being
    built. If you do this, you must carefully inspect
    [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
    and
    [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
    before running
    [`make()`](https://docs.ropensci.org/drake/reference/make.md) to be
    sure the dependency relationships among targets are correct. If you
    do not wish to incur extra dependencies with `loadd()` or `readd()`,
    you will need to use
    [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md),
    e.g. `drake_plan(x = 1, y = ignore(readd(x)))` or
    `drake_plan(x = 1, y = readd(ignore("x"), character_only = TRUE))`.
    Compare those plans to `drake_plan(x = 1, y = readd(x))` and
    `drake_plan(x = 1, y = readd("x", character_only = TRUE))` using
    [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
    and
    [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md).

## See also

[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

[`cached()`](https://docs.ropensci.org/drake/reference/cached.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the project, build the targets.
readd(reg1) # Return imported object 'reg1' from the cache.
readd(small) # Return targets 'small' from the cache.
readd("large", character_only = TRUE) # Return 'large' from the cache.
# For external files, only the fingerprint/hash is stored.
readd(file_store("report.md"), character_only = TRUE)
}
})
} # }
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the projects, build the targets.
config <- drake_config(my_plan)
loadd(small) # Load target 'small' into your workspace.
small
# For many targets, you can parallelize loadd()
# using the 'jobs' argument.
loadd(list = c("small", "large"), jobs = 2)
ls()
# Load the dependencies of the target, coef_regression2_small
loadd(coef_regression2_small, deps = TRUE, config = config)
ls()
# Load all the targets listed in the workflow plan
# of the previous `make()`.
# If you do not supply any target names, `loadd()` loads all the targets.
# Be sure your computer has enough memory.
loadd()
ls()
}
})
} # }
```
