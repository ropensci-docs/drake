# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
vis_drake_graph_impl(
  config,
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
  level_separation = NULL
)
```

## Arguments

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.
