# Show how a target/import was produced. **\[stable\]**

Show the command that produced a target or indicate that the object or
file was imported.

## Usage

``` r
show_source(target, config, character_only = FALSE)
```

## Arguments

- target:

  Symbol denoting the target or import or a character vector if
  character_only is `TRUE`.

- config:

  A
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  list.

- character_only:

  Logical, whether to interpret `target` as a symbol (`FALSE`) or
  character vector (`TRUE`).

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
plan <- drake_plan(x = sample.int(15))
cache <- storr::storr_environment() # custom in-memory cache
make(plan, cache = cache)
config <- drake_config(plan, cache = cache, history = FALSE)
show_source(x, config)
})
} # }
```
