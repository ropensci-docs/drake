# The default cache of a `drake` project. **\[deprecated\]**

Use
[`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md)
instead.

## Usage

``` r
get_cache(
  path = getwd(),
  search = TRUE,
  verbose = 1L,
  force = FALSE,
  fetch_cache = NULL,
  console_log_file = NULL
)
```

## Arguments

- path:

  Character, either the root file path of a `drake` project or a folder
  containing the root (top-level working directory where you plan to
  call [`make()`](https://docs.ropensci.org/drake/reference/make.md)).
  If this is too confusing, feel free to just use
  [`storr::storr_rds()`](https://richfitz.github.io/storr/reference/storr_rds.html)
  to get the cache. If `search = FALSE`, `path` must be the root. If
  `search = TRUE`, you can specify any subdirectory of the project.
  Let's say `"/home/you/my_project"` is the root. The following are
  equivalent and correct:

  - `get_cache(path = "/home/you/my_project", search = FALSE)`

  - `get_cache(path = "/home/you/my_project", search = TRUE)`

  - `get_cache(path = "/home/you/my_project/subdir/x", search = TRUE)`

  - `get_cache(path = "/home/you/my_project/.drake", search = TRUE)`

  - `get_cache(path = "/home/you/my_project/.drake/keys", search = TRUE)`

- search:

  Deprecated.

- verbose:

  Deprecated on 2019-09-11.

- force:

  Deprecated.

- fetch_cache:

  Deprecated.

- console_log_file:

  Deprecated in favor of `log_make`.

## Details

Deprecated on 2019-05-25.
