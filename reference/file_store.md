# Show a file's encoded representation in the cache **\[stable\]**

This function simply wraps literal double quotes around the argument `x`
so `drake` knows it is the name of a file. Use when you are calling
functions like
[`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md):
for example, `deps_code(file_store("report.md"))`. See the examples for
details. Internally, `drake` wraps the names of file targets/imports
inside literal double quotes to avoid confusion between files and
generic R objects.

## Usage

``` r
file_store(x)
```

## Arguments

- x:

  Character string to be turned into a filename understandable by drake
  (i.e., a string with literal single quotes on both ends).

## Value

A single-quoted character string: i.e., a filename understandable by
drake.

## Examples

``` r
# Wraps the string in single quotes.
file_store("my_file.rds") # "'my_file.rds'"
#> [1] "p-NV4V6ZTJNRSS44TEOM"
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
if (suppressWarnings(require("knitr"))) {
load_mtcars_example() # Get the code with drake_example("mtcars").
make(my_plan) # Run the workflow to build the targets
list.files() # Should include input "report.Rmd" and output "report.md".
head(readd(small)) # You can use symbols for ordinary objects.
# But if you want to read cached info on files, use `file_store()`.
readd(file_store("report.md"), character_only = TRUE) # File fingerprint.
deps_code(file_store("report.Rmd"))
config <- drake_config(my_plan)
deps_profile(
  file_store("report.Rmd"),
  plan = my_plan,
  character_only = TRUE
)
}
})
} # }
```
