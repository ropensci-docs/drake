# Transform a plan **\[stable\]**

Evaluate the
[`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
[`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
[`split()`](https://docs.ropensci.org/drake/reference/transformations.md)
and
[`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
operations in the `transform` column of a `drake` plan.

## Usage

``` r
transform_plan(
  plan,
  envir = parent.frame(),
  trace = FALSE,
  max_expand = NULL,
  tidy_eval = TRUE
)
```

## Arguments

- plan:

  A `drake` plan with a `transform` column

- envir:

  Environment for tidy evaluation.

- trace:

  Logical, whether to add columns to show what happens during target
  transformations.

- max_expand:

  Positive integer, optional. `max_expand` is the maximum number of
  targets to generate in each
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  transform. Useful if you have a massive plan and you want to test and
  visualize a strategic subset of targets before scaling up. Note: the
  `max_expand` argument of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  and `transform_plan()` is for static branching only. The dynamic
  branching `max_expand` is an argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

- tidy_eval:

  Logical, whether to use tidy evaluation (e.g. unquoting/`!!`) when
  resolving commands. Tidy evaluation in transformations is always
  turned on regardless of the value you supply to this argument.

## Details

`https://books.ropensci.org/drake/plans.html#large-plans` \# nolint

## See also

drake_plan, map, split, cross, combine

## Examples

``` r
plan1 <- drake_plan(
  y = target(
    f(x),
    transform = map(x = c(1, 2))
  ),
  transform = FALSE
)
plan2 <- drake_plan(
  z = target(
    g(y),
    transform = map(y, .id = x)
  ),
  transform = FALSE
)
plan <- bind_plans(plan1, plan2)
transform_plan(plan)
#> # A tibble: 4 × 2
#>   target command   
#>   <chr>  <expr_lst>
#> 1 y_1    f(1)      
#> 2 y_2    f(2)      
#> 3 z_1    g(y_1)    
#> 4 z_2    g(y_2)    
models <- c("glm", "hierarchical")
plan <- drake_plan(
  data = target(
    get_data(x),
    transform = map(x = c("simulated", "survey"))
  ),
  analysis = target(
    analyze_data(data, model),
    transform = cross(data, model = !!models, .id = c(x, model))
  ),
  summary = target(
    summarize_analysis(analysis),
    transform = map(analysis, .id = c(x, model))
  ),
  results = target(
    bind_rows(summary),
    transform = combine(summary, .by = data)
  )
)
plan
#> # A tibble: 12 × 2
#>    target                          command                                      
#>    <chr>                           <expr_lst>                                   
#>  1 analysis_simulated_glm          analyze_data(data_simulated, "glm")         …
#>  2 analysis_simulated_hierarchical analyze_data(data_simulated, "hierarchical")…
#>  3 analysis_survey_glm             analyze_data(data_survey, "glm")            …
#>  4 analysis_survey_hierarchical    analyze_data(data_survey, "hierarchical")   …
#>  5 data_simulated                  get_data("simulated")                       …
#>  6 data_survey                     get_data("survey")                          …
#>  7 results_data_simulated          bind_rows(summary_simulated_glm, summary_sim…
#>  8 results_data_survey             bind_rows(summary_survey_glm, summary_survey…
#>  9 summary_simulated_glm           summarize_analysis(analysis_simulated_glm)  …
#> 10 summary_simulated_hierarchical  summarize_analysis(analysis_simulated_hierar…
#> 11 summary_survey_glm              summarize_analysis(analysis_survey_glm)     …
#> 12 summary_survey_hierarchical     summarize_analysis(analysis_survey_hierarchi…
if (requireNamespace("styler", quietly = TRUE)) {
  print(drake_plan_source(plan))
}
#> drake_plan(
#>   analysis_simulated_glm = analyze_data(data_simulated, "glm"),
#>   analysis_simulated_hierarchical = analyze_data(data_simulated, "hierarchical"),
#>   analysis_survey_glm = analyze_data(data_survey, "glm"),
#>   analysis_survey_hierarchical = analyze_data(data_survey, "hierarchical"),
#>   data_simulated = get_data("simulated"),
#>   data_survey = get_data("survey"),
#>   results_data_simulated = bind_rows(summary_simulated_glm, summary_simulated_hierarchical),
#>   results_data_survey = bind_rows(summary_survey_glm, summary_survey_hierarchical),
#>   summary_simulated_glm = summarize_analysis(analysis_simulated_glm),
#>   summary_simulated_hierarchical = summarize_analysis(analysis_simulated_hierarchical),
#>   summary_survey_glm = summarize_analysis(analysis_survey_glm),
#>   summary_survey_hierarchical = summarize_analysis(analysis_survey_hierarchical)
#> )
# Tags:
drake_plan(
  x = target(
    command,
    transform = map(y = c(1, 2), .tag_in = from, .tag_out = c(to, out))
  ),
  trace = TRUE
)
#> # A tibble: 2 × 7
#>   target command    y     x     from  to    out  
#>   <chr>  <expr_lst> <chr> <chr> <chr> <chr> <chr>
#> 1 x_1    command    1     x_1   x     x_1   x_1  
#> 2 x_2    command    2     x_2   x     x_2   x_2  
plan <- drake_plan(
  survey = target(
    survey_data(x),
    transform = map(x = c(1, 2), .tag_in = source, .tag_out = dataset)
  ),
  download = target(
    download_data(),
    transform = map(y = c(5, 6), .tag_in = source, .tag_out = dataset)
  ),
  analysis = target(
    analyze(dataset),
    transform = map(dataset)
  ),
  results = target(
    bind_rows(analysis),
    transform = combine(analysis, .by = source)
  )
)
plan
#> # A tibble: 10 × 2
#>    target              command                                            
#>    <chr>               <expr_lst>                                         
#>  1 analysis_survey_1   analyze(survey_1)                                  
#>  2 analysis_survey_2   analyze(survey_2)                                  
#>  3 analysis_download_5 analyze(download_5)                                
#>  4 analysis_download_6 analyze(download_6)                                
#>  5 download_5          download_data()                                    
#>  6 download_6          download_data()                                    
#>  7 results_download    bind_rows(analysis_download_5, analysis_download_6)
#>  8 results_survey      bind_rows(analysis_survey_1, analysis_survey_2)    
#>  9 survey_1            survey_data(1)                                     
#> 10 survey_2            survey_data(2)                                     
if (requireNamespace("styler", quietly = TRUE)) {
  print(drake_plan_source(plan))
}
#> drake_plan(
#>   analysis_survey_1 = analyze(survey_1),
#>   analysis_survey_2 = analyze(survey_2),
#>   analysis_download_5 = analyze(download_5),
#>   analysis_download_6 = analyze(download_6),
#>   download_5 = download_data(),
#>   download_6 = download_data(),
#>   results_download = bind_rows(analysis_download_5, analysis_download_6),
#>   results_survey = bind_rows(analysis_survey_1, analysis_survey_2),
#>   survey_1 = survey_data(1),
#>   survey_2 = survey_data(2)
#> )
```
