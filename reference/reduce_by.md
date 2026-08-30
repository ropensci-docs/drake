# Reduce multiple groupings of targets **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
reduce_by(
  plan,
  ...,
  prefix = "target",
  begin = "",
  op = " + ",
  end = "",
  pairwise = TRUE,
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
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md)
  call is applied for each grouping. Groupings with all `NA`s in the
  selector variables are ignored.

- prefix:

  Character, prefix for naming the new targets. Suffixes are generated
  from the values of the columns specified in `...`.

- begin:

  Character, code to place at the beginning of each step in the
  reduction.

- op:

  Binary operator to apply in the reduction

- end:

  Character, code to place at the end of each step in the reduction.

- pairwise:

  Logical, whether to create multiple new targets, one for each
  pair/step in the reduction (`TRUE`), or to do the reduction all in one
  command.

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
  before
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md)?
  Because `gather_by(append = TRUE, filter = my_column == "my_value")`
  gathers on some targets while including all the original targets in
  the output. See the examples for a demonstration.

- sep:

  Character scalar, delimiter for creating the names of new targets.

## Value

A workflow plan data frame.

## Details

Perform several calls to
[`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md)
based on groupings from columns in the plan, and then row-bind the new
targets to the plan.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
