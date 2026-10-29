# Create the nodes data frame used in the legend of the graph visualizations. **\[soft-deprecated\]**

Output a `visNetwork`-friendly data frame of nodes. It tells you what
the colors and shapes mean in the graph visualizations.

## Usage

``` r
legend_nodes(font_size = 20)
```

## Arguments

- font_size:

  Font size of the node label text.

## Value

A data frame of legend nodes for the graph visualizations.

## Examples

``` r
if (FALSE) { # \dontrun{
# Show the legend nodes used in graph visualizations.
# For example, you may want to inspect the color palette more closely.
if (requireNamespace("visNetwork", quietly = TRUE)) {
# visNetwork::visNetwork(nodes = legend_nodes()) # nolint
}
} # }
```
