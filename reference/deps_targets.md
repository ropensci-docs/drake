# See the dependencies of a target **\[deprecated\]**

Use
[`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
(singular) instead.

## Usage

``` r
deps_targets(targets, config, reverse = FALSE)
```

## Arguments

- targets:

  A character vector of target names.

- config:

  An output list from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)

- reverse:

  Logical, whether to compute reverse dependencies (targets immediately
  downstream) instead of ordinary dependencies.

## Value

Names of dependencies listed by type (object, input file, etc).

## Details

Deprecated on 2018-08-30.
