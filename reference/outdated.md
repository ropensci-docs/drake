# List the targets that are out of date. **\[stable\]**

Outdated targets will be rebuilt in the next
[`make()`](https://docs.ropensci.org/drake/reference/make.md).
`outdated()` does not show dynamic sub-targets.

## Usage

``` r
outdated(..., make_imports = TRUE, do_prework = TRUE, config = NULL)
```

## Arguments

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets` and `envir`.

- make_imports:

  Logical, whether to make the imports first. Set to `FALSE` to save
  some time and risk obsolete output.

- do_prework:

  Whether to do the `prework` normally supplied to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).

- config:

  Deprecated (2019-12-21). A configured workflow from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

## Value

Character vector of the names of outdated targets.

## See also

[`r_outdated()`](https://docs.ropensci.org/drake/reference/r_make.md),
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
[`missed()`](https://docs.ropensci.org/drake/reference/missed.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
# Recopute the config list early and often to have the
# most current information. Do not modify the config list by hand.
outdated(my_plan) # Which targets are out of date?
make(my_plan) # Run the projects, build the targets.
# Now, everything should be up to date (no targets listed).
outdated(my_plan)
}
})
} # }
```
