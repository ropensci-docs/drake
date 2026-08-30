# Read a trace of a dynamic target. **\[stable\]**

Read a target's dynamic trace from the cache. Best used on its own
outside a `drake` plan.

## Usage

``` r
read_trace(
  trace,
  target,
  cache = drake::drake_cache(path = path),
  path = NULL,
  character_only = FALSE
)
```

## Arguments

- trace:

  Character, name of the trace you want to extract. Such trace names are
  declared in the `.trace` argument of
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  or
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md).

- target:

  Symbol or character, depending on the value of `character_only`.
  `target` is T=the name of a dynamic target with one or more traces
  defined using the `.trace` argument of dynamic
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  or
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md).

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

- character_only:

  Logical, whether `name` should be treated as a character or a symbol
  (just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html)).

## Value

The dynamic trace of one target in another: a vector of values from a
grouping variable.

## Details

In dynamic branching, the trace keeps track of how the sub-targets were
generated. It reminds us the values of grouping variables that go with
individual sub-targets.

## See also

[`get_trace()`](https://docs.ropensci.org/drake/reference/get_trace.md),
[`subtargets()`](https://docs.ropensci.org/drake/reference/subtargets.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("demonstrate dynamic trace", {
plan <- drake_plan(
  w = LETTERS[seq_len(3)],
  x = letters[seq_len(2)],

  # The first trace lets us see the values of w
  # that go with the sub-targets of y.
  y = target(paste0(w, x), dynamic = cross(w, x, .trace = w)),

  # We can use the trace as a grouping variable for the next
  # group().
  w_tr = read_trace("w", y),

  # Now, we use the trace again to keep track of the
  # values of w corresponding to the sub-targets of z.
  z = target(
    paste0(y, collapse = "-"),
    dynamic = group(y, .by = w_tr, .trace = w_tr)
  )
)
make(plan)

# We can read the trace outside make().
# That way, we know which values of `w` correspond
# to the sub-targets of `y`.
readd(y)
read_trace("w", y)

# And we know which values of `w_tr` (and thus `w`)
# match up with the sub-targets of `y`.
readd(z)
read_trace("w_tr", z)
})
} # }
```
