# Default arguments of Makefile parallelism **\[deprecated\]**

2019-01-03

## Usage

``` r
default_Makefile_args(jobs, verbose)
```

## Arguments

- jobs:

  Number of jobs.

- verbose:

  Integer, control printing to the console/terminal.

  - `0`: print nothing.

  - `1`: print target-by-target messages as
    [`make()`](https://docs.ropensci.org/drake/reference/make.md)
    progresses.

  - `2`: show a progress bar to track how many targets are done so far.

## Value

`args` for `system2(command, args)`
