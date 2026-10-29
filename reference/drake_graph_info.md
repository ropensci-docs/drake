# Prepare the workflow graph for visualization **\[stable\]**

With the returned data frames, you can plot your own custom `visNetwork`
graph.

## Usage

``` r
drake_graph_info(
  ...,
  from = NULL,
  mode = c("out", "in", "all"),
  order = NULL,
  subset = NULL,
  build_times = "build",
  digits = 3,
  targets_only = FALSE,
  font_size = 20,
  from_scratch = FALSE,
  make_imports = TRUE,
  full_legend = FALSE,
  group = NULL,
  clusters = NULL,
  show_output_files = TRUE,
  hover = FALSE,
  on_select_col = NULL,
  config = NULL
)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

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

- font_size:

  Numeric, font size of the node labels in the graph

- from_scratch:

  Logical, whether to assume all the targets will be made from scratch
  on the next
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). Makes
  all targets outdated, but keeps information about build progress in
  previous
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)s.

- make_imports:

  Logical, whether to make the imports first. Set to `FALSE` to increase
  speed and risk using obsolete information.

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
  in the `group` argument to `drake_graph_info()`.

- show_output_files:

  Logical, whether to include
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files in the graph.

- hover:

  Logical, whether to show text (file contents, commands, etc.) when you
  hover your cursor over a node.

- on_select_col:

  Optional string corresponding to the column name in the plan that
  should provide data for the `on_select` event.

- config:

  Deprecated.

## Value

A list of three data frames: one for nodes, one for edges, and one for
the legend nodes. The list also contains the default title of the graph.

## See also

[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (requireNamespace("visNetwork", quietly = TRUE)) {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
vis_drake_graph(my_plan)
# Get a list of data frames representing the nodes, edges,
# and legend nodes of the visNetwork graph from vis_drake_graph().
raw_graph <- drake_graph_info(my_plan)
# Choose a subset of the graph.
smaller_raw_graph <- drake_graph_info(
  my_plan,
  from = c("small", "reg2"),
  mode = "in"
)
# Inspect the raw graph.
str(raw_graph)
# Use the data frames to plot your own custom visNetwork graph.
# For example, you can omit the legend nodes
# and change the direction of the graph.
library(visNetwork)
graph <- visNetwork(nodes = raw_graph$nodes, edges = raw_graph$edges)
visHierarchicalLayout(graph, direction = 'UD')
}
}
})
} # }
```
