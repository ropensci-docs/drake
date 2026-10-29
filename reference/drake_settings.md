# `drake_settings` helper

List of class `drake_settings`.

## Usage

``` r
drake_settings(
  cache_log_file = NULL,
  curl_handles = list(),
  garbage_collection = FALSE,
  jobs = 1L,
  jobs_preprocess = 1L,
  keep_going = TRUE,
  lazy_load = "eager",
  lib_loc = character(0),
  lock_cache = TRUE,
  lock_envir = TRUE,
  log_build_times = TRUE,
  log_progress = TRUE,
  memory_strategy = "speed",
  parallelism = "loop",
  recover = TRUE,
  recoverable = TRUE,
  seed = 0L,
  session_info = TRUE,
  skip_imports = FALSE,
  skip_safety_checks = FALSE,
  skip_targets = FALSE,
  sleep = function(i) 0.01,
  template = list(),
  log_worker = FALSE
)
```

## Value

A `drake_settings` object.

## Examples

``` r
if (FALSE) { # stronger than roxygen dontrun
drake_settings()
}
```
