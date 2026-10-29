# Show an interactive visual network representation of your drake project. **\[stable\]**

It is good practice to visualize the dependency graph before running the
targets.

## Usage

``` r
vis_drake_graph(
  ...,
  file = character(0),
  selfcontained = FALSE,
  build_times = "build",
  digits = 3,
  targets_only = FALSE,
  font_size = 20,
  layout = NULL,
  main = NULL,
  direction = NULL,
  hover = FALSE,
  navigationButtons = TRUE,
  from = NULL,
  mode = c("out", "in", "all"),
  order = NULL,
  subset = NULL,
  ncol_legend = 1,
  full_legend = FALSE,
  make_imports = TRUE,
  from_scratch = FALSE,
  group = NULL,
  clusters = NULL,
  show_output_files = TRUE,
  collapse = TRUE,
  on_select_col = NULL,
  on_select = NULL,
  level_separation = NULL,
  config = NULL
)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- file:

  Name of a file to save the graph. If `NULL` or `character(0)`, no file
  is saved and the graph is rendered and displayed within R. If the file
  ends in a `.png`, `.jpg`, `.jpeg`, or `.pdf` extension, then a static
  image will be saved. In this case, the webshot package and PhantomJS
  are required:
  `install.packages("webshot"); webshot::install_phantomjs()`. If the
  file does not end in a `.png`, `.jpg`, `.jpeg`, or `.pdf` extension,
  an HTML file will be saved, and you can open the interactive graph
  using a web browser.

- selfcontained:

  Logical, whether to save the `file` as a self-contained HTML file
  (with external resources base64 encoded) or a file with external
  resources placed in an adjacent directory. If `TRUE`, pandoc is
  required. The `selfcontained` argument only applies to HTML files. In
  other words, if `file` is a PNG, PDF, or JPEG file, for instance, the
  point is moot.

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

- layout:

  Deprecated.

- main:

  Character string, title of the graph.

- direction:

  Deprecated.

- hover:

  Logical, whether to show text (file contents, commands, etc.) when you
  hover your cursor over a node.

- navigationButtons:

  Logical, whether to add navigation buttons with
  `visNetwork::visInteraction(navigationButtons = TRUE)`

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

- ncol_legend:

  Number of columns in the legend nodes. To remove the legend entirely,
  set `ncol_legend` to `NULL` or `0`.

- full_legend:

  Logical. If `TRUE`, all the node types are printed in the legend. If
  `FALSE`, only the node types used are printed in the legend.

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

- collapse:

  Logical, whether to allow nodes to collapse if you double click on
  them. Analogous to `visNetwork::visOptions(collapse = TRUE)`.

- on_select_col:

  Optional string corresponding to the column name in the plan that
  should provide data for the `on_select` event.

- on_select:

  defines node selection event handling. Either a string of valid
  JavaScript that may be passed to
  [`visNetwork::visEvents()`](https://rdrr.io/pkg/visNetwork/man/visEvents.html),
  or one of the following: `TRUE`, `NULL`/`FALSE`. If `TRUE` , enables
  the default behavior of opening the link specified by the
  `on_select_col` given to
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md).
  `NULL`/`FALSE` disables the behavior.

- level_separation:

  Numeric, `levelSeparation` argument to
  [`visNetwork::visHierarchicalLayout()`](https://rdrr.io/pkg/visNetwork/man/visHierarchicalLayout.html).
  Controls the distance between hierarchical levels. Consider setting if
  the aspect ratio of the graph is far from 1. Defaults to 150 through
  `visNetwork`.

- config:

  Deprecated.

## Value

A `visNetwork` graph.

## Details

For enhanced interactivity in the graph, see the `mandrake` package.

## See also

[`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md),
[`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md),
[`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md),
[`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
# Plot the network graph representation of the workflow.
if (requireNamespace("visNetwork", quietly = TRUE)) {
vis_drake_graph(my_plan)
make(my_plan) # Run the project, build the targets.
vis_drake_graph(my_plan) # The red nodes from before are now green.
# Plot a subgraph of the workflow.
vis_drake_graph(
  my_plan,
  from = c("small", "reg2")
)
}
}
})
} # }
```
