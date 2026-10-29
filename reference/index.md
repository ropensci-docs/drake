# Package index

## Help

- [`drake-package`](https://docs.ropensci.org/drake/reference/drake-package.md)
  [`drake`](https://docs.ropensci.org/drake/reference/drake-package.md)
  : drake: A pipeline toolkit for reproducible computation at scale.

## Examples

- [`use_drake()`](https://docs.ropensci.org/drake/reference/use_drake.md)
  :

  Use drake in a project **\[questioning\]**

- [`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)
  :

  Download the files of an example `drake` project. **\[stable\]**

- [`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md)
  :

  List the names of all the drake examples. **\[stable\]**

- [`load_mtcars_example()`](https://docs.ropensci.org/drake/reference/load_mtcars_example.md)
  :

  Load the mtcars example. **\[stable\]**

- [`clean_mtcars_example()`](https://docs.ropensci.org/drake/reference/clean_mtcars_example.md)
  :

  Clean the mtcars example from `drake_example("mtcars")` **\[stable\]**

## Build and configure

- [`make()`](https://docs.ropensci.org/drake/reference/make.md) :

  Run your project (build the outdated targets). **\[stable\]**

- [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  :

  Ending of \_drake.R for r_make() and friends **\[stable\]**

- [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)
  :

  Build/process a single target or import. **\[questioning\]**

## drake plans and helpers

- [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  :

  Create a drake plan for the `plan` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
  **\[stable\]**

- [`transform_plan()`](https://docs.ropensci.org/drake/reference/transform_plan.md)
  :

  Transform a plan **\[stable\]**

- [`drake_plan_source()`](https://docs.ropensci.org/drake/reference/drake_plan_source.md)
  :

  Show the code required to produce a given `drake` plan **\[stable\]**

- [`code_to_function()`](https://docs.ropensci.org/drake/reference/code_to_function.md)
  :

  Turn a script into a function. **\[stable\]**

- [`code_to_plan()`](https://docs.ropensci.org/drake/reference/code_to_plan.md)
  :

  Turn an R script file or `knitr` / R Markdown report into a `drake`
  plan. **\[questioning\]**

- [`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md)
  :

  Turn a `drake` plan into a plain R script file. **\[questioning\]**

- [`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md)
  :

  Turn a `drake` plan into an R notebook. **\[questioning\]**

- [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md)
  :

  Row-bind together drake plans **\[stable\]**

- [`drake_slice()`](https://docs.ropensci.org/drake/reference/drake_slice.md)
  :

  Take a strategic subset of a dataset. **\[stable\]**

## drake plan keywords

- [`target()`](https://docs.ropensci.org/drake/reference/target.md) :

  Customize a target in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
  **\[stable\]**

- [`trigger()`](https://docs.ropensci.org/drake/reference/trigger.md) :

  Customize the decision rules for rebuilding targets **\[stable\]**

- [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md) :

  Declare input files and directories. **\[stable\]**

- [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  :

  Declare output files and directories. **\[stable\]**

- [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  :

  Declare `knitr`/`rmarkdown` source files as dependencies.
  **\[stable\]**

- [`cancel()`](https://docs.ropensci.org/drake/reference/cancel.md) :

  Cancel a target mid-build **\[stable\]**

- [`cancel_if()`](https://docs.ropensci.org/drake/reference/cancel_if.md)
  :

  Cancel a target mid-build under some condition **\[stable\]**

- [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md) :

  Ignore code **\[stable\]**

- [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md) :

  Suppress dependency detection. **\[stable\]**

- [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md) :

  Name of the current target **\[stable\]**

- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md)
  :

  Get the environment where drake builds targets **\[questioning\]**

## Transformations

- [`transformations`](https://docs.ropensci.org/drake/reference/transformations.md)
  [`map`](https://docs.ropensci.org/drake/reference/transformations.md)
  [`split`](https://docs.ropensci.org/drake/reference/transformations.md)
  [`cross`](https://docs.ropensci.org/drake/reference/transformations.md)
  [`combine`](https://docs.ropensci.org/drake/reference/transformations.md)
  [`group`](https://docs.ropensci.org/drake/reference/transformations.md)
  :

  Transformations in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
  **\[stable\]**

## Dynamic branching

- [`subtargets()`](https://docs.ropensci.org/drake/reference/subtargets.md)
  :

  List sub-targets **\[stable\]**

- [`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md)
  :

  Read a trace of a dynamic target. **\[stable\]**

## Reproducible R session management

- [`drake_script()`](https://docs.ropensci.org/drake/reference/drake_script.md)
  :

  Write an example `_drake.R` script to the current working directory.

- [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_drake_build()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_outdated()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_recoverable()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_missed()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_deps_target()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_drake_graph_info()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_vis_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_drake_ggraph()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_text_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_predict_runtime()`](https://docs.ropensci.org/drake/reference/r_make.md)
  [`r_predict_workers()`](https://docs.ropensci.org/drake/reference/r_make.md)
  :

  Launch a drake function in a fresh new R process **\[stable\]**

## Network graphs and visualization

- [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  :

  Show an interactive visual network representation of your drake
  project. **\[stable\]**

- [`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md)
  :

  Show a Sankey graph of your drake project. **\[stable\]**

- [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  :

  Visualize the workflow with `ggraph`/`ggplot2` **\[stable\]**

- [`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)
  :

  Show a workflow graph as text in your terminal window. **\[stable\]**

- [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md)
  :

  Render a visualization using the data frames generated by
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md).
  **\[stable\]**

- [`render_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/render_sankey_drake_graph.md)
  :

  Render a Sankey diagram from
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md).
  **\[stable\]**

- [`render_drake_ggraph()`](https://docs.ropensci.org/drake/reference/render_drake_ggraph.md)
  :

  Visualize the workflow with `ggplot2`/`ggraph` using
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  output. **\[stable\]**

- [`render_text_drake_graph()`](https://docs.ropensci.org/drake/reference/render_text_drake_graph.md)
  :

  Show a workflow graph as text in your terminal window using
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  output. **\[stable\]**

- [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  :

  Prepare the workflow graph for visualization **\[stable\]**

- [`legend_nodes()`](https://docs.ropensci.org/drake/reference/legend_nodes.md)
  :

  Create the nodes data frame used in the legend of the graph
  visualizations. **\[soft-deprecated\]**

## Target status

- [`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md)
  :

  History and provenance **\[stable\]**

- [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
  :

  List the targets that are out of date. **\[stable\]**

- [`recoverable()`](https://docs.ropensci.org/drake/reference/recoverable.md)
  :

  List the most upstream *recoverable* outdated targets. **\[stable\]**

- [`missed()`](https://docs.ropensci.org/drake/reference/missed.md) :

  Report any import objects required by your drake_plan plan but missing
  from your workspace or file system. **\[stable\]**

- [`tracked()`](https://docs.ropensci.org/drake/reference/tracked.md) :

  List the targets and imports that are reproducibly tracked.
  **\[stable\]**

- [`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md)
  :

  List the dependencies of a function or command **\[stable\]**

- [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
  :

  List the dependencies of a target **\[stable\]**

- [`deps_knitr()`](https://docs.ropensci.org/drake/reference/deps_knitr.md)
  :

  Find the drake dependencies of a dynamic knitr report target.
  **\[stable\]**

- [`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md)
  :

  Find out why a target is out of date. **\[stable\]**

## Debugging and testing

- [`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md)
  :

  Get diagnostic metadata on a target. **\[stable\]**

- [`drake_debug()`](https://docs.ropensci.org/drake/reference/drake_debug.md)
  :

  Run a single target's command in debug mode.' **\[questioning\]**

## High-performance computing

- [`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md)
  :

  Write a template file for deploying work to a cluster / job scheduler.
  **\[stable\]**

- [`drake_hpc_template_files()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_files.md)
  :

  List the available example template files for deploying work to a
  cluster / job scheduler. **\[stable\]**

## Time

- [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md)
  :

  See the time it took to build each target. **\[stable\]**

- [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)
  :

  Predict the elapsed runtime of the next call to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) for
  non-staged parallel backends. **\[stable\]**

- [`predict_workers()`](https://docs.ropensci.org/drake/reference/predict_workers.md)
  :

  Predict the load balancing of the next call to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) for
  non-staged parallel backends. **\[stable\]**

## Cache creation

- [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md)
  :

  Get the cache of a `drake` project. **\[stable\]**

- [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md)
  :

  Make a new `drake` cache. **\[stable\]**

- [`find_cache()`](https://docs.ropensci.org/drake/reference/find_cache.md)
  :

  Search up the file system for the nearest drake cache. **\[stable\]**

## Cache usage

- [`readd()`](https://docs.ropensci.org/drake/reference/readd.md)
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) :

  Read and return a drake target/import from the cache. **\[stable\]**

- [`cached()`](https://docs.ropensci.org/drake/reference/cached.md) :

  List targets in the cache. **\[stable\]**

- [`cached_planned()`](https://docs.ropensci.org/drake/reference/cached_planned.md)
  :

  List targets in both the plan and the cache. **\[stable\]**

- [`cached_unplanned()`](https://docs.ropensci.org/drake/reference/cached_unplanned.md)
  :

  List targets in the cache but not the plan. **\[stable\]**

- [`drake_cache_log()`](https://docs.ropensci.org/drake/reference/drake_cache_log.md)
  :

  Get the state of the cache. **\[stable\]**

- [`drake_get_session_info()`](https://docs.ropensci.org/drake/reference/drake_get_session_info.md)
  :

  Session info of the last call to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
  **\[stable\]**

- [`read_drake_seed()`](https://docs.ropensci.org/drake/reference/read_drake_seed.md)
  :

  Read the pseudo-random number generator seed of the project.
  **\[stable\]**

- [`show_source()`](https://docs.ropensci.org/drake/reference/show_source.md)
  :

  Show how a target/import was produced. **\[stable\]**

- [`file_store()`](https://docs.ropensci.org/drake/reference/file_store.md)
  :

  Show a file's encoded representation in the cache **\[stable\]**

- [`drake_tempfile()`](https://docs.ropensci.org/drake/reference/drake_tempfile.md)
  :

  drake tempfile **\[stable\]**

## Cache maintenance

- [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) :

  Invalidate and deregister targets. **\[stable\]**

- [`which_clean()`](https://docs.ropensci.org/drake/reference/which_clean.md)
  :

  Which targets will
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md)
  invalidate? **\[stable\]**

- [`drake_gc()`](https://docs.ropensci.org/drake/reference/drake_gc.md)
  :

  Do garbage collection on the drake cache. **\[stable\]**

- [`rescue_cache()`](https://docs.ropensci.org/drake/reference/rescue_cache.md)
  :

  Try to repair a drake cache that is prone to throwing `storr`-related
  errors. **\[questioning\]**

## Progress

- [`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md)
  :

  Get the build progress of your targets **\[stable\]**

- [`drake_running()`](https://docs.ropensci.org/drake/reference/drake_running.md)
  :

  List running targets. **\[stable\]**

- [`drake_done()`](https://docs.ropensci.org/drake/reference/drake_done.md)
  :

  List done targets. **\[stable\]**

- [`drake_failed()`](https://docs.ropensci.org/drake/reference/drake_failed.md)
  :

  List failed targets. **\[stable\]**

- [`drake_cancelled()`](https://docs.ropensci.org/drake/reference/drake_cancelled.md)
  :

  List cancelled targets. **\[stable\]**
