# Deprecated: clean the main example from `drake_example("main")` **\[deprecated\]**

This function deletes files. Use at your own risk. Destroys the
`.drake/` cache and the `report.Rmd` file in the current working
directory. Your working directory (`getcwd()`) must be the folder from
which you first ran
[`load_main_example()`](https://docs.ropensci.org/drake/reference/load_main_example.md)
and `make(my_plan)`.

## Usage

``` r
clean_main_example()
```

## Value

Nothing.

## Details

Deprecated 2018-12-31.
