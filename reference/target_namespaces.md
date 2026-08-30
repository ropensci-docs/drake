# Storr namespaces for targets **\[deprecated\]**

Deprecated on 2019-01-13.

## Usage

``` r
target_namespaces(default = storr::storr_environment()$default_namespace)
```

## Arguments

- default:

  Name of the default `storr` namespace.

## Value

A character vector of `storr` namespaces that store target-level
information.

## Details

Ordinary users do not need to worry about this function. It is just
another window into `drake`'s internals.

## See also

[`make()`](https://docs.ropensci.org/drake/reference/make.md)
