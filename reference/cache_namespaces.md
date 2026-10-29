# List all the `storr` cache namespaces used by drake. **\[deprecated\]**

Deprecated on 2019-01-12.

## Usage

``` r
cache_namespaces(default = storr::storr_environment()$default_namespace)
```

## Arguments

- default:

  Name of the default `storr` namespace.

## Value

A character vector of `storr` namespaces used for drake.

## Details

Ordinary users do not need to worry about this function. It is just
another window into `drake`'s internals.

## See also

[`make()`](https://docs.ropensci.org/drake/reference/make.md)
