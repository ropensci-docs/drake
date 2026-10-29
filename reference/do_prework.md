# Do the prework in the `prework` argument to [`make()`](https://docs.ropensci.org/drake/reference/make.md). **\[stable\]**

For internal use only. The only reason this function is exported is to
set up parallel socket (PSOCK) clusters without too much fuss.

## Usage

``` r
do_prework(config, verbose_packages)
```

## Arguments

- config:

  A configured workflow from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

- verbose_packages:

  logical, whether to print package startup messages

## Value

Inivisibly returns `NULL`.

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
# Create a main internal configuration list with prework.
con <- drake_config(my_plan, prework = c("library(knitr)", "x <- 1"))
# Do the prework. Usually done at the beginning of `make()`,
# and for distributed computing backends like "future_lapply",
# right before each target is built.
do_prework(config = con, verbose_packages = TRUE)
# The `eval` element is the environment where the prework
# and the commands in your workflow plan data frame are executed.
identical(con$eval$x, 1) # Should be TRUE.
}
})
} # }
```
