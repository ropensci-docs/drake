# Create a plan that maps a function to a grid of arguments. **\[deprecated\]**

Deprecated on 2019-05-16. Use
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
transformations instead. See
`https://books.ropensci.org/drake/plans.html#large-plans` for the
details.

## Usage

``` r
map_plan(args, fun, id = "id", character_only = FALSE, trace = FALSE)
```

## Arguments

- args:

  A data frame (or better yet, a `tibble`) of function arguments to
  `fun`. Here, the column names should be the names of the arguments of
  `fun`, and each row of `args` corresponds to a call to `fun`.

- fun:

  Name of a function to apply the arguments row-by-row. Supply a symbol
  if `character_only` is `FALSE` and a character scalar otherwise.

- id:

  Name of an optional column in `args` giving the names of the targets.
  If not supplied, target names will be generated automatically. `id`
  should be a symbol if `character_only` is `FALSE` and a character
  scalar otherwise.

- character_only:

  Logical, whether to interpret the `fun` and `id` arguments as
  character scalars or symbols.

- trace:

  Logical, whether to append the columns of `args` to the output
  workflow plan data frame. The added columns help "trace back" the
  original settings that went into building each target. Similar to the
  `trace` argument of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).

## Value

A workflow plan data frame.

## Details

`map_plan()` is like
[`base::Map()`](https://rdrr.io/r/base/funprog.html): it takes a
function name and a grid of arguments, and writes out all the commands
calls to apply the function to each row of arguments.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
