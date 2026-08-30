# Cancel a target mid-build **\[stable\]**

Cancel a target mid-build. Upon cancellation, `drake` halts the current
target and moves to the next one. The target's previous value and
metadata, if they exist, remain in the cache.

## Usage

``` r
cancel(allow_missing = TRUE)
```

## Arguments

- allow_missing:

  Logical. If `FALSE`, `drake` will not cancel the target if it is
  missing from the cache (or if you removed the key with
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md)).

## Value

Nothing.

## See also

cancel_if

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("cancel()", {
f <- function(x) {
  cancel()
  Sys.sleep(2) # Does not run.
}
g <- function(x) f(x)
plan <- drake_plan(y = g(1))
make(plan)
# Does not exist.
# readd(y)
})
} # }
```
