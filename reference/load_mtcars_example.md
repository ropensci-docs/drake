# Load the mtcars example. **\[stable\]**

Is there an association between the weight and the fuel efficiency of
cars? To find out, we use the mtcars example from
`drake_example("mtcars")`. The mtcars dataset itself only has 32 rows,
so we generate two larger bootstrapped datasets and then analyze them
with regression models. Finally, we summarize the regression models to
see if there is an association.

## Usage

``` r
load_mtcars_example(
  envir = parent.frame(),
  report_file = NULL,
  overwrite = FALSE,
  force = FALSE
)
```

## Arguments

- envir:

  The environment to load the example into. Defaults to your workspace.
  For an insulated workspace, set
  `envir = new.env(parent = globalenv())`.

- report_file:

  Where to write the report file. Deprecated. In a future release, the
  report file will always be `report.Rmd` and will always be written to
  your working directory (current default).

- overwrite:

  Logical, whether to overwrite an existing file `report.Rmd`.

- force:

  Deprecated.

## Value

Nothing.

## Details

Use `drake_example("mtcars")` to get the code for the mtcars example.
This function also writes/overwrites the file, `report.Rmd`.

## See also

[`clean_mtcars_example()`](https://docs.ropensci.org/drake/reference/clean_mtcars_example.md)
[`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md)

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
