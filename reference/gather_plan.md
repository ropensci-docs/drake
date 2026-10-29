# Combine targets **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
gather_plan(plan = NULL, target = "target", gather = "list", append = FALSE)
```

## Arguments

- plan:

  Workflow plan data frame of prespecified targets.

- target:

  Name of the new aggregated target.

- gather:

  Function used to gather the targets. Should be one of `list(...)`,
  `c(...)`, `rbind(...)`, or similar.

- append:

  Logical. If `TRUE`, the output will include the original rows in the
  `plan` argument. If `FALSE`, the output will only include the new
  targets and commands.

## Value

A workflow plan data frame that aggregates multiple prespecified targets
into one additional target downstream.

## Details

Creates a new workflow plan to aggregate existing targets in the
supplied plan.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
