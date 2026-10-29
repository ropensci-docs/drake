# Deprecated: create replicates of targets. **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
expand_plan(plan, values = NULL, rename = TRUE, sep = "_", sanitize = TRUE)
```

## Arguments

- plan:

  Workflow plan data frame.

- values:

  Values to expand over. These will be appended to the names of the new
  targets.

- rename:

  Logical, whether to rename the targets based on the `values`. See the
  examples for a demo.

- sep:

  Character scalar, delimiter between the original target names and the
  values to append to create the new target names. Only relevant when
  `rename` is `TRUE`.

- sanitize:

  Logical, whether to sanitize the plan.

## Value

An expanded workflow plan data frame (with replicated targets).

## Details

Duplicates the rows of a workflow plan data frame. Prefixes are appended
to the new target names so targets still have unique names.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
