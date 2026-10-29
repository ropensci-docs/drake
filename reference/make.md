# Run your project (build the outdated targets). **\[stable\]**

This is the central, most important function of the drake package. It
runs all the steps of your workflow in the correct order, skipping any
work that is already up to date. Because of how `make()` tracks global
functions and objects as dependencies of targets, please restart your R
session so the pipeline runs in a clean reproducible environment.

## Usage

``` r
make(
  plan,
  targets = NULL,
  envir = parent.frame(),
  verbose = 1L,
  hook = NULL,
  cache = drake::drake_cache(),
  fetch_cache = NULL,
  parallelism = "loop",
  jobs = 1L,
  jobs_preprocess = 1L,
  packages = rev(.packages()),
  lib_loc = NULL,
  prework = character(0),
  prepend = NULL,
  command = NULL,
  args = NULL,
  recipe_command = NULL,
  log_progress = TRUE,
  skip_targets = FALSE,
  timeout = NULL,
  cpu = Inf,
  elapsed = Inf,
  retries = 0,
  force = FALSE,
  graph = NULL,
  trigger = drake::trigger(),
  skip_imports = FALSE,
  skip_safety_checks = FALSE,
  config = NULL,
  lazy_load = "eager",
  session_info = NULL,
  cache_log_file = NULL,
  seed = NULL,
  caching = "main",
  keep_going = FALSE,
  session = NULL,
  pruning_strategy = NULL,
  makefile_path = NULL,
  console_log_file = NULL,
  ensure_workers = NULL,
  garbage_collection = FALSE,
  template = list(),
  sleep = function(i) 0.01,
  hasty_build = NULL,
  memory_strategy = "speed",
  layout = NULL,
  spec = NULL,
  lock_envir = NULL,
  history = TRUE,
  recover = FALSE,
  recoverable = TRUE,
  curl_handles = list(),
  max_expand = NULL,
  log_build_times = TRUE,
  format = NULL,
  lock_cache = TRUE,
  log_make = NULL,
  log_worker = FALSE
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

  - `1`: print target-by-target messages as `make()` progresses.

  - `2`: show a progress bar to track how many targets are done so far.

- hook:

  Deprecated.

- cache:

  drake cache as created by
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  See also
  [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md).

- fetch_cache:

  Deprecated.

- parallelism:

  Character scalar, type of parallelism to use. For detailed
  explanations, see `https://books.ropensci.org/drake/hpc.html`.

  You could also supply your own scheduler function if you want to
  experiment or aggressively optimize. The function should take a single
  `config` argument (produced by
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)).
  Existing examples from `drake`'s internals are the `backend_*()`
  functions:

  - `backend_loop()`

  - `backend_clustermq()`

  - `backend_future()` However, this functionality is really a back door
    and should not be used for production purposes unless you really
    know what you are doing and you are willing to suffer setbacks
    whenever `drake`'s unexported core functions are updated.

- jobs:

  Maximum number of parallel workers for processing the targets. You can
  experiment with
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)
  to help decide on an appropriate number of jobs. For details, visit
  `https://books.ropensci.org/drake/time.html`.

- jobs_preprocess:

  Number of parallel jobs for processing the imports and doing other
  preprocessing tasks.

- packages:

  Character vector packages to load, in the order they should be loaded.
  Defaults to `rev(.packages())`, so you should not usually need to set
  this manually. Just call
  [`library()`](https://rdrr.io/r/base/library.html) to load your
  packages before `make()`. However, sometimes packages need to be
  strictly forced to load in a certain order, especially if
  `parallelism` is `"Makefile"`. To do this, do not use
  [`library()`](https://rdrr.io/r/base/library.html) or
  [`require()`](https://rdrr.io/r/base/library.html) or
  [`loadNamespace()`](https://rdrr.io/r/base/ns-load.html) or
  [`attachNamespace()`](https://rdrr.io/r/base/ns-load.html) to load any
  libraries beforehand. Just list your packages in the `packages`
  argument in the order you want them to be loaded.

- lib_loc:

  Character vector, optional. Same as in
  [`library()`](https://rdrr.io/r/base/library.html) or
  [`require()`](https://rdrr.io/r/base/library.html). Applies to the
  `packages` argument (see above).

- prework:

  Expression (language object), list of expressions, or character
  vector. Code to run right before targets build. Called only once if
  `parallelism` is `"loop"` and once per target otherwise. This code can
  be used to set global options, etc.

- prepend:

  Deprecated.

- command:

  Deprecated.

- args:

  Deprecated.

- recipe_command:

  Deprecated.

- log_progress:

  Logical, whether to log the progress of individual targets as they are
  being built. Progress logging creates extra files in the cache
  (usually the `.drake/` folder) and slows down `make()` a little. If
  you need to reduce or limit the number of files in the cache, call
  `make(log_progress = FALSE, recover = FALSE)`.

- skip_targets:

  Logical, whether to skip building the targets in `plan` and just
  import objects and files.

- timeout:

  `deprecated`. Use `elapsed` and `cpu` instead.

- cpu:

  Same as the `cpu` argument of
  [`setTimeLimit()`](https://rdrr.io/r/base/setTimeLimit.html). Seconds
  of cpu time before a target times out. Assign target-level cpu timeout
  times with an optional `cpu` column in `plan`.

- elapsed:

  Same as the `elapsed` argument of
  [`setTimeLimit()`](https://rdrr.io/r/base/setTimeLimit.html). Seconds
  of elapsed time before a target times out. Assign target-level elapsed
  timeout times with an optional `elapsed` column in `plan`.

- retries:

  Number of retries to execute if the target fails. Assign target-level
  retries with an optional `retries` column in `plan`.

- force:

  Logical. If `FALSE` (default) then `drake` imposes checks if the cache
  was created with an old and incompatible version of drake. If there is
  an incompatibility, `make()` stops to give you an opportunity to
  downgrade `drake` to a compatible version rather than rerun all your
  targets from scratch.

- graph:

  Deprecated.

- trigger:

  Name of the trigger to apply to all targets. Ignored if `plan` has a
  `trigger` column. See
  [`trigger()`](https://docs.ropensci.org/drake/reference/trigger.md)
  for details.

- skip_imports:

  Logical, whether to totally neglect to process the imports and jump
  straight to the targets. This can be useful if your imports are
  massive and you just want to test your project, but it is bad practice
  for reproducible data analysis. This argument is overridden if you
  supply your own `graph` argument.

- skip_safety_checks:

  Logical, whether to skip the safety checks on your workflow. Use at
  your own peril.

- config:

  Deprecated.

- lazy_load:

  An old feature, currently being questioned. For the current
  recommendations on memory management, see
  `https://books.ropensci.org/drake/memory.html#memory-strategies`. The
  `lazy_load` argument is either a character vector or a logical. For
  dynamic targets, the behavior is always `"eager"` (see below). So the
  `lazy_load` argument is for static targets only. Choices for
  `lazy_load`:

  - `"eager"`: no lazy loading. The target is loaded right away with
    [`assign()`](https://rdrr.io/r/base/assign.html).

  - `"promise"`: lazy loading with
    [`delayedAssign()`](https://rdrr.io/r/base/delayedAssign.html)

  - `"bind"`: lazy loading with active bindings:
    [`bindr::populate_env()`](https://krlmlr.github.io/bindr/reference/create_env.html).

  - `TRUE`: same as `"promise"`.

  - `FALSE`: same as `"eager"`.

  If `lazy_load` is `"eager"`, drake prunes the execution environment
  before each target/stage, removing all superfluous targets and then
  loading any dependencies it will need for building. In other words,
  drake prepares the environment in advance and tries to be memory
  efficient. If `lazy_load` is `"bind"` or `"promise"`, drake assigns
  promises to load any dependencies at the last minute. Lazy loading may
  be more memory efficient in some use cases, but it may duplicate the
  loading of dependencies, costing time.

- session_info:

  Logical, whether to save the
  [`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) to the
  cache. Defaults to `TRUE`. This behavior is recommended for serious
  `make()`s for the sake of reproducibility. This argument only exists
  to speed up tests. Apparently,
  [`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) is a
  bottleneck for small `make()`s.

- cache_log_file:

  Name of the CSV cache log file to write. If `TRUE`, the default file
  name is used (`drake_cache.CSV`). If `NULL`, no file is written. If
  activated, this option writes a flat text file to represent the state
  of the cache (fingerprints of all the targets and imports). If you put
  the log file under version control, your commit history will give you
  an easy representation of how your results change over time as the
  rest of your project changes. Hopefully, this is a step in the right
  direction for data reproducibility.

- seed:

  Integer, the root pseudo-random number generator seed to use for your
  project. In `make()`, `drake` generates a unique local seed for each
  target using the global seed and the target name. That way, different
  pseudo-random numbers are generated for different targets, and this
  pseudo-randomness is reproducible.

  To ensure reproducibility across different R sessions,
  [`set.seed()`](https://rdrr.io/r/base/Random.html) and `.Random.seed`
  are ignored and have no affect on `drake` workflows. Conversely,
  `make()` does not usually change `.Random.seed`, even when
  pseudo-random numbers are generated. The exception to this last point
  is `make(parallelism = "clustermq")` because the `clustermq` package
  needs to generate random numbers to set up ports and sockets for
  ZeroMQ.

  On the first call to `make()` or
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
  `drake` uses the random number generator seed from the `seed`
  argument. Here, if the `seed` is `NULL` (default), `drake` uses a
  `seed` of `0`. On subsequent `make()`s for existing projects, the
  project's cached seed will be used in order to ensure reproducibility.
  Thus, the `seed` argument must either be `NULL` or the same seed from
  the project's cache (usually the `.drake/` folder). To reset the
  random number generator seed for a project, use
  `clean(destroy = TRUE)`.

- caching:

  Character string, either `"main"` or `"worker"`.

  - `"main"`: Targets are built by remote workers and sent back to the
    main process. Then, the main process saves them to the cache
    (`config$cache`, usually a file system `storr`). Appropriate if
    remote workers do not have access to the file system of the calling
    R session. Targets are cached one at a time, which may be slow in
    some situations.

  - `"worker"`: Remote workers not only build the targets, but also save
    them to the cache. Here, caching happens in parallel. However,
    remote workers need to have access to the file system of the calling
    R session. Transferring target data across a network can be slow.

- keep_going:

  Logical, whether to still keep running `make()` if targets fail.

- session:

  Deprecated. Has no effect now.

- pruning_strategy:

  Deprecated. See `memory_strategy`.

- makefile_path:

  Deprecated.

- console_log_file:

  Deprecated in favor of `log_make`.

- ensure_workers:

  Deprecated.

- garbage_collection:

  Logical, whether to call [`gc()`](https://rdrr.io/r/base/gc.html) each
  time a target is built during `make()`.

- template:

  A named list of values to fill in the `{{ ... }}` placeholders in
  template files (e.g. from
  [`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md)).
  Same as the `template` argument of
  [`clustermq::Q()`](https://mschubert.github.io/clustermq/reference/Q.html)
  and
  [`clustermq::workers`](https://mschubert.github.io/clustermq/reference/workers.html).
  Enabled for `clustermq` only (`make(parallelism = "clustermq")`), not
  `future` or `batchtools` so far. For more information, see the
  `clustermq` package: `https://github.com/mschubert/clustermq`. Some
  template placeholders such as `{{ job_name }}` and `{{ n_jobs }}`
  cannot be set this way.

- sleep:

  Optional function on a single numeric argument `i`. Default:
  `function(i) 0.01`.

  To conserve memory, `drake` assigns a brand new closure to `sleep`, so
  your custom function should not depend on in-memory data except from
  loaded packages.

  For parallel processing, `drake` uses a central main process to check
  what the parallel workers are doing, and for the affected
  high-performance computing workflows, wait for data to arrive over a
  network. In between loop iterations, the main process sleeps to avoid
  throttling. The `sleep` argument to `make()` and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  allows you to customize how much time the main process spends
  sleeping.

  The `sleep` argument is a function that takes an argument `i` and
  returns a numeric scalar, the number of seconds to supply to
  [`Sys.sleep()`](https://rdrr.io/r/base/Sys.sleep.html) after iteration
  `i` of checking. (Here, `i` starts at 1.) If the checking loop does
  something other than sleeping on iteration `i`, then `i` is reset back
  to 1.

  To sleep for the same amount of time between checks, you might supply
  something like `function(i) 0.01`. But to avoid consuming too many
  resources during heavier and longer workflows, you might use an
  exponential back-off: say,
  `function(i) { 0.1 + 120 * pexp(i - 1, rate = 0.01) }`.

- hasty_build:

  Deprecated

- memory_strategy:

  Character scalar, name of the strategy `drake` uses to load/unload a
  target's dependencies in memory. You can give each target its own
  memory strategy, (e.g.
  `drake_plan(x = 1, y = target(f(x), memory_strategy = "lookahead"))`)
  to override the global memory strategy. Choices:

  - `"speed"`: Once a target is newly built or loaded in memory, just
    keep it there. This choice maximizes speed and hogs memory.

  - `"autoclean"`: Just before building each new target, unload
    everything from memory except the target's direct dependencies.
    After a target is built, discard it from memory. (Set
    `garbage_collection = TRUE` to make sure it is really gone.) This
    option conserves memory, but it sacrifices speed because each new
    target needs to reload any previously unloaded targets from storage.

  - `"preclean"`: Just before building each new target, unload
    everything from memory except the target's direct dependencies.
    After a target is built, keep it in memory until `drake` determines
    they can be unloaded. This option conserves memory, but it
    sacrifices speed because each new target needs to reload any
    previously unloaded targets from storage.

  - `"lookahead"`: Just before building each new target, search the
    dependency graph to find targets that will not be needed for the
    rest of the current `make()` session. After a target is built, keep
    it in memory until the next memory management stage. In this mode,
    targets are only in memory if they need to be loaded, and we avoid
    superfluous reads from the cache. However, searching the graph takes
    time, and it could even double the computational overhead for large
    projects.

  - `"unload"`: Just before building each new target, unload all targets
    from memory. After a target is built, **do not** keep it in memory.
    This mode aggressively optimizes for both memory and speed, but in
    commands and triggers, you have to manually load any dependencies
    you need using
    [`readd()`](https://docs.ropensci.org/drake/reference/readd.md).

  - `"none"`: Do not manage memory at all. Do not load or unload
    anything before building targets. After a target is built, **do
    not** keep it in memory. This mode aggressively optimizes for both
    memory and speed, but in commands and triggers, you have to manually
    load any dependencies you need using
    [`readd()`](https://docs.ropensci.org/drake/reference/readd.md).

  For even more direct control over which targets `drake` keeps in
  memory, see the help file examples of
  [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md).
  Also see the `garbage_collection` argument of `make()` and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

- layout:

  Deprecated.

- spec:

  Deprecated.

- lock_envir:

  Deprecated in `drake >= 7.13.10`. Environments are no longer locked.

- history:

  Logical, whether to record the build history of your targets. You can
  also supply a `txtq`, which is how `drake` records history. Must be
  `TRUE` for
  [`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md)
  to work later.

- recover:

  Logical, whether to activate automated data recovery. The default is
  `FALSE` because

  1.  Automated data recovery is still stable.

  2.  It has reproducibility issues. Targets recovered from the distant
      past may have been generated with earlier versions of R and
      earlier package environments that no longer exist.

  3.  It is not always possible, especially when dynamic files are
      combined with dynamic branching (e.g. `dynamic = map(stuff)` and
      `format = "file"` etc.) since behavior is harder to predict in
      advance.

  How it works: if `recover` is `TRUE`, `drake` tries to salvage old
  target values from the cache instead of running commands from the
  plan. A target is recoverable if

  1.  There is an old value somewhere in the cache that shares the
      command, dependencies, etc. of the target about to be built.

  2.  The old value was generated with `make(recoverable = TRUE)`.

  If both conditions are met, `drake` will

  1.  Assign the most recently-generated admissible data to the target,
      and

  2.  skip the target's command.

  Functions
  [`recoverable()`](https://docs.ropensci.org/drake/reference/recoverable.md)
  and
  [`r_recoverable()`](https://docs.ropensci.org/drake/reference/r_make.md)
  show the most upstream outdated targets that will be recovered in this
  way in the next `make()` or
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md).

- recoverable:

  Logical, whether to make target values recoverable with
  `make(recover = TRUE)`. This requires writing extra files to the
  cache, and it prevents old metadata from being removed with garbage
  collection (`clean(garbage_collection = TRUE)`,
  [`gc()`](https://rdrr.io/r/base/gc.html) in `storr`s). If you need to
  limit the cache size or the number of files in the cache, consider
  `make(recoverable = FALSE, progress = FALSE)`. Recovery is not always
  possible, especially when dynamic files are combined with dynamic
  branching (e.g. `dynamic = map(stuff)` and `format = "file"` etc.)
  since behavior is harder to predict in advance.

- curl_handles:

  A named list of curl handles. Each value is an object from
  [`curl::new_handle()`](https://jeroen.r-universe.dev/curl/reference/handle.html),
  and each name is a URL (and should start with "http", "https", or
  "ftp"). Example: list( `http://httpbin.org/basic-auth` =
  curl::new_handle( username = "user", password = "passwd" ) ) Then, if
  your plan has `file_in("http://httpbin.org/basic-auth/user/passwd")`
  `drake` will authenticate using the username and password of the
  handle for `http://httpbin.org/basic-auth/`.

  `drake` uses partial matching on text to find the right handle of the
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  URL, so the name of the handle could be the complete URL
  (`"http://httpbin.org/basic-auth/user/passwd"`) or a part of the URL
  (e.g. `"http://httpbin.org/"` or `"http://httpbin.org/basic-auth/"`).
  If you have multiple handles whose names match your URL, `drake` will
  choose the closest match.

- max_expand:

  Positive integer, optional. `max_expand` is the maximum number of
  targets to generate in each
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md)
  dynamic transform. Useful if you have a massive number of dynamic
  sub-targets and you want to work with only the first few sub-targets
  before scaling up. Note: the `max_expand` argument of `make()` and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  is for dynamic branching only. The static branching `max_expand` is an
  argument of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  and
  [`transform_plan()`](https://docs.ropensci.org/drake/reference/transform_plan.md).

- log_build_times:

  Logical, whether to record build_times for targets. Mac users may
  notice a 20% speedup in `make()` with `build_times = FALSE`.

- format:

  Character, an optional custom storage format for targets without an
  explicit `target(format = ...)` in the plan. Details about formats:
  `https://books.ropensci.org/drake/plans.html#special-data-formats-for-targets`
  \# nolint

- lock_cache:

  Logical, whether to lock the cache before running `make()` etc. It is
  usually recommended to keep cache locking on. However, if you
  interrupt `make()` before it can clean itself up, then the cache will
  stay locked, and you will need to manually unlock it with
  `drake::drake_cache("xyz")$unlock()`. Repeatedly unlocking the cache
  by hand is annoying, and `lock_cache = FALSE` prevents the cache from
  locking in the first place.

- log_make:

  Optional character scalar of a file name or connection object (such as
  [`stdout()`](https://rdrr.io/r/base/showConnections.html)) to dump
  maximally verbose log information for `make()` and other functions
  (all functions that accept a `config` argument, plus
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)).
  If you choose to use a text file as the console log, it will persist
  over multiple function calls until you delete it manually. Fields in
  each row the log file, from left to right: - The node name (short host
  name) of the computer (from `Sys.info()["nodename"]`). - The process
  ID (from [`Sys.getpid()`](https://rdrr.io/r/base/Sys.getpid.html)). -
  A timestamp with the date and time (in microseconds). - A brief
  description of what `drake` was
  doing.` The fields are separated by pipe symbols (`"\|"\`).

- log_worker:

  Logical, same as the `log_worker` argument of
  [`clustermq::workers()`](https://mschubert.github.io/clustermq/reference/workers.html)
  and
  [`clustermq::Q()`](https://mschubert.github.io/clustermq/reference/Q.html).
  Only relevant if `parallelism` is `"clustermq"`.

## Value

nothing

## Interactive mode

In interactive sessions, consider
[`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md),
[`r_outdated()`](https://docs.ropensci.org/drake/reference/r_make.md),
etc. rather than `make()`,
[`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md),
etc. The `r_*()` `drake` functions are more reproducible when the
session is interactive. If you do run `make()` interactively, please
restart your R session beforehand so your functions and global objects
get loaded into a clean reproducible environment. This prevents targets
from getting invalidated unexpectedly.

A serious drake workflow should be consistent and reliable, ideally with
the help of a main R script. This script should begin in a fresh R
session, load your packages and functions in a dependable manner, and
then run `make()`. Example:
`https://github.com/wlandau/drake-examples/tree/main/gsp`. Batch mode,
especially within a container, is particularly helpful.

Interactive R sessions are still useful, but they easily grow stale.
Targets can falsely invalidate if you accidentally change a function or
data object in your environment.

## Self-invalidation

It is possible to construct a workflow that tries to invalidate itself.
Example:

    plan <- drake_plan(
      x = {
        data(mtcars)
        mtcars$mpg
      },
      y = mean(x)
    )

Here, because [`data()`](https://rdrr.io/r/utils/data.html) loads
`mtcars` into the global environment, the very act of building `x`
changes the dependencies of `x`. In other words, without safeguards, `x`
would not be up to date at the end of `make(plan)`. Please try to avoid
workflows that modify the global environment. Functions such as
[`data()`](https://rdrr.io/r/utils/data.html) belong in your setup
scripts prior to `make()`, not in any functions or commands that get
called during `make()` itself.

For each target that is still problematic (e.g.
`https://github.com/rstudio/gt/issues/297`) you can safely run the
command in its own special
[`callr::r()`](https://callr.r-lib.org/reference/r.html) process.
Example:
`https://github.com/rstudio/gt/issues/297#issuecomment-497778735`. \#
nolint

## Cache locking

When `make()` runs, it locks the cache so other processes cannot modify
it. Same goes for
[`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md),
[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
and similar functions when `make_imports = TRUE`. This is a safety
measure to prevent simultaneous processes from corrupting the cache. If
you get an error saying that the cache is locked, either set
`make_imports = FALSE` or manually force unlock it with
`drake_cache()$unlock()`.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
[`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
config <- drake_config(my_plan)
outdated(my_plan) # Which targets need to be (re)built?
make(my_plan) # Build what needs to be built.
outdated(my_plan) # Everything is up to date.
# Change one of your imported function dependencies.
reg2 = function(d) {
  d$x3 = d$x^3
  lm(y ~ x3, data = d)
}
outdated(my_plan) # Some targets depend on reg2().
make(my_plan) # Rebuild just the outdated targets.
outdated(my_plan) # Everything is up to date again.
if (requireNamespace("visNetwork", quietly = TRUE)) {
vis_drake_graph(my_plan) # See how they fit in an interactive graph.
make(my_plan, cache_log_file = TRUE) # Write a CSV log file this time.
vis_drake_graph(my_plan) # The colors changed in the graph.
# Run targets in parallel:
# options(clustermq.scheduler = "multicore") # nolint
# make(my_plan, parallelism = "clustermq", jobs = 2) # nolint
}
clean() # Start from scratch next time around.
}
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
