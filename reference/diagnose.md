# Get diagnostic metadata on a target. **\[stable\]**

Diagnostics include errors, warnings, messages, runtimes, and other
context/metadata from when a target was built or an import was
processed. If your target's last build succeeded, then
`diagnose(your_target)` has the most current information from that
build. But if your target failed, then only
`diagnose(your_target)$error`, `diagnose(your_target)$warnings`, and
`diagnose(your_target)$messages` correspond to the failure, and all the
other metadata correspond to the last build that completed without an
error.

## Usage

``` r
diagnose(
  target = NULL,
  character_only = FALSE,
  path = NULL,
  search = NULL,
  cache = drake::drake_cache(path = path),
  verbose = 1L
)
```

## Arguments

- target:

  Name of the target of the error to get. Can be a symbol if
  `character_only` is `FALSE`, must be a character if `character_only`
  is `TRUE`.

- character_only:

  Logical, whether `target` should be treated as a character or a
  symbol. Just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html).

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- search:

  Deprecated.

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- verbose:

  Deprecated on 2019-09-11.

## Value

Either a character vector of target names or an object of class
`"error"`.

## See also

[`drake_failed()`](https://docs.ropensci.org/drake/reference/drake_failed.md),
[`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md),
[`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine side effects.", {
diagnose() # List all the targets with recorded error logs.
# Define a function doomed to failure.
f <- function() {
  stop("unusual error")
}
# Create a workflow plan doomed to failure.
bad_plan <- drake_plan(my_target = f())
# Running the project should generate an error
# when trying to build 'my_target'.
try(make(bad_plan), silent = FALSE)
drake_failed() # List the failed targets from the last make() (my_target).
# List targets that failed at one point or another
# over the course of the project (my_target).
# drake keeps all the error logs.
diagnose()
# Get the error log, an object of class "error".
error <- diagnose(my_target)$error # See also warnings and messages.
str(error) # See what's inside the error log.
error$calls # View the traceback. (See the rlang::trace_back() function).
})
} # }
```
