# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
text_drake_graph_impl(
  config,
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
  print = TRUE
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
