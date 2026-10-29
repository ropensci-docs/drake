# Compute the initial pre-build metadata of a target or import. **\[deprecated\]**

Deprecated on 2019-01-12.

## Usage

``` r
drake_meta(target, config)
```

## Arguments

- target:

  Character scalar, name of the target to get metadata.

- config:

  Top-level internal configuration list produced by
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

## Value

A list of metadata on a target. Does not include the file modification
time if the target is a file. That piece is computed later in
[`make()`](https://docs.ropensci.org/drake/reference/make.md) by
`drake:::store_outputs()`.

## Details

The metadata helps determine if the target is up to date or outdated.
The metadata of imports is used to compute the metadata of targets.
Target metadata is computed with `drake_meta()`, and then
`drake:::store_outputs()` completes the metadata after the target is
built. In other words, the output of `drake_meta()` corresponds to the
state of the target immediately before
[`make()`](https://docs.ropensci.org/drake/reference/make.md) builds it.
See
[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md) to
read the final metadata of a target, including any errors, warnings, and
messages in the last build.

## See also

[`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md),
[`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)
