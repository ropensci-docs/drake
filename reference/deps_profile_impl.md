# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
deps_profile_impl(target, config, character_only = FALSE)
```

## Arguments

- target:

  Name of a target.

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.

- character_only:

  Logical, whether to interpret `target` as a character (`TRUE`) or a
  symbol (`FALSE`).
