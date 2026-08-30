# Deprecated, get a trace of a dynamic target's value. **\[deprecated\]**

Deprecated on 2019-12-10. Use
[`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md)
instead.

## Usage

``` r
get_trace(trace, value)
```

## Arguments

- trace:

  Character, name of the trace you want to extract. Such trace names are
  declared in the `.trace` argument of
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  or
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md)..

- value:

  Value of the dynamic target

## Value

The dynamic trace of one target in another: a vector of values from a
grouping variable.
