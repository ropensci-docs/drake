# Make a new `drake` cache. **\[stable\]**

Uses the
[`storr::storr_rds()`](https://richfitz.github.io/storr/reference/storr_rds.html)
function from the `storr` package.

## Usage

``` r
new_cache(
  path = NULL,
  verbose = NULL,
  type = NULL,
  hash_algorithm = NULL,
  short_hash_algo = NULL,
  long_hash_algo = NULL,
  ...,
  console_log_file = NULL
)
```

## Arguments

- path:

  File path to the cache if the cache is a file system cache.

- verbose:

  Deprecated on 2019-09-11.

- type:

  Deprecated argument. Once stood for cache type. Use `storr` to
  customize your caches instead.

- hash_algorithm:

  Name of a hash algorithm to use. See the `algo` argument of the
  `digest` package for your options.

- short_hash_algo:

  Deprecated on 2018-12-12. Use `hash_algorithm` instead.

- long_hash_algo:

  Deprecated on 2018-12-12. Use `hash_algorithm` instead.

- ...:

  other arguments to the cache constructor.

- console_log_file:

  Deprecated on 2019-09-11.

## Value

A newly created drake cache as a storr object.

## See also

[`make()`](https://docs.ropensci.org/drake/reference/make.md)

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("Quarantine new_cache() side effects.", {
clean(destroy = TRUE) # Should not be necessary.
unlink("not_hidden", recursive = TRUE) # Should not be necessary.
cache1 <- new_cache() # Creates a new hidden '.drake' folder.
cache2 <- new_cache(path = "not_hidden", hash_algorithm = "md5")
clean(destroy = TRUE, cache = cache2)
})
} # }
```
