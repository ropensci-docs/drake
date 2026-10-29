# Row-bind together drake plans **\[stable\]**

Combine drake plans together in a way that correctly fills in missing
entries.

## Usage

``` r
bind_plans(...)
```

## Arguments

- ...:

  Workflow plan data frames (see
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)).

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
# You might need to refresh your data regularly (see ?triggers).
download_plan <- drake_plan(
  data = target(
    command = download_data(),
    trigger = "always"
  )
)
# But if the data don't change, the analyses don't need to change.
analysis_plan <- drake_plan(
  usage = get_usage_metrics(data),
  topline = scrape_topline_table(data)
)
your_plan <- bind_plans(download_plan, analysis_plan)
your_plan
#> # A tibble: 3 × 3
#>   target  command                    trigger   
#>   <chr>   <expr_lst>                 <expr_lst>
#> 1 data    download_data()            "always"  
#> 2 usage   get_usage_metrics(data)    NA        
#> 3 topline scrape_topline_table(data) NA        
```
