# RStudio addin for r_make() **\[stable\]**

Call [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md)
in an RStudio addin.

## Usage

``` r
rs_addin_r_make(r_args = list())
```

## Arguments

- r_args:

  List of arguments to `r_fn`, not including `func` or `args`. Example:
  `r_make(r_fn = callr::r_bg, r_args = list(stdout = "stdout.log"))`.

## Value

Nothing.
