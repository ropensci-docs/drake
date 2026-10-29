# List sub-targets **\[stable\]**

List the sub-targets of a dynamic target.

## Usage

``` r
subtargets(
  target = NULL,
  character_only = FALSE,
  cache = drake::drake_cache(path = path),
  path = NULL
)
```

## Arguments

- target:

  Character string or symbol, depending on `character_only`. Name of a
  dynamic target.

- character_only:

  Logical, whether `target` should be treated as a character or a
  symbol. Just like `character.only` in
  [`library()`](https://rdrr.io/r/base/library.html).

- cache:

  drake cache. See
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md).
  If supplied, `path` is ignored.

- path:

  Path to a `drake` cache (usually a hidden `.drake/` folder) or `NULL`.

## Value

Character vector of sub-target names

## See also

[`get_trace()`](https://docs.ropensci.org/drake/reference/get_trace.md),
[`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("dynamic branching", {
plan <- drake_plan(
  w = c("a", "a", "b", "b"),
  x = seq_len(4),
  y = target(x + 1, dynamic = map(x)),
  z = target(sum(x) + sum(y), dynamic = group(x, y, .by = w))
)
make(plan)
subtargets(y)
subtargets(z)
readd(x)
readd(y)
readd(z)
})
} # }
```
