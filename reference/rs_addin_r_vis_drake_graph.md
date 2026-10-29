# RStudio addin for r_vis_drake_graph() **\[stable\]**

Call
[`r_vis_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md)
in an RStudio addin.

## Usage

``` r
rs_addin_r_vis_drake_graph(r_args = list(), .print = TRUE)
```

## Arguments

- r_args:

  List of arguments to `r_fn`, not including `func` or `args`. Example:
  `r_make(r_fn = callr::r_bg, r_args = list(stdout = "stdout.log"))`.

- .print:

  Logical, whether to [`print()`](https://rdrr.io/r/base/print.html) the
  result to the console. Required for the addin.

## Value

A `visNetwork` graph.
