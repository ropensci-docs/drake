# Turn a script into a function. **\[stable\]**

`code_to_function()` is a quick (and very dirty) way to retrofit drake
to an existing script-based project. It parses individual `\*.R/\*.RMD`
files into functions so they can be added into the drake workflow.

## Usage

``` r
code_to_function(path, envir = parent.frame())
```

## Arguments

- path:

  Character vector, path to script.

- envir:

  Environment of the created function.

## Value

A function to be input into the drake plan

## Details

Most data science workflows consist of imperative scripts. `drake`, on
the other hand, assumes you write *functions*. `code_to_function()`
allows for pre-existing workflows to incorporate drake as a workflow
management tool seamlessly for cases where re-factoring is unfeasible.
So drake can monitor dependencies, the targets are passed as arguments
of the dependent functions.

## See also

[`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md),
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md),
[`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md),
[`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md),
[`code_to_plan()`](https://docs.ropensci.org/drake/reference/code_to_plan.md),
[`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md),
[`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
if (requireNamespace("ggplot2", quietly = TRUE)) {
# The `code_to_function()` function creates a function that makes it
# available for drake to process as part of the workflow.
# The main purpose is to allow pre-existing workflows to incorporate drake
# into the workflow seamlessly for cases where re-factoring is unfeasible.
#

script1 <- tempfile()
script2 <- tempfile()
script3 <- tempfile()
script4 <- tempfile()

writeLines(c(
  "data <- mtcars",
  "data$make <- do.call('c',",
  "lapply(strsplit(rownames(data), split=\" \"), `[`, 1))",
  "saveRDS(data, \"mtcars_alt.RDS\")"
 ),
  script1
)

writeLines(c(
  "data <- readRDS(\"mtcars_alt.RDS\")",
  "mtcars_lm <- lm(mpg~cyl+disp+vs+gear+make,data=data)",
  "saveRDS(mtcars_lm, \"mtcars_lm.RDS\")"
  ),
  script2
)
writeLines(c(
  "mtcars_lm <- readRDS(\"mtcars_lm.RDS\")",
  "lm_summary <- summary(mtcars_lm)",
  "saveRDS(lm_summary, \"mtcars_lm_summary.RDS\")"
  ),
  script3
)
writeLines(c(
  "data<-readRDS(\"mtcars_alt.RDS\")",
  "gg <- ggplot2::ggplot(data)+",
  "ggplot2::geom_point(ggplot2::aes(",
  "x=disp, y=mpg, shape=as.factor(vs), color=make))",
  "ggplot2::ggsave(\"mtcars_plot.png\", gg)"
 ),
  script4
)


do_munge <- code_to_function(script1)
do_analysis <- code_to_function(script2)
do_summarize <- code_to_function(script3)
do_vis <- code_to_function(script4)

plan <- drake_plan(
  munged   = do_munge(),
  analysis = do_analysis(munged),
  summary  = do_summarize(analysis),
  plot     = do_vis(munged)
 )

plan
# drake knows  "script1" is the first script to be evaluated and ran,
# because it has no dependencies on other code and a dependency of
# `analysis`. See for yourself:

make(plan)

# See the connections that the sourced scripts create:
if (requireNamespace("visNetwork", quietly = TRUE)) {
  vis_drake_graph(plan)
}
}
})
} # }
```
