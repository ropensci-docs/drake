# Configure the hash algorithms, etc. of a drake cache. **\[deprecated\]**

The purpose of this function is to prepare the cache to be called from
[`make()`](https://docs.ropensci.org/drake/reference/make.md). `drake`
only uses a single hash algorithm now, so we no longer need this
configuration step.

## Usage

``` r
configure_cache(
  cache = drake::get_cache(verbose = verbose),
  short_hash_algo = drake::default_short_hash_algo(cache = cache),
  long_hash_algo = drake::default_long_hash_algo(cache = cache),
  log_progress = FALSE,
  overwrite_hash_algos = FALSE,
  verbose = 1L,
  jobs = 1,
  init_common_values = FALSE
)
```

## Arguments

- cache:

  Cache to configure

- short_hash_algo:

  Short hash algorithm for drake. The short algorithm must be among
  [`available_hash_algos()`](https://docs.ropensci.org/drake/reference/available_hash_algos.md),
  which is just the collection of algorithms available to the `algo`
  argument in
  [`digest::digest()`](https://eddelbuettel.github.io/digest/man/digest.html).
  See
  [`default_short_hash_algo()`](https://docs.ropensci.org/drake/reference/default_short_hash_algo.md)
  for more.

- long_hash_algo:

  Long hash algorithm for drake. The long algorithm must be among
  [`available_hash_algos()`](https://docs.ropensci.org/drake/reference/available_hash_algos.md),
  which is just the collection of algorithms available to the `algo`
  argument in
  [`digest::digest()`](https://eddelbuettel.github.io/digest/man/digest.html).
  See
  [`default_long_hash_algo()`](https://docs.ropensci.org/drake/reference/default_long_hash_algo.md)
  for more.

- log_progress:

  Deprecated logical. Previously toggled whether to clear the recorded
  build progress if this cache was used for previous calls to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).

- overwrite_hash_algos:

  Logical, whether to try to overwrite the hash algorithms in the cache
  with any user-specified ones.

- verbose:

  Deprecated on 2019-09-11.

- jobs:

  Number of jobs for parallel processing

- init_common_values:

  Logical, whether to set the initial `drake` version in the cache and
  other common values. Not always a thread safe operation, so should
  only be `TRUE` on the main process

## Value

A drake/storr cache.

## Details

Deprecated on 2018-12-12.
