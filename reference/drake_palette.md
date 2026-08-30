# Show drake's color palette. **\[deprecated\]**

Deprecated on 2019-01-12.

## Usage

``` r
drake_palette()
```

## Value

There is a console message, but the actual return value is `NULL`.

## Details

This function is used in both the console and graph visualizations. Your
console must have the crayon package enabled. This palette applies to
console output (internal functions `console()` and
`console_many_targets()`) and the node colors in the graph
visualizations. So if you want to contribute improvements to the
palette, please both `drake_palette()` and
`visNetwork::visNetwork(nodes = legend_nodes())`
