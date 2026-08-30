# List the targets and imports that are reproducibly tracked. **\[stable\]**

List all the spec in your project's dependency network.

## Usage

``` r
tracked(config)
```

## Arguments

- config:

  An output list from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

## Value

A character vector with the names of reproducibly-tracked targets.

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Load the canonical example for drake.
# List all the targets/imports that are reproducibly tracked.
config <- drake_config(my_plan)
tracked(config)
}
})
} # }
```
