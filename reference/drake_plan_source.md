# Show the code required to produce a given `drake` plan **\[stable\]**

You supply a plan, and `drake_plan_source()` supplies code to generate
that plan. If you have the `prettycode` package, installed, you also get
nice syntax highlighting in the console when you print it.

## Usage

``` r
drake_plan_source(plan)
```

## Arguments

- plan:

  A workflow plan data frame (see
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md))

## Value

a character vector of lines of text. This text is a call to
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
that produces the plan you provide.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)

## Examples

``` r
plan <- drake::drake_plan(
  small_data = download_data("https://some_website.com"),
  large_data_raw = target(
    command = download_data("https://lots_of_data.com"),
    trigger = trigger(
      change = time_last_modified("https://lots_of_data.com"),
      command = FALSE,
      depend = FALSE
    ),
    timeout = 1e3
  )
)
print(plan)
#> # A tibble: 2 × 4
#>   target         command                                   trigger       timeout
#>   <chr>          <expr_lst>                                <expr_lst>      <dbl>
#> 1 small_data     download_data("https://some_website.com") NA          …      NA
#> 2 large_data_raw download_data("https://lots_of_data.com") trigger(chan…    1000
if (requireNamespace("styler", quietly = TRUE)) {
  source <- drake_plan_source(plan)
  print(source) # Install the prettycode package for syntax highlighting.
  file <- tempfile() # Path to an R script to contain the drake_plan() call.
  writeLines(source, file) # Save the code to an R script.
}
#> drake_plan(
#>   small_data = download_data("https://some_website.com"),
#>   large_data_raw = target(
#>     command = download_data("https://lots_of_data.com"),
#>     trigger = trigger(
#>       change = time_last_modified("https://lots_of_data.com"),
#>       command = FALSE,
#>       depend = FALSE
#>     ),
#>     timeout = 1000
#>   )
#> )
```
