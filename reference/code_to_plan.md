# Turn an R script file or `knitr` / R Markdown report into a `drake` plan. **\[questioning\]**

`code_to_plan()`,
[`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md),
and
[`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md)
together illustrate the relationships between `drake` plans, R scripts,
and R Markdown documents.

## Usage

``` r
code_to_plan(path)
```

## Arguments

- path:

  A file path to an R script or `knitr` report.

## Details

This feature is easy to break, so there are some rules for your code
file:

1.  Stick to assigning a single expression to a single target at a time.
    For multi-line commands, please enclose the whole command in curly
    braces. Conversely, compound assignment is not supported (e.g.
    `target_1 <- target_2 <- target_3 <- get_data()`).

2.  Once you assign an expression to a variable, do not modify the
    variable any more. The target/command binding should be permanent.

3.  Keep it simple. Please use the assignment operators rather than
    [`assign()`](https://rdrr.io/r/base/assign.html) and similar
    functions.

## See also

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md),
[`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md),
[`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md)

## Examples

``` r
plan <- drake_plan(
  raw_data = read_excel(file_in("raw_data.xlsx")),
  data = raw_data,
  hist = create_plot(data),
  fit = lm(Ozone ~ Temp + Wind, data)
)
file <- tempfile()
# Turn the plan into an R script a the given file path.
plan_to_code(plan, file)
#> Loading required namespace: styler
# Here is what the script looks like.
cat(readLines(file), sep = "\n")
#> raw_data <- read_excel(file_in("raw_data.xlsx"))
#> data <- raw_data
#> fit <- lm(Ozone ~ Temp + Wind, data)
#> hist <- create_plot(data)
# Convert back to a drake plan.
code_to_plan(file)
#> # A tibble: 4 × 2
#>   target   command                             
#>   <chr>    <expr_lst>                          
#> 1 raw_data read_excel(file_in("raw_data.xlsx"))
#> 2 data     raw_data                            
#> 3 fit      lm(Ozone ~ Temp + Wind, data)       
#> 4 hist     create_plot(data)                   
```
