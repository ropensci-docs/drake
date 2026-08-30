# Task passed to individual futures in the `"future"` backend **\[stable\]**

For internal use only. Only exported to make available to futures.

## Usage

``` r
future_build(target, meta, config, spec, config_tmp, protect)
```

## Arguments

- target:

  Name of the target.

- meta:

  A list of metadata.

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  list.

- config_tmp:

  Internal, parts of `config` that the workers need.

- protect:

  Names of targets that still need their dependencies available in
  memory.

## Value

Either the target value or a list of build results.
