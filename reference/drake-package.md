# drake: A pipeline toolkit for reproducible computation at scale.

drake is a pipeline toolkit
(`https://github.com/pditommaso/awesome-pipeline`) and a scalable,
R-focused solution for reproducibility and high-performance computing.

## References

`https://github.com/ropensci/drake`

## Author

William Michael Landau <will.landau@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
library(drake)
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Build everything.
plot(my_plan) # fast call to vis_drake_graph()
make(my_plan) # Nothing is done because everything is already up to date.
reg2 = function(d) { # Change one of your functions.
  d$x3 = d$x^3
  lm(y ~ x3, data = d)
}
make(my_plan) # Only the pieces depending on reg2() get rebuilt.
# Write a flat text log file this time.
make(my_plan, cache_log_file = TRUE)
# Read/load from the cache.
readd(small)
loadd(large)
head(large)
}
# Dynamic branching
# Get the mean mpg for each cyl in the mtcars dataset.
plan <- drake_plan(
  raw = mtcars,
  group_index = raw$cyl,
  munged = target(raw[, c("mpg", "cyl")], dynamic = map(raw)),
  mean_mpg_by_cyl = target(
    data.frame(mpg = mean(munged$mpg), cyl = munged$cyl[1]),
    dynamic = group(munged, .by = group_index)
  )
)
make(plan)
readd(mean_mpg_by_cyl)
})
} # }
```
