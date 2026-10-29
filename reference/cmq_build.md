# Build a target using the clustermq backend **\[stable\]**

For internal use only

## Usage

``` r
cmq_build(target, meta, deps, spec, config_tmp, config)
```

## Arguments

- target:

  Target name.

- meta:

  List of metadata.

- deps:

  Named list of target dependencies.

- spec:

  Internal, part of the full `config$spec`.

- config_tmp:

  Internal, extra parts of `config` that the workers need.

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  list.
