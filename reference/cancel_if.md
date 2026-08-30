# Cancel a target mid-build under some condition **\[stable\]**

Cancel a target mid-build if some logical condition is met. Upon
cancellation, `drake` halts the current target and moves to the next
one. The target's previous value and metadata, if they exist, remain in
the cache.

## Usage

``` r
cancel_if(condition, allow_missing = TRUE)
```

## Arguments

- condition:

  Logical, whether to cancel the target.

- allow_missing:

  Logical. If `FALSE`, `drake` will not cancel the target if it is
  missing from the cache (or if you removed the key with
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md)).

## Value

Nothing.

## See also

cancel

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("cancel_if()", {
f <- function(x) {
  cancel_if(x > 1)
  Sys.sleep(2) # Does not run if x > 1.
}
g <- function(x) f(x)
plan <- drake_plan(y = g(2))
make(plan)
# Does not exist.
# readd(y)
})
} # }
```
