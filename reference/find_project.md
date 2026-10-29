# Search up the file system for the nearest root path of a drake project. **\[deprecated\]**

Deprecated on 2019-01-08.

## Usage

``` r
find_project(path = getwd())
```

## Arguments

- path:

  Starting path for search back for the project. Should be a
  subdirectory of the drake project.

## Value

File path of the nearest drake project or `NULL` if no drake project is
found.

## Details

Only works if the cache is a file system in a folder named `.drake`
(default).

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)
