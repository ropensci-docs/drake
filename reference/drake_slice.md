# Take a strategic subset of a dataset. **\[stable\]**

`drake_slice()` is similar to
[`split()`](https://docs.ropensci.org/drake/reference/transformations.md).
Both functions partition data into disjoint subsets, but whereas
[`split()`](https://docs.ropensci.org/drake/reference/transformations.md)
returns *all* the subsets, `drake_slice()` returns just *one*. In other
words, `drake_slice(..., index = i)` returns `split(...)[[i]]`. Other
features: 1. `drake_slice()` works on vectors, data frames, matrices,
lists, and arbitrary arrays. 2. Like
[`parallel::splitIndices()`](https://rdrr.io/r/parallel/splitIndices.html),
`drake_slice()` tries to distribute the data uniformly across subsets.
See the examples to learn why splitting is useful in `drake`.

## Usage

``` r
drake_slice(data, slices, index, margin = 1L, drop = FALSE)
```

## Arguments

- data:

  A list, vector, data frame, matrix, or arbitrary array. Anything with
  a [`length()`](https://rdrr.io/r/base/length.html) or
  [`dim()`](https://rdrr.io/r/base/dim.html).

- slices:

  Integer of length 1, number of slices (i.e. pieces) of the whole
  dataset. Remember, `drake_slice(index = i)` returns only slice number
  `i`.

- index:

  Integer of length 1, which piece of the partition to return.

- margin:

  Integer of length 1, margin over which to split the data. For example,
  for a data frame or matrix, use `margin = 1` to split over rows and
  `margin = 2` to split over columns. Similar to `MARGIN` in
  [`apply()`](https://rdrr.io/r/base/apply.html).

- drop:

  Logical, for matrices and arrays. If
  `TRUE`,` the result is coerced to the lowest possible dimension. See ?`\[\`
  for details.

## Value

A subset of `data`.

## Examples

``` r
# Simple usage
x <- matrix(seq_len(20), nrow = 5)
x
#>      [,1] [,2] [,3] [,4]
#> [1,]    1    6   11   16
#> [2,]    2    7   12   17
#> [3,]    3    8   13   18
#> [4,]    4    9   14   19
#> [5,]    5   10   15   20
drake_slice(x, slices = 3, index = 1)
#>      [,1] [,2] [,3] [,4]
#> [1,]    1    6   11   16
#> [2,]    2    7   12   17
drake_slice(x, slices = 3, index = 2)
#>      [,1] [,2] [,3] [,4]
#> [1,]    3    8   13   18
#> [2,]    4    9   14   19
drake_slice(x, slices = 3, index = 3)
#>      [,1] [,2] [,3] [,4]
#> [1,]    5   10   15   20
drake_slice(x, slices = 3, margin = 2, index = 1)
#>      [,1] [,2]
#> [1,]    1    6
#> [2,]    2    7
#> [3,]    3    8
#> [4,]    4    9
#> [5,]    5   10
# In drake, you can split a large dataset over multiple targets.
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
plan <- drake_plan(
  large_data = mtcars,
  data_split = target(
    drake_slice(large_data, slices = 32, index = i),
    transform = map(i = !!seq_len(32))
  )
)
plan
cache <- storr::storr_environment()
make(plan, cache = cache, session_info = FALSE, verbose = FALSE)
readd(data_split_1L, cache = cache)
readd(data_split_2L, cache = cache)
})
} # }
```
