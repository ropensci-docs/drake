# Download the files of an example `drake` project. **\[stable\]**

The `drake_example()` function downloads a folder from
`https://github.com/wlandau/drake-examples`. By default, it creates a
new folder with the example name in your current working directory.
After the files are written, have a look at the enclosed `README` file.
Other instructions are available in the files at
`https://github.com/wlandau/drake-examples`.

## Usage

``` r
drake_example(
  example = "main",
  to = getwd(),
  destination = NULL,
  overwrite = FALSE,
  quiet = TRUE
)
```

## Arguments

- example:

  Name of the example. The possible values are the names of the folders
  at `https://github.com/wlandau/drake-examples`.

- to:

  Character scalar, the folder containing the code files for the
  example. passed to the `exdir` argument of
  [`utils::unzip()`](https://rdrr.io/r/utils/unzip.html).

- destination:

  Deprecated; use `to` instead.

- overwrite:

  Logical, whether to overwrite an existing folder with the same name as
  the drake example.

- quiet:

  Logical, passed to
  [`downloader::download()`](https://rdrr.io/pkg/downloader/man/download.html)
  and thus
  [`utils::download.file()`](https://rdrr.io/r/utils/download.file.html).
  Whether to download quietly or print progress.

## Value

`NULL`

## See also

[`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
if (requireNamespace("downloader")) {
drake_examples() # List all the drake examples.
# Sets up the same example from load_mtcars_example()
drake_example("mtcars")
# Sets up the SLURM example.
drake_example("slurm")
}
})
} # }
```
