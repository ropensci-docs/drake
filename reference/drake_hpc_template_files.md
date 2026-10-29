# List the available example template files for deploying work to a cluster / job scheduler. **\[stable\]**

See the example files from
[`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md)
and
[`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)
for example usage.

## Usage

``` r
drake_hpc_template_files()
```

## Value

A character vector of example template files that you can write with
[`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md).

## See also

[`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md),
[`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md),
[`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md),
[`shell_file()`](https://docs.ropensci.org/drake/reference/shell_file.md)

## Examples

``` r
if (FALSE) { # \dontrun{
plan <- drake_plan(x = rnorm(1e7), y = rnorm(1e7))
# List the available template files.
drake_hpc_template_files()
# Write a SLURM template file.
out <- file.path(tempdir(), "slurm_batchtools.tmpl")
drake_hpc_template_file("slurm_batchtools.tmpl", to = tempdir())
cat(readLines(out), sep = "\n")
# library(future.batchtools) # nolint
# future::plan(batchtools_slurm, template = out) # nolint
# make(plan, parallelism = "future", jobs = 2) # nolint
} # }
```
