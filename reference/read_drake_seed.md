# Read the pseudo-random number generator seed of the project. **\[stable\]**

When a project is created with
[`make()`](https://docs.ropensci.org/drake/reference/make.md) or
[`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
the project's pseudo-random number generator seed is cached. Then,
unless the cache is destroyed, the seeds of all the targets will
deterministically depend on this one central seed. That way,
reproducibility is protected, even under randomness.

## Usage

``` r
read_drake_seed(path = NULL, search = NULL, cache = NULL, verbose = NULL)
```

## Arguments

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

An integer vector.

## Examples

``` r
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
cache <- storr::storr_environment() # Just for the examples.
my_plan <- drake_plan(
  target1 = sqrt(1234),
  target2 = sample.int(n = 12, size = 1) + target1
)
tmp <- sample.int(1) # Needed to get a .Random.seed, but not for drake.
digest::digest(.Random.seed) # Fingerprint of the current R session's seed.
make(my_plan, cache = cache) # Run the project, build the targets.
digest::digest(.Random.seed) # Your session's seed did not change.
# drake uses a hard-coded seed if you do not supply one.
read_drake_seed(cache = cache)
readd(target2, cache = cache) # Randomly-generated target data.
clean(target2, cache = cache) # Oops, I removed the data!
tmp <- sample.int(1) # Maybe the R session's seed also changed.
make(my_plan, cache = cache) # Rebuild target2.
# Same as before:
read_drake_seed(cache = cache)
readd(target2, cache = cache)
# You can also supply a seed.
# If your project already exists, it must agree with the project's
# preexisting seed (default: 0)
clean(target2, cache = cache)
make(my_plan, cache = cache, seed = 0)
read_drake_seed(cache = cache)
readd(target2, cache = cache)
# If you want to supply a different seed than 0,
# you need to destroy the cache and start over first.
clean(destroy = TRUE, cache = cache)
cache <- storr::storr_environment() # Just for the examples.
make(my_plan, cache = cache, seed = 1234)
read_drake_seed(cache = cache)
readd(target2, cache = cache)
})
} # }
```
