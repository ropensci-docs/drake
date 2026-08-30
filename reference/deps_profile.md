# Find out why a target is out of date. **\[stable\]**

The dependency profile can give you a hint as to why a target is out of
date. It can tell you if

- the command changed (`deps_profile()` reports the *hash* of the
  command, not the command itself)

- at least one input file changed,

- at least one output file changed,

- or a non-file dependency changed. For this last part, the imports need
  to be up to date in the cache, which you can do with
  [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
  or `make(skip_targets = TRUE)`.

- the pseudo-random number generator seed changed. Unfortunately,
  `deps_profile()` does not currently get more specific than that.

## Usage

``` r
deps_profile(target, ..., character_only = FALSE, config = NULL)
```

## Arguments

- target:

  Name of the target.

- ...:

  Arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), such as
  `plan` and `targets`.

- character_only:

  Logical, whether to assume `target` is a character string rather than
  a symbol.

- config:

  Deprecated.

## Value

A data frame of old and new values for each of the main triggers, along
with an indication of which values changed since the last
[`make()`](https://docs.ropensci.org/drake/reference/make.md).

## See also

[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md),
[`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md),
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Load drake's canonical example.
make(my_plan) # Run the project, build the targets.
# Get some example dependency profiles of targets.
deps_profile(small, my_plan)
# Change a dependency.
simulate <- function(x) {}
# Update the in-memory imports in the cache
# so deps_profile can detect changes to them.
# Changes to targets are already cached.
make(my_plan, skip_targets = TRUE)
# The dependency hash changed.
deps_profile(small, my_plan)
}
})
} # }
```
