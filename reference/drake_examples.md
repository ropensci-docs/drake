# List the names of all the drake examples. **\[stable\]**

You can find the code files of the examples at
`https://github.com/wlandau/drake-examples`. The `drake_examples()`
function downloads the list of examples from
`https://wlandau.github.io/drake-examples/examples.md`, so you need an
internet connection.

## Usage

``` r
drake_examples(quiet = TRUE)
```

## Arguments

- quiet:

  Logical, passed to
  [`downloader::download()`](https://rdrr.io/pkg/downloader/man/download.html)
  and thus
  [`utils::download.file()`](https://rdrr.io/r/utils/download.file.html).
  Whether to download quietly or print progress.

## Value

Names of all the drake examples.

## See also

[`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (requireNamespace("downloader")) {
drake_examples() # List all the drake examples.
# Sets up the example from load_mtcars_example()
drake_example("mtcars")
# Sets up the SLURM example.
drake_example("slurm")
}
})
} # }
```
