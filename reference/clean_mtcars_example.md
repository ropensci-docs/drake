# Clean the mtcars example from `drake_example("mtcars")` **\[stable\]**

This function deletes files. Use at your own risk. Destroys the
`.drake/` cache and the `report.Rmd` file in the current working
directory. Your working directory (`getcwd()`) must be the folder from
which you first ran
[`load_mtcars_example()`](https://docs.ropensci.org/drake/reference/load_mtcars_example.md)
and `make(my_plan)`.

## Usage

``` r
clean_mtcars_example()
```

## Value

nothing

## See also

[`load_mtcars_example()`](https://docs.ropensci.org/drake/reference/load_mtcars_example.md),
[`clean()`](https://docs.ropensci.org/drake/reference/clean.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
# Populate your workspace and write 'report.Rmd'.
load_mtcars_example() # Get the code: drake_example("mtcars")
# Check the dependencies of an imported function.
deps_code(reg1)
# Check the dependencies of commands in the workflow plan.
deps_code(my_plan$command[1])
deps_code(my_plan$command[4])
# Plot the interactive network visualization of the workflow.
outdated(my_plan) # Which targets are out of date?
# Run the workflow to build all the targets in the plan.
make(my_plan)
outdated(my_plan) # Everything should be up to date.
# For the reg2() model on the small dataset,
# the p-value is so small that there may be an association
# between weight and fuel efficiency after all.
readd(coef_regression2_small)
# Clean up the example.
clean_mtcars_example()
}
})
} # }
```
