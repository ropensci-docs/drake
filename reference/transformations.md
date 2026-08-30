# Transformations in `drake_plan()`. **\[stable\]**

In
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
you can define whole batches of targets with transformations such as
`map()`, `split()`, `cross()`, and `combine()`.

## Arguments

- ...:

  Grouping variables. New grouping variables must be supplied with their
  names and values, existing grouping variables can be given as symbols
  without any values assigned. For dynamic branching, the entries in
  `...` must be unnamed symbols with no values supplied, and they must
  be the names of targets.

- .data:

  A data frame of new grouping variables with grouping variable names as
  column names and values as elements.

- .names:

  Literal character vector of names for the targets. Must be the same
  length as the targets generated.

- .id:

  Symbol or vector of symbols naming grouping variables to incorporate
  into target names. Useful for creating short target names. Set
  `.id = FALSE` to use integer indices as target name suffixes.

- .tag_in:

  A symbol or vector of symbols. Tags assign targets to grouping
  variables. Use `.tag_in` to assign *untransformed* targets to grouping
  variables.

- .tag_out:

  Just like `.tag_in`, except that `.tag_out` assigns *transformed*
  targets to grouping variables.

- slice:

  Number of slices into which `split()` partitions the data.

- margin:

  Which margin to take the slices in `split()`. Same meaning as the
  `MARGIN` argument of [`apply()`](https://rdrr.io/r/base/apply.html).

- drop:

  Logical, whether to drop a dimension if its length is 1. Same meaning
  as `mtcars[, 1L, drop = TRUE]` versus `mtcars[, 1L, drop = TRUE]`.

- .by:

  Symbol or vector of symbols of grouping variables. `combine()`
  aggregates/groups targets by the grouping variables in `.by`. For
  dynamic branching, `.by` can only take one variable at a time, and
  that variable must be a vector. Ideally, it should take little space
  in memory.

- .trace:

  Symbol or vector of symbols for the dynamic trace. The dynamic trace
  allows you to keep track of the values of dynamic dependencies are
  associated with individual sub-targets. For `combine()`, `.trace` must
  either be empty or the same as the variable given for `.by`. See
  [`get_trace()`](https://docs.ropensci.org/drake/reference/get_trace.md)
  and
  [`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md)
  for examples and other details.

## Details

For details, see
`https://books.ropensci.org/drake/plans.html#large-plans`.

## Transformations

`drake` has special syntax for generating large plans. Your code will
look something like
`drake_plan(y = target(f(x), transform = map(x = c(1, 2, 3)))` You can
read about this interface at
`https://books.ropensci.org/drake/plans.html#large-plans`. \# nolint

## Static branching

In static branching, you define batches of targets based on information
you know in advance. Overall usage looks like
`drake_plan(<x> = target(<...>, transform = <call>)`, where

- `<x>` is the name of the target or group of targets.

- `<...>` is optional arguments to
  [`target()`](https://docs.ropensci.org/drake/reference/target.md).

- `<call>` is a call to one of the transformation functions.

Transformation function usage:

- `map(..., .data, .names, .id, .tag_in, .tag_out)`

- `split(..., slices, margin = 1L, drop = FALSE, .names, .tag_in, .tag_out)`
  \# nolint

- `cross(..., .data, .names, .id, .tag_in, .tag_out)`

- `combine(..., .by, .names, .id, .tag_in, .tag_out)`

## Dynamic branching

- `map(..., .trace)`

- `cross(..., .trace)`

- `group(..., .by, .trace)`

`map()` and `cross()` create dynamic sub-targets from the variables
supplied to the dots. As with static branching, the variables supplied
to `map()` must all have equal length. `group(f(data), .by = x)` makes
new dynamic sub-targets from `data`. Here, `data` can be either static
or dynamic. If `data` is dynamic, `group()` aggregates existing
sub-targets. If `data` is static, `group()` splits `data` into multiple
subsets based on the groupings from `.by`.

Differences from static branching:

- `...` must contain *unnamed* symbols with no values supplied, and they
  must be the names of targets.

- Arguments `.id`, `.tag_in`, and `.tag_out` no longer apply.

## Examples

``` r
# Static branching
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
if (requireNamespace("styler")) {
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
# Static splitting
plan <- drake_plan(
  analysis = target(
    analyze(data),
    transform = split(data, slices = 3L, margin = 1L, drop = FALSE)
  )
)
print(plan)
#> # A tibble: 3 × 2
#>   target     command                                                            
#>   <chr>      <expr_lst>                                                         
#> 1 analysis_1 analyze(drake_slice(data = data, slices = 3L, index = 1, margin = …
#> 2 analysis_2 analyze(drake_slice(data = data, slices = 3L, index = 2, margin = …
#> 3 analysis_3 analyze(drake_slice(data = data, slices = 3L, index = 3, margin = …
if (requireNamespace("styler", quietly = TRUE)) {
  print(drake_plan_source(plan))
}
#> drake_plan(
#>   analysis_1 = analyze(drake_slice(
#>     data = data, slices = 3L, index = 1, margin = 1L,
#>     drop = FALSE
#>   )),
#>   analysis_2 = analyze(drake_slice(
#>     data = data, slices = 3L, index = 2, margin = 1L,
#>     drop = FALSE
#>   )),
#>   analysis_3 = analyze(drake_slice(
#>     data = data, slices = 3L, index = 3, margin = 1L,
#>     drop = FALSE
#>   ))
#> )
# Static tags:
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
