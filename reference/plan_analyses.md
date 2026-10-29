# Specialized wildcard for analyses **\[deprecated\]**

Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
instead. See `https://books.ropensci.org/drake/plans.html#large-plans`
for details.

## Usage

``` r
plan_analyses(plan, datasets, sep = "_")
```

## Arguments

- plan:

  Workflow plan data frame of analysis methods. The commands in the
  `command` column must have the `dataset__` wildcard where the datasets
  go. For example, one command could be `lm(dataset__)`. Then, the
  commands in the output will include `lm(your_dataset_1)`,
  `lm(your_dataset_2)`, etc.

- datasets:

  Workflow plan data frame with instructions to make the datasets.

- sep:

  character Scalar, delimiter for creating the names of new targets.

## Value

An evaluated workflow plan data frame of analysis targets.

## Details

2019-01-13
