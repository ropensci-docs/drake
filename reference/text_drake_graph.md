# Show a workflow graph as text in your terminal window. **\[stable\]**

This is a low-tech version of
[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
and friends. It is designed for when you do not have access to the usual
graphics devices for viewing visuals in an interactive R session: for
example, if you are logged into a remote machine with SSH and you do not
have access to X Window support.

## Usage

``` r
text_drake_graph(
  ...,
  from = NULL,
  mode = c("out", "in", "all"),
  order = NULL,
  subset = NULL,
  targets_only = FALSE,
  make_imports = TRUE,
  from_scratch = FALSE,
  group = NULL,
  clusters = NULL,
  show_output_files = TRUE,
  nchar = 1L,
  print = TRUE,
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

- targets_only:

  Logical, whether to skip the imports and only include the targets in
  the workflow plan.

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

- nchar:

  For each node, maximum number of characters of the node label to show.
  Can be 0, in which case each node is a colored box instead of a node
  label. Caution: `nchar` \> 0 will mess with the layout.

- print:

  Logical. If `TRUE`, the graph will print to the console via
  [`message()`](https://rdrr.io/r/base/message.html). If `FALSE`,
  nothing is printed. However, you still have the visualization because
  `text_drake_graph()` and
  [`render_text_drake_graph()`](https://docs.ropensci.org/drake/reference/render_text_drake_graph.md)
  still invisibly return a character string that you can print yourself
  with [`message()`](https://rdrr.io/r/base/message.html).

- config:

  Deprecated.

## Value

A `visNetwork` graph.

## See also

[`render_text_drake_graph()`](https://docs.ropensci.org/drake/reference/render_text_drake_graph.md),
[`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
[`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md),
[`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
# Plot the network graph representation of the workflow.
pkg <- requireNamespace("txtplot", quietly = TRUE) &&
  requireNamespace("visNetwork", quietly = TRUE)
if (pkg) {
text_drake_graph(my_plan)
make(my_plan) # Run the project, build the targets.
text_drake_graph(my_plan) # The black nodes from before are now green.
}
}
})
} # }
```
