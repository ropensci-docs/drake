# Get a template file for execution on a cluster. **\[deprecated\]**

Deprecated. Use
[`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md)
instead.

## Usage

``` r
drake_batchtools_tmpl_file(
  example = drake::drake_hpc_template_files(),
  to = getwd(),
  overwrite = FALSE
)
```

## Arguments

- example:

  Name of template file.

- to:

  Character vector, where to write the file.

- overwrite:

  Logical, whether to overwrite an existing file of the same name.

## Details

Deprecated on 2018-06-27.
