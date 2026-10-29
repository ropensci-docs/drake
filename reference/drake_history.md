# History and provenance **\[stable\]**

See the history and provenance of your targets: what you ran, when you
ran it, the function arguments you used, and how to get old data back.

## Usage

``` r
drake_history(cache = NULL, history = NULL, analyze = TRUE, verbose = NULL)
```

## Arguments

- cache:

  drake cache as created by
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  See also
  [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md).

- history:

  Logical, whether to record the build history of your targets. You can
  also supply a `txtq`, which is how `drake` records history. Must be
  `TRUE` for `drake_history()` to work later.

- analyze:

  Logical, whether to analyze
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  commands for arguments to function calls. Could be slow because this
  requires parsing and analyzing lots of R code.

- verbose:

  Deprecated on 2019-09-11.

## Value

A data frame of target history.

## Details

`drake_history()` returns a data frame with the following columns.

- `target`: the name of the target.

- `current`: logical, whether the row describes the data actually
  assigned to the target name in the cache, e.g. what you get with
  `loadd(target)` and `readd(target)`. Does **NOT** tell you if the
  target is up to date.

- `built`: when the target's value was stored in the cache. This is the
  true creation date of the target's value, not the recovery date from
  `make(recover = TRUE)`.

- `exists`: logical, whether the target's historical value still exists
  in the cache. Garbage collection via
  (`clean(garbage_collection = TRUE)` and `drake_cache()$gc()`) remove
  these historical values, but
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) under
  the default settings does not.

- `hash`: fingerprint of the target's historical value in the cache. If
  the value still exists, you can read it with
  `drake_cache()$get_value(hash)`.

- `command`: the
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  command executed to build the target.

- `seed`: random number generator seed.

- `runtime`: the time it took to execute the
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  command. Does not include overhead due to `drake`'s processing.

If `analyze` is `TRUE`, various other columns are included to show the
explicitly-named length-1 arguments to function calls in the commands.
See the "Provenance" section for more details.

## Provenance

If `analyze` is `TRUE`, `drake` scans your
[`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
commands for function arguments and mentions them in the history. A
function argument shows up if and only if: 1. It has length 1.  
2. It is atomic, i.e. a base type: logical, integer, real, complex,
character, or raw.  
3. It is explicitly named in the function call, For example, `x` is
detected as `1` in `fn(list(x = 1))` but not `f(list(1))`. The
exceptions are
[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
[`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md), and
[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md).
For example, `filename` is detected as `"my_file.csv"` in
`process_data(filename = file_in("my_file.csv"))`. NB: in
`process_data(filename = file_in("a", "b"))` `filename` is not detected
because the value must be atomic.  

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side-effects", {
if (requireNamespace("knitr", quietly = TRUE)) {
# First, let's iterate on a drake workflow.
load_mtcars_example()
make(my_plan, history = TRUE, verbose = 0L)
# Naturally, we'll make updates to our targets along the way.
reg2 <- function(d) {
  d$x2 <- d$x ^ 3
  lm(y ~ x2, data = d)
}
Sys.sleep(0.01)
make(my_plan, history = TRUE, verbose = 0L)
# The history is a data frame about all the recorded runs of your targets.
out <- drake_history(analyze = TRUE)
print(out)
# Let's use the history to recover the oldest version
# of our regression2_small target.
oldest_reg2_small <- max(which(out$target == "regression2_small"))
hash_oldest_reg2_small <- out[oldest_reg2_small, ]$hash
cache <- drake_cache()
cache$get_value(hash_oldest_reg2_small)
# If you run clean(), drake can still find all the targets.
clean(small)
drake_history()
# But if you run clean() with garbage collection,
# older versions of your targets may be gone.
clean(large, garbage_collection = TRUE)
drake_history()
invisible()
}
})
} # }
```
