# Visualize the workflow with `ggraph`/`ggplot2` **\[stable\]**

This function requires packages `ggplot2` and `ggraph`. Install them
with `install.packages(c("ggplot2", "ggraph"))`.

## Usage

``` r
drake_ggraph(
  ...,
  build_times = "build",
  digits = 3,
  targets_only = FALSE,
  main = NULL,
  from = NULL,
  mode = c("out", "in", "all"),
  order = NULL,
  subset = NULL,
  make_imports = TRUE,
  from_scratch = FALSE,
  full_legend = FALSE,
  group = NULL,
  clusters = NULL,
  show_output_files = TRUE,
  label_nodes = FALSE,
  transparency = TRUE,
  config = NULL
)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- build_times:

  Character string or logical. If character, the choices are 1.
  `"build"`: runtime of the command plus the time it take to store the
  target or import. 2. `"command"`: just the runtime of the command. 3.
  `"none"`: no build times. If logical, `build_times` selects whether to
  show the times from \`build_times(..., type = "build")“ or use no
  build times at all. See
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md)
  for details.

- digits:

  Number of digits for rounding the build times

- targets_only:

  Logical, whether to skip the imports and only include the targets in
  the workflow plan.

- main:

  Character string, title of the graph.

- from:

  Optional collection of target/import names. If `from` is nonempty, the
  graph will restrict itself to a neighborhood of `from`. Control the
  neighborhood with `mode` and `order`.

- mode:

  Which direction to branch out in the graph to create a neighborhood
  around `from`. Use `"in"` to go upstream, `"out"` to go downstream,
  and `"all"` to go both ways and disregard edge direction altogether.

- order:

  How far to branch out to create a neighborhood around `from`. Defaults
  to as far as possible. If a target is in the neighborhood, then so are
  all of its custom
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files if `show_output_files` is `TRUE`. That means the actual graph
  order may be slightly greater than you might expect, but this ensures
  consistency between `show_output_files = TRUE` and
  `show_output_files = FALSE`.

- subset:

  Optional character vector. Subset of targets/imports to display in the
  graph. Applied after `from`, `mode`, and `order`. Be advised: edges
  are only kept for adjacent nodes in `subset`. If you do not select all
  the intermediate nodes, edges will drop from the graph.

- make_imports:

  Logical, whether to make the imports first. Set to `FALSE` to increase
  speed and risk using obsolete information.

- from_scratch:

  Logical, whether to assume all the targets will be made from scratch
  on the next
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). Makes
  all targets outdated, but keeps information about build progress in
  previous
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)s.

- full_legend:

  Logical. If `TRUE`, all the node types are printed in the legend. If
  `FALSE`, only the node types used are printed in the legend.

- group:

  Optional character scalar, name of the column used to group nodes into
  columns. All the columns names of your original `drake` plan are
  choices. The other choices (such as `"status"`) are column names in
  the `nodes` . To group nodes into clusters in the graph, you must also
  supply the `clusters` argument.

- clusters:

  Optional character vector of values to cluster on. These values must
  be elements of the column of the `nodes` data frame that you specify
  in the `group` argument to
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md).

- show_output_files:

  Logical, whether to include
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files in the graph.

- label_nodes:

  Logical, whether to label the nodes. If `FALSE`, the graph will not
  have any text next to the nodes, which is recommended for large graphs
  with lots of targets.

- transparency:

  Logical, whether to allow transparency in the rendered graph. Set to
  `FALSE` if you get warnings like "semi-transparency is not supported
  on this device".

- config:

  Deprecated.

## Value

A `ggplot2` object, which you can modify with more layers, show with
[`plot()`](https://rdrr.io/r/graphics/plot.default.html), or save as a
file with
[`ggsave()`](https://ggplot2.tidyverse.org/reference/ggsave.html).

## See also

[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
[`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md),
[`render_drake_ggraph()`](https://docs.ropensci.org/drake/reference/render_drake_ggraph.md),
[`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
load_mtcars_example() # Get the code with drake_example("mtcars").
# Plot the network graph representation of the workflow.
if (requireNamespace("ggraph", quietly = TRUE)) {
  drake_ggraph(my_plan) # Save to a file with `ggplot2::ggsave()`.
}
})
} # }
```
