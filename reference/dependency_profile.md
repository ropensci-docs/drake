# States of the dependencies of a target **\[deprecated\]**

Deprecated on 2019-02-14.

## Usage

``` r
dependency_profile(target, config, character_only = FALSE)
```

## Arguments

- target:

  Name of the target.

- config:

  Deprecated.

- character_only:

  Logical, whether to assume `target` is a character string rather than
  a symbol.

## Value

A data frame of the old hashes and new hashes of the data frame, along
with an indication of which hashes changed since the last
[`make()`](https://docs.ropensci.org/drake/reference/make.md).
