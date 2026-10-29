# Manage the in-memory dependencies of a target. **\[stable\]**

Load/unload a target's dependencies. Not a user-side function.

## Usage

``` r
manage_memory(target, config, downstream = NULL, jobs = 1)
```

## Arguments

- target:

  Character, name of the target.

- config:

  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  list.

- downstream:

  Optional, character vector of any targets assumed to be downstream.

- jobs:

  Number of jobs for local parallel computing

## Value

Nothing.
