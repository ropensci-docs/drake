# `drake_triggers` helper

Triggers of a target.

## Usage

``` r
drake_triggers(
  command = TRUE,
  depend = TRUE,
  file = TRUE,
  seed = TRUE,
  format = TRUE,
  condition = FALSE,
  change = NULL,
  mode = c("whitelist", "blacklist", "condition")
)
```

## Arguments

- command:

  Logical, whether to rebuild the target if the
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  command changes.

- depend:

  Logical, whether to rebuild if a non-file dependency changes.

- file:

  Logical, whether to rebuild the target if a
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)/[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)/[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  file changes. Also applies to external data tracked with
  `target(format = "file")`.

- seed:

  Logical, whether to rebuild the target if the seed changes. Only makes
  a difference if you set a custom `seed` column in your
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  at some point in your workflow.

- format:

  Logical, whether to rebuild the target if the choice of specialized
  data format changes: for example, if you use `target(format = "qs")`
  one instance and `target(format = "fst")` the next. See
  `https://books.ropensci.org/drake/plans.html#special-data-formats-for-targets`
  \# nolint for details on formats.

- condition:

  R code (expression or language object) that returns a logical. The
  target will rebuild if the code evaluates to `TRUE`.

- change:

  R code (expression or language object) that returns any value. The
  target will rebuild if that value is different from last time or not
  already cached.

- mode:

  A character scalar equal to `"whitelist"` (default) or `"blacklist"`
  or `"condition"`. With the `mode` argument, you can choose how the
  `condition` trigger factors into the decision to build or skip the
  target. Here are the options.

  - `"whitelist"` (default): we *rebuild* the target whenever
    `condition` evaluates to `TRUE`. Otherwise, we defer to the other
    triggers. This behavior is the same as the decision rule described
    in the "Details" section of this help file.

  - `"blacklist"`: we *skip* the target whenever `condition` evaluates
    to `FALSE`. Otherwise, we defer to the other triggers.

  - `"condition"`: here, the `condition` trigger is the only decider,
    and we ignore all the other triggers. We *rebuild* target whenever
    `condition` evaluates to `TRUE` and *skip* it whenever `condition`
    evaluates to `FALSE`.
