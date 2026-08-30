# List the most upstream *recoverable* outdated targets. **\[stable\]**

Only shows the most upstream updated targets. Whether downstream targets
are recoverable depends on the eventual values of the upstream targets
in the next
[`make()`](https://docs.ropensci.org/drake/reference/make.md).

## Usage

``` r
recoverable(..., make_imports = TRUE, do_prework = TRUE, config = NULL)
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

Character vector of the names of recoverable targets.

## Recovery

`make(recover = TRUE, recoverable = TRUE)` powers automated data
recovery. The default of `recover` is `FALSE` because targets recovered
from the distant past may have been generated with earlier versions of R
and earlier package environments that no longer exist.

How it works: if `recover` is `TRUE`, `drake` tries to salvage old
target values from the cache instead of running commands from the plan.
A target is recoverable if

1.  There is an old value somewhere in the cache that shares the
    command, dependencies, etc. of the target about to be built.

2.  The old value was generated with `make(recoverable = TRUE)`.

If both conditions are met, `drake` will

1.  Assign the most recently-generated admissible data to the target,
    and

2.  skip the target's command.

## See also

[`r_recoverable()`](https://docs.ropensci.org/drake/reference/r_make.md),
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
make(my_plan)
clean()
outdated(my_plan) # Which targets are outdated?
recoverable(my_plan) # Which of these are recoverable and upstream?
# The report still builds because clean() removes report.md,
# but make() recovers the rest.
make(my_plan, recover = TRUE)
outdated(my_plan)
# When was the *recovered* small data actually built (first stored)?
# (Was I using a different version of R back then?)
diagnose(small)$date
# If you set the same seed as before, you can even
# rename targets without having to build them again.
# For an example, see
# the "Reproducible data recovery and renaming" section of
# https://github.com/ropensci/drake/blob/main/README.md.
}
})
} # }
```
