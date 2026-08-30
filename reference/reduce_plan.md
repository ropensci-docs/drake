# Write commands to reduce several targets down to one. **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
reduce_plan(
  plan = NULL,
  target = "target",
  begin = "",
  op = " + ",
  end = "",
  pairwise = TRUE,
  append = FALSE,
  sep = "_"
)
```

## Arguments

- plan:

  Workflow plan data frame of prespecified targets.

- target:

  Name of the new reduced target.

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

- sep:

  Character scalar, delimiter for creating new target names.

## Value

A workflow plan data frame that aggregates multiple prespecified targets
into one additional target downstream.

## Details

Creates a new workflow plan data frame with the commands to do a
reduction (i.e. to repeatedly apply a binary operator to pairs of
targets to produce one target).

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
