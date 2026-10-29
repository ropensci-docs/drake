# Show a Sankey graph of your drake project. **\[stable\]**

To save time for repeated plotting, this function is divided into
[`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
and
[`render_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/render_sankey_drake_graph.md).
A legend is unfortunately unavailable for the graph itself, but you can
see what all the colors mean with
`visNetwork::visNetwork(drake::legend_nodes())`.

## Usage

``` r
sankey_drake_graph(
  ...,
  file = character(0),
  selfcontained = FALSE,
  build_times = "build",
  digits = 3,
  targets_only = FALSE,
  from = NULL,
  mode = c("out", "in", "all"),
  order = NULL,
  subset = NULL,
  make_imports = TRUE,
  from_scratch = FALSE,
  group = NULL,
  clusters = NULL,
  show_output_files = TRUE,
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
  required.

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

- config:

  Deprecated.

## Value

A `visNetwork` graph.

## See also

[`render_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/render_sankey_drake_graph.md),
[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
[`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md),
[`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
if (requireNamespace("networkD3", quietly = TRUE)) {
if (requireNamespace("visNetwork", quietly = TRUE)) {
# Plot the network graph representation of the workflow.
sankey_drake_graph(my_plan)
# Show the legend separately.
visNetwork::visNetwork(nodes = drake::legend_nodes())
make(my_plan) # Run the project, build the targets.
sankey_drake_graph(my_plan) # The black nodes from before are now green.
# Plot a subgraph of the workflow.
sankey_drake_graph(my_plan, from = c("small", "reg2"))
}
}
}
})
} # }
```
