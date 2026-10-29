# Use wildcard templating to create a workflow plan data frame from a template data frame. **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
evaluate_plan(
  plan,
  rules = NULL,
  wildcard = NULL,
  values = NULL,
  expand = TRUE,
  rename = expand,
  trace = FALSE,
  columns = "command",
  sep = "_"
)
```

## Arguments

- plan:

  Workflow plan data frame, similar to one produced by
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).

- rules:

  Named list with wildcards as names and vectors of replacements as
  values. This is a way to evaluate multiple wildcards at once. When not
  `NULL`, `rules` overrules `wildcard` and `values` if not `NULL`.

- wildcard:

  Character scalar denoting a wildcard placeholder.

- values:

  Vector of values to replace the wildcard in the drake instructions.
  Will be treated as a character vector. Must be the same length as
  `plan$command` if `expand` is `TRUE`.

- expand:

  If `TRUE`, create a new rows in the workflow plan data frame if
  multiple values are assigned to a single wildcard. If `FALSE`, each
  occurrence of the wildcard is replaced with the next entry in the
  `values` vector, and the values are recycled.

- rename:

  Logical, whether to rename the targets based on the values supplied
  for the wildcards (based on `values` or `rules`).

- trace:

  Logical, whether to add columns that trace the wildcard expansion
  process. These new columns indicate which targets were evaluated and
  with which wildcards.

- columns:

  Character vector of names of columns to look for and evaluate the
  wildcards.

- sep:

  Character scalar, separator for the names of the new targets
  generated. For example, in
  `evaluate_plan(drake_plan(x = sqrt(y__)), list(y__ = 1:2), sep = ".")`,
  the names of the new targets are `x.1` and `x.2`.

## Value

A workflow plan data frame with the wildcards evaluated.

## Details

The commands in workflow plan data frames can have wildcard symbols that
can stand for datasets, parameters, function arguments, etc. These
wildcards can be evaluated over a set of possible values using
`evaluate_plan()`.

Specify a single wildcard with the `wildcard` and `values` arguments. In
each command, the text in `wildcard` will be replaced by each value in
`values` in turn. Specify multiple wildcards with the `rules` argument,
which overrules `wildcard` and `values` if not `NULL`. Here, `rules`
should be a list with wildcards as names and vectors of possible values
as list elements.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
