# Customize the decision rules for rebuilding targets **\[stable\]**

Use this function inside a target's command in your
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
or the `trigger` argument to
[`make()`](https://docs.ropensci.org/drake/reference/make.md) or
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
For details, see the chapter on triggers in the user manual:
`https://books.ropensci.org/drake/triggers.html`

## Usage

``` r
trigger(
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

## Value

A list of trigger specification details that `drake` processes
internally when it comes time to decide whether to build the target.

## Details

A target always builds if it has not been built before. Triggers allow
you to customize the conditions under which a pre-existing target
*re*builds. By default, the target will rebuild if and only if:

- Any of `command`, `depend`, or `file` is `TRUE`, or

- `condition` evaluates to `TRUE`, or

- `change` evaluates to a value different from last time. The above
  steps correspond to the "whitelist" decision rule. You can select
  other decision rules with the `mode` argument described in this help
  file. On another note, there may be a slight efficiency loss if you
  set complex triggers for `change` and/or `condition` because `drake`
  needs to load any required dependencies into memory before evaluating
  these triggers.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
# A trigger is just a set of decision rules
# to decide whether to build a target.
trigger()
#> drake_triggers
#>  $ command  : logi TRUE
#>  $ depend   : logi TRUE
#>  $ file     : logi TRUE
#>  $ seed     : logi TRUE
#>  $ format   : logi TRUE
#>  $ condition: logi FALSE
#>  $ change   : NULL
#>  $ mode     : chr "whitelist"
# This trigger will build a target on Tuesdays
# and when the value of an online dataset changes.
trigger(condition = today() == "Tuesday", change = get_online_dataset())
#> drake_triggers
#>  $ command  : logi TRUE
#>  $ depend   : logi TRUE
#>  $ file     : logi TRUE
#>  $ seed     : logi TRUE
#>  $ format   : logi TRUE
#>  $ condition: language today() == "Tuesday"
#>  $ change   : language get_online_dataset()
#>  $ mode     : chr "whitelist"
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
# You can use a global trigger argument:
# for example, to always run everything.
make(my_plan, trigger = trigger(condition = TRUE))
make(my_plan, trigger = trigger(condition = TRUE))
# You can also define specific triggers for each target.
plan <- drake_plan(
  x = sample.int(15),
  y = target(
    command = x + 1,
    trigger = trigger(depend = FALSE)
  )
)
# Now, when x changes, y will not.
make(plan)
make(plan)
plan$command[1] <- "sample.int(16)" # change x
make(plan)
}
})
} # }
```
