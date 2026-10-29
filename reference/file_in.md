# Declare input files and directories. **\[stable\]**

`file_in()` marks individual files (and whole directories) that your
targets depend on.

## Usage

``` r
file_in(...)
```

## Arguments

- ...:

  Character vector, paths to files and directories. Use `.id_chr` to
  refer to the current target by name. `.id_chr` is not limited to use
  in `file_in()` and
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md).

## Value

A character vector of declared input file or directory paths.

## URLs

As of `drake` 7.4.0, `file_in()` and
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
have support for URLs. If the file name begins with "http://",
"https://", or "ftp://",
[`make()`](https://docs.ropensci.org/drake/reference/make.md) attempts
to check the ETag to see if the data changed from last time. If no ETag
can be found, `drake` simply uses the ETag from last
[`make()`](https://docs.ropensci.org/drake/reference/make.md) and
registers the file as unchanged (which prevents your workflow from
breaking if you lose internet access). If your `file_in()` URLs require
authentication, see the `curl_handles` argument of
[`make()`](https://docs.ropensci.org/drake/reference/make.md) and
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
to learn how to supply credentials.

## Keywords

[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
understands special keyword functions for your commands. With the
exception of
[`target()`](https://docs.ropensci.org/drake/reference/target.md), each
one is a proper function with its own help file.

- [`target()`](https://docs.ropensci.org/drake/reference/target.md):
  give the target more than just a command. Using
  [`target()`](https://docs.ropensci.org/drake/reference/target.md), you
  can apply a transformation (examples:
  `https://books.ropensci.org/drake/plans.html#large-plans`), \# nolint
  supply a trigger (`https://books.ropensci.org/drake/triggers.html`),
  \# nolint or set any number of custom columns.

- `file_in()`: declare an input file dependency.

- [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md):
  declare an output file to be produced when the target is built.

- [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md):
  declare a `knitr` file dependency such as an R Markdown (`*.Rmd`) or R
  LaTeX (`*.Rnw`) file.

- [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md):
  force `drake` to entirely ignore a piece of code: do not track it for
  changes and do not analyze it for dependencies.

- [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md):
  tell `drake` to not track the dependencies of a piece of code. `drake`
  still tracks the code itself for changes.

- [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md): Get
  the name of the current target.

- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md):
  get the environment where drake builds targets. Intended for advanced
  custom memory management.

## See also

[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md),
[`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md),
[`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
# The `file_out()` and `file_in()` functions
# just takes in strings and returns them.
file_out("summaries.txt")
# Their main purpose is to orchestrate your custom files
# in your workflow plan data frame.
plan <- drake_plan(
  out = write.csv(mtcars, file_out("mtcars.csv")),
  contents = read.csv(file_in("mtcars.csv"))
)
plan
# drake knows "\"mtcars.csv\"" is the first target
# and a dependency of `contents`. See for yourself:

make(plan)
file.exists("mtcars.csv")

# You may use `.id_chr` inside `file_out()` and `file_in()`
# to refer  to the current target. This works inside
# static `map()`, `combine()`, `split()`, and `cross()`.

plan <- drake::drake_plan(
  data = target(
    write.csv(data, file_out(paste0(.id_chr, ".csv"))),
    transform = map(data = c(airquality, mtcars))
  )
)
plan

# You can also work with entire directories this way.
# However, in `file_out("your_directory")`, the directory
# becomes an entire unit. Thus, `file_in("your_directory")`
# is more appropriate for subsequent steps than
# `file_in("your_directory/file_inside.txt")`.
plan <- drake_plan(
  out = {
    dir.create(file_out("dir"))
    write.csv(mtcars, "dir/mtcars.csv")
  },
  contents = read.csv(file.path(file_in("dir"), "mtcars.csv"))
)
plan

make(plan)
file.exists("dir/mtcars.csv")

# See the connections that the file relationships create:
if (requireNamespace("visNetwork", quietly = TRUE)) {
  vis_drake_graph(plan)
}
})
} # }
```
