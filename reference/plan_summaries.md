# Specialized wildcard for summaries **\[deprecated\]**

Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
with transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for details.

## Usage

``` r
plan_summaries(
  plan,
  analyses,
  datasets,
  gather = rep("list", nrow(plan)),
  sep = "_"
)
```

## Arguments

- plan:

  Workflow plan data frame with commands for the summaries. Use the
  `analysis__` and `dataset__` wildcards just like the `dataset__`
  wildcard in
  [`plan_analyses()`](https://docs.ropensci.org/drake/reference/plan_analyses.md).

- analyses:

  Workflow plan data frame of analysis instructions.

- datasets:

  Workflow plan data frame with instructions to make or import the
  datasets.

- gather:

  Character vector, names of functions to gather the summaries. If not
  `NULL`, the length must be the number of rows in the `plan`. See the
  [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md)
  function for more.

- sep:

  Character scalar, delimiter for creating the new target names.

## Value

An evaluated workflow plan data frame of instructions for computing
summaries of analyses and datasets. analyses of multiple datasets in
multiple ways.

## Details

2019-01-13
