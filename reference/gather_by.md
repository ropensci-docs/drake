# Gather multiple groupings of targets **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
gather_by(
  plan,
  ...,
  prefix = "target",
  gather = "list",
  append = TRUE,
  filter = NULL,
  sep = "_"
)
```

## Arguments

- plan:

  Workflow plan data frame of prespecified targets.

- ...:

  Symbols, columns of `plan` to define target groupings. A
  [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md)
  call is applied for each grouping. Groupings with all `NA`s in the
  selector variables are ignored.

- prefix:

  Character, prefix for naming the new targets. Suffixes are generated
  from the values of the columns specified in `...`.

- gather:

  Function used to gather the targets. Should be one of `list(...)`,
  `c(...)`, `rbind(...)`, or similar.

- append:

  Logical. If `TRUE`, the output will include the original rows in the
  `plan` argument. If `FALSE`, the output will only include the new
  targets and commands.

- filter:

  An expression like you would pass to
  [`dplyr::filter()`](https://dplyr.tidyverse.org/reference/filter.html).
  The rows for which `filter` evaluates to `TRUE` will be gathered, and
  the rest will be excluded from gathering. Why not just call
  [`dplyr::filter()`](https://dplyr.tidyverse.org/reference/filter.html)
  before `gather_by()`? Because
  `gather_by(append = TRUE, filter = my_column == "my_value")` gathers
  on some targets while including all the original targets in the
  output. See the examples for a demonstration.

- sep:

  Character scalar, delimiter for creating the names of new targets.

## Value

A workflow plan data frame.

## Details

Perform several calls to
[`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md)
based on groupings from columns in the plan, and then row-bind the new
targets to the plan.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
