# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
sankey_drake_graph_impl(
  config,
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
  show_output_files = TRUE
)
```

## Arguments

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.
