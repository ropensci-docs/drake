# List the dependencies of a function or command **\[stable\]**

Functions are assumed to be imported, and language/text are assumed to
be commands in a plan.

## Usage

``` r
deps_code(x)
```

## Arguments

- x:

  A function, expression, or text.

## Value

A data frame of the dependencies.

## See also

[`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md),
[`deps_knitr()`](https://docs.ropensci.org/drake/reference/deps_knitr.md)

## Examples

``` r
# Your workflow likely depends on functions in your workspace.
f <- function(x, y) {
  out <- x + y + g(x)
  saveRDS(out, "out.rds")
}
# Find the dependencies of f. These could be R objects/functions
# in your workspace or packages. Any file names or target names
# will be ignored.
deps_code(f)
#> # A tibble: 2 × 2
#>   name    type   
#>   <chr>   <chr>  
#> 1 saveRDS globals
#> 2 g       globals
# Define a workflow plan data frame that uses your function f().
my_plan <- drake_plan(
  x = 1 + some_object,
  my_target = x + readRDS(file_in("tracked_input_file.rds")),
  return_value = f(x, y, g(z + w))
)
# Get the dependencies of workflow plan commands.
# Here, the dependencies could be R functions/objects from your workspace
# or packages, imported files, or other targets in the workflow plan.
deps_code(my_plan$command[[1]])
#> # A tibble: 1 × 2
#>   name        type   
#>   <chr>       <chr>  
#> 1 some_object globals
deps_code(my_plan$command[[2]])
#> # A tibble: 3 × 2
#>   name                   type   
#>   <chr>                  <chr>  
#> 1 x                      globals
#> 2 readRDS                globals
#> 3 tracked_input_file.rds file_in
deps_code(my_plan$command[[3]])
#> # A tibble: 6 × 2
#>   name  type   
#>   <chr> <chr>  
#> 1 w     globals
#> 2 x     globals
#> 3 y     globals
#> 4 z     globals
#> 5 f     globals
#> 6 g     globals
# You can also supply expressions or text.
deps_code(quote(x + y + 123))
#> # A tibble: 2 × 2
#>   name  type   
#>   <chr> <chr>  
#> 1 x     globals
#> 2 y     globals
deps_code("x + y + 123")
#> # A tibble: 2 × 2
#>   name  type   
#>   <chr> <chr>  
#> 1 x     globals
#> 2 y     globals
```
