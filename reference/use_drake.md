# Use drake in a project **\[questioning\]**

Add top-level R script files to use `drake` in your data analysis
project. For details, read
`https://books.ropensci.org/drake/projects.html`

## Usage

``` r
use_drake(open = interactive())
```

## Arguments

- open:

  Logical, whether to open `make.R` for editing.

## Details

Files written:

1.  `make.R`: a suggested main R script for batch mode.

2.  `_drake.R`: a configuration R script for the `r_*()` functions
    documented at \# nolint
    `https://books.ropensci.org/drake/projects.html#safer-interactivity`.
    \# nolint Remarks:

- There is nothing magical about the name, `make.R`. You can call it
  whatever you want.

- Other supporting scripts, such as `R/packages.R`, `R/functions.R`, and
  `R/plan.R`, are not included.

- You can find examples at `https://github.com/wlandau/drake-examples`
  and download examples with
  [`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)
  (e.g. `drake_example("main")`).

## Examples

``` r
if (FALSE) { # \dontrun{
# use_drake(open = FALSE) # nolint
} # }
```
