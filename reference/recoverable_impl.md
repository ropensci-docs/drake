# Internal function with a drake_config() argument

Not a user-side function.

## Usage

``` r
recoverable_impl(config = NULL, make_imports = TRUE, do_prework = TRUE)
```

## Arguments

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object.

- make_imports:

  Logical, whether to make the imports first. Set to `FALSE` to save
  some time and risk obsolete output.

- do_prework:

  Whether to do the `prework` normally supplied to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
