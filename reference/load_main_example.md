# Load the main example. **\[deprecated\]**

The main example lives at
`https://github.com/wlandau/drake-examples/tree/main/main`. Use
`drake_example("main")` to download its code. This function also
writes/overwrites the files `report.Rmd` and `raw_data.xlsx`.

## Usage

``` r
load_main_example(
  envir = parent.frame(),
  report_file = "report.Rmd",
  overwrite = FALSE,
  force = FALSE
)
```

## Arguments

- envir:

  The environment to load the example into. Defaults to your workspace.
  For an insulated workspace, set
  `envir = new.env(parent = globalenv())`.

- report_file:

  Where to write the report file `report.Rmd`.

- overwrite:

  Logical, whether to overwrite an existing file `report.Rmd`

- force:

  Deprecated.

## Value

A
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
configuration list.

## Details

Deprecated 2018-12-31.
