# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
drake_ggraph_impl(
  config,
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
  transparency = TRUE
)
```

## Arguments

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.

- make_imports:

  Logical, whether to make the imports first. Set to `FALSE` to save
  some time and risk obsolete output.
