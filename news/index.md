# Changelog

## Version 7.13.11

CRAN release: 2024-12-04

- Compatibility with `igraph` \>= 2.1.2.

## Version 7.13.10

CRAN release: 2024-05-15

- Remove environment locking, c.f.
  <https://github.com/r-lib/rlang/issues/1705>.
- Export S3 methods.
- Avoid `memo_expr()` because it causes errors on R-devel.

## Version 7.13.9

CRAN release: 2024-03-04

- Avoid [`is.R()`](https://rdrr.io/r/base/base-defunct.html).

## Version 7.13.8

CRAN release: 2023-11-06

- Fix CRAN note.

## Version 7.13.7

- Fix test for CRAN.

## Version 7.13.6

CRAN release: 2023-10-17

- Migrate to the new interface in `clustermq` 0.9.0
  ([@mschubert](https://github.com/mschubert)).

## Version 7.13.5

CRAN release: 2023-03-24

- Always pass a character vector to
  [`rm()`](https://rdrr.io/r/base/rm.html) and
  [`remove()`](https://rdrr.io/r/base/rm.html).

## Version 7.13.4

CRAN release: 2022-08-19

- Fix HTML documentation files.

## Version 7.13.3

CRAN release: 2021-09-21

- Improve error messages from static code analysis of malformed code
  ([\#1371](https://github.com/ropensci/drake/issues/1371),
  [@billdenney](https://github.com/billdenney)).
- Handle invalid language objects in commands
  ([\#1372](https://github.com/ropensci/drake/issues/1372),
  [@gorgitko](https://github.com/gorgitko)).
- Do not lock namespaces
  ([\#1373](https://github.com/ropensci/drake/issues/1373),
  [@gorgitko](https://github.com/gorgitko)).
- Compatibility with `rlang` PR 1255.

## Version 7.13.2

CRAN release: 2021-04-22

- Update SLURM `batchtools` template file can be brewed
  ([\#1359](https://github.com/ropensci/drake/issues/1359),
  [@pat-s](https://github.com/pat-s)).
- Change start-up message to tip about `targets`.

## Version 7.13.1

CRAN release: 2021-02-03

- Add files `NOTICE` and `inst/NOTICE` to more explicitly credit code
  included from other open source projects. (Previously `drake` just had
  comments in the source with links to the various projects.)

## Version 7.13.0

CRAN release: 2021-01-04

### Bug fixes

- Avoid checking printed output in test of testing infrastructure.
- Use `dsl_sym()` instead of
  [`as.symbol()`](https://rdrr.io/r/base/name.html) when constructing
  commands for
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  ([\#1340](https://github.com/ropensci/drake/issues/1340),
  [@vkehayas](https://github.com/vkehayas)).

### New features

- Add a new `level_separation` argument to
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md)
  to control the aspect ratio of `visNetwork` graphs
  ([\#1303](https://github.com/ropensci/drake/issues/1303),
  [@matthewstrasiotto](https://github.com/matthewstrasiotto),
  [@matthiasgomolka](https://github.com/matthiasgomolka),
  [@robitalec](https://github.com/robitalec)).

## Version 7.12.7

CRAN release: 2020-10-27

### Enhancements

- Deprecate `caching = "master"` in favor of `caching = "main"`.
- Improve the error message when a valid plan is not supplied
  ([\#1334](https://github.com/ropensci/drake/issues/1334),
  [@robitalec](https://github.com/robitalec)).

## Version 7.12.6

CRAN release: 2020-10-10

### Bug fixes

- Fix defunct functions error message when using namespace
  ([\#1310](https://github.com/ropensci/drake/issues/1310),
  [@malcolmbarrett](https://github.com/malcolmbarrett)).
- Preserve names of list elements in `.data` in DSL
  ([\#1323](https://github.com/ropensci/drake/issues/1323),
  [@shirdekel](https://github.com/shirdekel)).
- Use [`identical()`](https://rdrr.io/r/base/identical.html) to compare
  file hashes ([\#1324](https://github.com/ropensci/drake/issues/1324),
  [@shirdekel](https://github.com/shirdekel)).
- Set `seed = TRUE` in
  [`future::future()`](https://future.futureverse.org/reference/future.html).
- Manually relay warnings when `parallelism = "clustermq"` and
  `caching = "worker"`
  ([@richardbayes](https://github.com/richardbayes)).

### Enhancements

- Make logs more machine-readable by sanitizing messages and preventing
  race conditions
  ([\#1331](https://github.com/ropensci/drake/issues/1331),
  [@Plebejer](https://github.com/Plebejer)).

## Version 7.12.5

CRAN release: 2020-08-26

### Bug fixes

- Sanitize empty symbols in language columns
  ([\#1299](https://github.com/ropensci/drake/issues/1299),
  [@odaniel1](https://github.com/odaniel1)).
- Handle cases where [`NROW()`](https://rdrr.io/r/base/nrow.html) throws
  an error ([\#1300](https://github.com/ropensci/drake/issues/1300),
  `julian-tagell` on Stack Overflow).
- Prohibit dynamic branching over non-branching dynamic files
  ([\#1302](https://github.com/ropensci/drake/issues/1302),
  [@djbirke](https://github.com/djbirke)).

### Enhancements

- Transition to updated `lifecycle` that does not require badges to be
  in `man/figures`.
- Improve error message for empty dynamic grouping variables
  ([\#1308](https://github.com/ropensci/drake/issues/1308),
  [@saadaslam](https://github.com/saadaslam)).
- Expose the `log_worker` argument of
  [`clustermq::workers()`](https://mschubert.github.io/clustermq/reference/workers.html)
  to [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  ([\#1305](https://github.com/ropensci/drake/issues/1305),
  [@billdenney](https://github.com/billdenney),
  [@mschubert](https://github.com/mschubert)).
- Set `as.is` to `TRUE` in
  [`utils::type.convert()`](https://rdrr.io/r/utils/type.convert.html)
  ([\#1309](https://github.com/ropensci/drake/issues/1309),
  [@bbolker](https://github.com/bbolker)).

## Version 7.12.4

CRAN release: 2020-06-29

- Fix a CRAN warning about docs.

## Version 7.12.3

### Bug fixes

- [`cached_planned()`](https://docs.ropensci.org/drake/reference/cached_planned.md)
  and
  [`cached_unplanned()`](https://docs.ropensci.org/drake/reference/cached_unplanned.md)
  now work with non-standard cache locations
  ([\#1268](https://github.com/ropensci/drake/issues/1268),
  [@Plebejer](https://github.com/Plebejer)).
- Set `use_cache` to `FALSE` more often
  ([\#1257](https://github.com/ropensci/drake/issues/1257),
  [@Plebejer](https://github.com/Plebejer)).
- Use namespaced function calls in mtcars example instead of loading
  packages.
- Replace the `iris` dataset with the `airquality` dataset in all
  documentation, examples, and tests
  ([\#1271](https://github.com/ropensci/drake/issues/1271)).
- Assign functions created with
  [`code_to_function()`](https://docs.ropensci.org/drake/reference/code_to_function.md)
  to the proper environment
  ([\#1275](https://github.com/ropensci/drake/issues/1275),
  [@robitalec](https://github.com/robitalec)).
- Store tracebacks as character vectors and restrict the contents of
  error objects to try to prevent accidental storage of large data from
  the environment
  ([\#1276](https://github.com/ropensci/drake/issues/1276),
  [@billdenney](https://github.com/billdenney)).
- Strongly depend on `tidyselect`
  ([\#1274](https://github.com/ropensci/drake/issues/1274),
  [@dernst](https://github.com/dernst)).
- Avoid `txtq` lockfiles
  ([\#1232](https://github.com/ropensci/drake/issues/1232),
  [\#1239](https://github.com/ropensci/drake/issues/1239),
  [\#1280](https://github.com/ropensci/drake/issues/1280),
  [@danwwilson](https://github.com/danwwilson),
  [@pydupont](https://github.com/pydupont),
  [@mattwarkentin](https://github.com/mattwarkentin)).

### New features

- Add a new
  [`drake_script()`](https://docs.ropensci.org/drake/reference/drake_script.md)
  function to write `_drake.R` files for
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md)
  ([\#1282](https://github.com/ropensci/drake/issues/1282)).

### Enhancements

- Deprecate
  [`expose_imports()`](https://docs.ropensci.org/drake/reference/expose_imports.md)
  in favor of `make(envir = getNamespace("yourPackage")`
  ([\#1286](https://github.com/ropensci/drake/issues/1286),
  [@mvarewyck](https://github.com/mvarewyck)).
- Suppress the message recommending
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) if
  `getOption("drake_r_make_message")` is `FALSE`
  ([\#1238](https://github.com/ropensci/drake/issues/1238),
  [@januz](https://github.com/januz)).
- Improve the appearance of the `visNetwork` graph by using the
  hierarchical layout with
  `visEdges(smooth = list(type = "cubicBezier", forceDirection = TRUE))`
  ([\#1289](https://github.com/ropensci/drake/issues/1289),
  [@mstr3336](https://github.com/mstr3336)).

## Version 7.12.2

CRAN release: 2020-06-02

### Bug fixes

- Invalidate old sub-targets when finalizing a dynamic target
  ([@richardbayes](https://github.com/richardbayes)). Solves a major
  reproducibility bug
  ([\#1260](https://github.com/ropensci/drake/issues/1260)).
- Prevent `splice_inner()` from dropping formal arguments shared by
  [`c()`](https://rdrr.io/r/base/c.html)
  ([\#1262](https://github.com/ropensci/drake/issues/1262),
  [@bart1](https://github.com/bart1)).

## Version 7.12.1

CRAN release: 2020-05-14

### Bug fixes

- Repair `subtarget_hashes.cross()` for crosses on a single grouping
  variable.
- Repair dynamic
  [`group()`](https://docs.ropensci.org/drake/reference/transformations.md)
  used with specialized formats
  ([\#1236](https://github.com/ropensci/drake/issues/1236),
  [@adamaltmejd](https://github.com/adamaltmejd)).
- Enforce `tidyselect` \>= 1.0.0.

### New features

- Allow user-defined target names in static branching with the `.names`
  argument ([\#1240](https://github.com/ropensci/drake/issues/1240),
  [@maciejmotyka](https://github.com/maciejmotyka),
  [@januz](https://github.com/januz)).

### Enhancements

- Do not analyze dependencies of calls to
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  ([\#1237](https://github.com/ropensci/drake/issues/1237),
  [@januz](https://github.com/januz)).
- Error message for locked cache gives paste-able error message in
  Windows ([\#1243](https://github.com/ropensci/drake/issues/1243),
  [@billdenney](https://github.com/billdenney)).
- Prevent stack traces from accidentally storing large amounts of data
  ([\#1253](https://github.com/ropensci/drake/issues/1253),
  [@sclewis23](https://github.com/sclewis23)).

## Version 7.12.0

CRAN release: 2020-03-25

### Bug fixes

- **Ensure up-to-date sub-targets are skipped even if the dynamic parent
  does not get a chance to finalize
  ([\#1209](https://github.com/ropensci/drake/issues/1209),
  [\#1211](https://github.com/ropensci/drake/issues/1211),
  [@psadil](https://github.com/psadil),
  [@kendonB](https://github.com/kendonB)).**
- Restrict static transforms so they only use the upstream part of the
  plan ([\#1199](https://github.com/ropensci/drake/issues/1199),
  [\#1200](https://github.com/ropensci/drake/issues/1200),
  [@bart1](https://github.com/bart1)).
- Correctly match the names and values of dynamic
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  sub-targets ([\#1204](https://github.com/ropensci/drake/issues/1204),
  [@psadil](https://github.com/psadil)). Expansion order is the same,
  but names are correctly matched now.
- Stop trying to remove
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files in
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md), even
  when `garbage_collection` is `TRUE`
  ([\#521](https://github.com/ropensci/drake/issues/521),
  [@the-Hull](https://github.com/the-Hull)).
- Fix `keep_going = TRUE` for formatted targets
  ([\#1206](https://github.com/ropensci/drake/issues/1206)).
- Use the correct variable names in logger helper (`progress_bar`
  instead of `progress`) so that `drake` works without the `progress`
  package ([\#1208](https://github.com/ropensci/drake/issues/1208),
  [@mbaccou](https://github.com/mbaccou)).
- Avoid conflict between formats and upstream dynamic targets
  ([\#1210](https://github.com/ropensci/drake/issues/1210),
  [@psadil](https://github.com/psadil)).
- Always compute trigger metadata up front because recovery keys need
  it.
- Deprecate and remove hasty mode and custom parallel backends
  ([\#1222](https://github.com/ropensci/drake/issues/1222)).
- Compartmentalize fixed runtime parameters in `config$settings`
  ([\#965](https://github.com/ropensci/drake/issues/965)).

### New features

- Add new functions
  [`drake_done()`](https://docs.ropensci.org/drake/reference/drake_done.md)
  and
  [`drake_cancelled()`](https://docs.ropensci.org/drake/reference/drake_cancelled.md)
  ([\#1205](https://github.com/ropensci/drake/issues/1205)).

### Speedups

- Avoid reading build times of dynamic sub-targets in
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  ([\#1207](https://github.com/ropensci/drake/issues/1207)).

### Enhancements

- Show an empty progress bar just before targets start to build when
  `verbose` is `2`
  ([\#1203](https://github.com/ropensci/drake/issues/1203),
  [@kendonB](https://github.com/kendonB)).
- Deprecate the `jobs` argument of
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md).
- Show an informative error message for empty dynamic grouping variables
  ([\#1212](https://github.com/ropensci/drake/issues/1212),
  [@kendonB](https://github.com/kendonB)).
- Throw error messages if users supply dynamic targets to
  [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)
  or
  [`drake_debug()`](https://docs.ropensci.org/drake/reference/drake_debug.md)
  ([\#1214](https://github.com/ropensci/drake/issues/1214),
  [@kendonB](https://github.com/kendonB)).
- Log the sub-target name and index of the failing sub-target in the
  metadata of the sub-target and its parent
  ([\#1214](https://github.com/ropensci/drake/issues/1214),
  [@kendonB](https://github.com/kendonB)).
- Shorten the call stack in error metadata.
- Deprecate and remove custom schedulers
  ([\#1222](https://github.com/ropensci/drake/issues/1222)).
- Deprecate `hasty_build`
  ([\#1222](https://github.com/ropensci/drake/issues/1222)).
- Migrate constant runtime parameters to `config$settings`
  ([\#965](https://github.com/ropensci/drake/issues/965)).
- Warn the user if
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)/[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)/[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  files are not literal strings
  ([\#1229](https://github.com/ropensci/drake/issues/1229)).
- Prohibit
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  and
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  in imported functions
  ([\#1229](https://github.com/ropensci/drake/issues/1229)).
- Prohibit
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  in dynamic branching
  ([\#1229](https://github.com/ropensci/drake/issues/1229)).
- Improve the help file of
  [`target()`](https://docs.ropensci.org/drake/reference/target.md).
- Deprecate and rename progress functions to avoid potential name
  conflicts
  ([`progress()`](https://docs.ropensci.org/drake/reference/progress.md)
  =\>
  [`drake_progress()`](https://docs.ropensci.org/drake/reference/drake_progress.md),
  [`running()`](https://docs.ropensci.org/drake/reference/running.md)
  =\>
  [`drake_running()`](https://docs.ropensci.org/drake/reference/drake_running.md),
  [`failed()`](https://docs.ropensci.org/drake/reference/failed.md) =\>
  [`drake_failed()`](https://docs.ropensci.org/drake/reference/drake_failed.md))
  ([\#1205](https://github.com/ropensci/drake/issues/1205)).

## Version 7.11.0

CRAN release: 2020-03-01

### Bug fixes

- Sanitize internal S3 classes for target storage
  ([\#1159](https://github.com/ropensci/drake/issues/1159),
  [@rsangole](https://github.com/rsangole)).
- Bump `digest` version to require 0.6.21
  ([\#1166](https://github.com/ropensci/drake/issues/1166),
  [@boshek](https://github.com/boshek))
- Actually store output file sizes in metadata.
- Use the `depend` trigger to toggle invalidation from dynamic-only
  dependencies, including the `max_expand` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Repair `session_info` argument parsing (and reduce calls to
  [`utils::sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) in
  tests).
- Ensure compatibility with `tibble` 3.0.0.

### New features

- Allow dynamic files with `target(format = "file")`
  ([\#1168](https://github.com/ropensci/drake/issues/1168),
  [\#1127](https://github.com/ropensci/drake/issues/1127)).
- Implement dynamic `max_expand` on a target-by-target basis via
  [`target()`](https://docs.ropensci.org/drake/reference/target.md)
  ([\#1175](https://github.com/ropensci/drake/issues/1175),
  [@kendonB](https://github.com/kendonB)).

### Enhancements

- Assert dependencies of formats at the very beginning of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), not in
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  ([\#1156](https://github.com/ropensci/drake/issues/1156)).
- In `make(verbose = 2)`, remove the spinner and use a progress bar to
  track how many targets are done so far.
- Reduce logging of utility functions.
- Improve the aesthetics of console messages using `cli` (optional
  package).
- Deprecate `console_log_file` in favor of `log_make` as an argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Immediately relay warnings and messages in `"loop"` and `"future"`
  parallel backends
  ([\#400](https://github.com/ropensci/drake/issues/400)).
- Warn when converting trailing dots
  ([\#1147](https://github.com/ropensci/drake/issues/1147)).
- Warn about imports with trailing dots on Windows
  ([\#1147](https://github.com/ropensci/drake/issues/1147)).
- Allow user-defined caches for the
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
  RStudio addin through the new `rstudio_drake_cache` global option
  ([\#1169](https://github.com/ropensci/drake/issues/1169),
  [@joelnitta](https://github.com/joelnitta)).
- Change dynamic target finalization message to “finalize” instead of
  “aggregate” ([\#1176](https://github.com/ropensci/drake/issues/1176),
  [@kendonB](https://github.com/kendonB)).
- Describe the limits of
  [`recoverable()`](https://docs.ropensci.org/drake/reference/recoverable.md),
  e.g. dynamic branching + dynamic files.
- Throw an error instead of a warning in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  if a grouping variable is undefined or invalid
  ([\#1182](https://github.com/ropensci/drake/issues/1182),
  [@kendonB](https://github.com/kendonB)).
- Rigorous S3 framework for static code analysis objects of type
  `drake_deps` and `drake_deps_ht`
  ([\#1183](https://github.com/ropensci/drake/issues/1183)).
- Use
  [`rlang::trace_back()`](https://rlang.r-lib.org/reference/trace_back.html)
  to make `diagnose()$error$calls` nicer
  ([\#1198](https://github.com/ropensci/drake/issues/1198)).

## Version 7.10.0

CRAN release: 2020-02-01

### Unavoidable but minor breaking changes

These changes invalidate some targets in some workflows, but they are
necessary bug fixes.

- Remove spurious local variables detected in `$<-()` and `@<-()`
  ([\#1144](https://github.com/ropensci/drake/issues/1144)).
- Avoid target names with trailing dots
  ([\#1147](https://github.com/ropensci/drake/issues/1147),
  [@Plebejer](https://github.com/Plebejer)).

### Bug fixes

- Handle unequal list columns in
  [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md)
  ([\#1136](https://github.com/ropensci/drake/issues/1136),
  [@jennysjaarda](https://github.com/jennysjaarda)).
- Handle non-vector sub-targets in dynamic branching
  ([\#1138](https://github.com/ropensci/drake/issues/1138)).
- Handle calls in `analyze_assign()`
  ([\#1119](https://github.com/ropensci/drake/issues/1119),
  [@jennysjaarda](https://github.com/jennysjaarda)).
- Restore correct environment locking
  ([\#1143](https://github.com/ropensci/drake/issues/1143),
  [@kuriwaki](https://github.com/kuriwaki)).
- Log `"running"` progress of dynamic targets.
- Log dynamic targets as failed if a sub-target fails
  ([\#1158](https://github.com/ropensci/drake/issues/1158)).

### New features

- Add a new `"fst_tbl"` format for large `tibble` targets
  ([\#1154](https://github.com/ropensci/drake/issues/1154),
  [@kendonB](https://github.com/kendonB)).
- Add a new `format` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), an
  optional custom storage format for targets without an explicit
  `target(format = ...)` in the plan
  ([\#1124](https://github.com/ropensci/drake/issues/1124)).
- Add a new `lock_cache` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) to
  optionally suppress cache locking
  ([\#1129](https://github.com/ropensci/drake/issues/1129)). (It can be
  annoying to interrupt
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  repeatedly and unlock the cache manually every time.)
- Add new functions
  [`cancel()`](https://docs.ropensci.org/drake/reference/cancel.md) and
  [`cancel_if()`](https://docs.ropensci.org/drake/reference/cancel_if.md)
  function to cancel targets mid-build
  ([\#1131](https://github.com/ropensci/drake/issues/1131)).
- Add a new `subtarget_list` argument to
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md) to
  optionally load a dynamic target as a list of sub-targets
  ([\#1139](https://github.com/ropensci/drake/issues/1139),
  [@MilesMcBain](https://github.com/MilesMcBain)).
- Prohibit dynamic
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  ([\#1141](https://github.com/ropensci/drake/issues/1141)).

### Enhancements

- Check for illegal formats early on at the
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  level ([\#1156](https://github.com/ropensci/drake/issues/1156),
  [@MilesMcBain](https://github.com/MilesMcBain)).
- Smoothly deprecate the `config` argument in all user-side functions
  ([\#1118](https://github.com/ropensci/drake/issues/1118),
  [@vkehayas](https://github.com/vkehayas)). Users can now supply the
  plan and other
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  arguments directly, without bothering with
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  Now, you only need to call
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  in the `_drake.R` file for
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) and
  friends. Old code with `config` objects should still work. Affected
  functions:
  - [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  - [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
  - [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)
  - [`drake_debug()`](https://docs.ropensci.org/drake/reference/drake_debug.md)
  - [`recoverable()`](https://docs.ropensci.org/drake/reference/recoverable.md)
  - [`missed()`](https://docs.ropensci.org/drake/reference/missed.md)
  - [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
  - [`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md)
  - [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  - [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  - [`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md)
  - `drake_graph()`
  - [`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)
  - [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md).
    Needed to rename the `targets` argument to `targets_predict` and
    `jobs` to `jobs_predict`.
  - [`predict_workers()`](https://docs.ropensci.org/drake/reference/predict_workers.md).
    Same argument name changes as
    [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md).
- Because of [\#1118](https://github.com/ropensci/drake/issues/1118),
  the only remaining user-side purpose of
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  is to serve functions
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) and
  friends.
- Document the limitations of grouping variables
  ([\#1128](https://github.com/ropensci/drake/issues/1128)).
- Handle the `@` operator. For example, in the static code analysis of
  `x@y`, do not register `y` as a dependency
  ([\#1130](https://github.com/ropensci/drake/issues/1130),
  [@famuvie](https://github.com/famuvie)).
- Remove superfluous/incorrect information about imports from the output
  of
  [`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md)
  ([\#1134](https://github.com/ropensci/drake/issues/1134),
  [@kendonB](https://github.com/kendonB)).
- Append hashes to
  [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
  output ([\#1134](https://github.com/ropensci/drake/issues/1134),
  [@kendonB](https://github.com/kendonB)).
- Add S3 class and pretty print method for `drake_meta_()` objects
  objects.
- Use call stacks instead of environment inheritance to power
  [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md)
  and [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md)
  ([\#1132](https://github.com/ropensci/drake/issues/1132)).
- Allow
  [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md)
  to select the environment with imports
  ([\#882](https://github.com/ropensci/drake/issues/882)).
- Improve visualization labels for dynamic targets: clarify that the
  listed runtime is a total runtime over all sub-targets and list the
  number of sub-targets.

## Version 7.9.0

CRAN release: 2020-01-08

### Breaking changes in dynamic branching

- Embrace the `vctrs` paradigm and its type stability for dynamic
  branching ([\#1105](https://github.com/ropensci/drake/issues/1105),
  [\#1106](https://github.com/ropensci/drake/issues/1106)).
- Accept `target` as a symbol by default in
  [`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md).
  Required for the trace to make sense in
  [\#1107](https://github.com/ropensci/drake/issues/1107).

### Bug fixes

- Repair reference to custom HPC resources in the `"future"` backend
  ([\#1083](https://github.com/ropensci/drake/issues/1083),
  [@jennysjaarda](https://github.com/jennysjaarda)).
- Properly copy data when importing targets from one cache into another
  ([\#1120](https://github.com/ropensci/drake/issues/1120),
  [@brendanf](https://github.com/brendanf)).
- Prevent dynamic vector sizes from conflicting with file sizes in
  metadata.

### New features

- Add a new `log_build_times` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  Allows users to disable the recording of build times. Produces a
  speedup of up to 20% on Macs
  ([\#1078](https://github.com/ropensci/drake/issues/1078)).
- Implement cache locking to prohibit concurrent calls to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md),
  `outdated(make_imports = TRUE)`, `recoverable(make_imports = TRUE)`,
  `vis_drake_graph(make_imports = TRUE)`,
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md), etc.
  on the same cache.
- Add a new `format` trigger to invalidate targets when the specialized
  data format changes
  ([\#1104](https://github.com/ropensci/drake/issues/1104),
  [@kendonB](https://github.com/kendonB)).
- Add new functions `cache_planned()` and `cache_unplanned()` to help
  selectively clean workflows with dynamic targets
  ([\#1110](https://github.com/ropensci/drake/issues/1110),
  [@kendonB](https://github.com/kendonB)).
- Add S3 classes and pretty print methods for
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  objects and `analyze_code()` objects.
- Add a new `"qs"` format
  ([\#1121](https://github.com/ropensci/drake/issues/1121),
  [@kendonB](https://github.com/kendonB)).

### Speedups

- Avoid setting seeds for imports
  ([\#1086](https://github.com/ropensci/drake/issues/1086),
  [@adamkski](https://github.com/adamkski)).
- Avoid working directly with POSIXct times
  ([\#1086](https://github.com/ropensci/drake/issues/1086),
  [@adamkski](https://github.com/adamkski))
- Avoid excessive calls to `%||%` (`%|||%` is faster).
  ([\#1089](https://github.com/ropensci/drake/issues/1089),
  [@billdenney](https://github.com/billdenney))
- Remove `%||NA` due to slowness
  ([\#1089](https://github.com/ropensci/drake/issues/1089),
  [@billdenney](https://github.com/billdenney)).
- Use hash tables to speed up `is_dynamic()` and `is_subtarget()`
  ([\#1089](https://github.com/ropensci/drake/issues/1089),
  [@billdenney](https://github.com/billdenney)).
- Use `getVDigest()` instead of `digest()`
  ([\#1089](https://github.com/ropensci/drake/issues/1089),
  [\#1092](https://github.com/ropensci/drake/issues/1092),
  <https://github.com/eddelbuettel/digest/issues/139#issuecomment-561870289>,
  [@eddelbuettel](https://github.com/eddelbuettel),
  [@billdenney](https://github.com/billdenney)).
- Pre-compute `backtick` and
  [`.deparseOpts()`](https://rdrr.io/r/base/deparseOpts.html) to speed
  up [`deparse()`](https://rdrr.io/r/base/deparse.html)
  ([\#1086](https://github.com/ropensci/drake/issues/1086),
  `https://stackoverflow.com/users/516548/g-grothendieck`,
  [@adamkski](https://github.com/adamkski)).
- Pre-compute which targets exist in advance
  ([\#1095](https://github.com/ropensci/drake/issues/1095)).
- Avoid gratuitous cache interactions and data frame operations in
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md)
  ([\#1098](https://github.com/ropensci/drake/issues/1098)).
- Use `mget_hash()` in
  [`progress()`](https://docs.ropensci.org/drake/reference/progress.md)
  ([\#1098](https://github.com/ropensci/drake/issues/1098)).
- Get target progress info only once in
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  ([\#1098](https://github.com/ropensci/drake/issues/1098)).
- Speed up the retrieval of old metadata in
  [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
  ([\#1098](https://github.com/ropensci/drake/issues/1098)).
- In [`make()`](https://docs.ropensci.org/drake/reference/make.md),
  avoid checking for nonexistent metadata for missing targets.
- Reduce logging in
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).

### Enhancements

- Write a complete project structure in
  [`use_drake()`](https://docs.ropensci.org/drake/reference/use_drake.md)
  ([\#1097](https://github.com/ropensci/drake/issues/1097),
  [@lorenzwalthert](https://github.com/lorenzwalthert),
  [@tjmahr](https://github.com/tjmahr)).
- Add a minor logger note to say how many dynamic sub-targets are
  registered at a time
  ([\#1102](https://github.com/ropensci/drake/issues/1102),
  [@kendonB](https://github.com/kendonB)).
- Handle dependencies that are dynamic targets but not declared as such
  for the current target
  ([\#1107](https://github.com/ropensci/drake/issues/1107)).
- Internally, the “layout” data structure is now called the “workflow
  specification”, or “spec” for short. The spec is `drake`’s
  interpretation of the plan. In the plan, all the dependency
  relationships among targets and files are *implicit*. In the spec,
  they are all *explicit*. We get from the plan to the spec using static
  code analysis, e.g. `analyze_code()`.

## Version 7.8.0

CRAN release: 2019-12-02

### Bug fixes

- Prevent `drake::drake_plan(x = target(...))` from throwing an error if
  `drake` is not loaded
  ([\#1039](https://github.com/ropensci/drake/issues/1039),
  [@mstr3336](https://github.com/mstr3336)).
- Move the `transformations` lifecycle badge to the proper location in
  the docstring
  ([\#1040](https://github.com/ropensci/drake/issues/1040),
  [@jeroen](https://github.com/jeroen)).
- Prevent
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md) /
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) from
  turning an imported function into a target
  ([\#1067](https://github.com/ropensci/drake/issues/1067)).
- Align in-memory `disk.frame` targets with their stored values
  ([\#1077](https://github.com/ropensci/drake/issues/1077),
  [@brendanf](https://github.com/brendanf)).

### New features

- Implement dynamic branching
  ([\#685](https://github.com/ropensci/drake/issues/685)).
- Add a new
  [`subtargets()`](https://docs.ropensci.org/drake/reference/subtargets.md)
  function to get the cached names of the sub-targets of a dynamic
  target.
- Add new `subtargets` arguments to
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md) to
  retrieve specific sub-targets from a parent dynamic target.
- Add new
  [`get_trace()`](https://docs.ropensci.org/drake/reference/get_trace.md)
  and
  [`read_trace()`](https://docs.ropensci.org/drake/reference/read_trace.md)
  functions to help track which values of grouping variables go into the
  making of dynamic sub-targets.
- Add a new
  [`id_chr()`](https://docs.ropensci.org/drake/reference/id_chr.md)
  function to get the name of the target while
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) is
  running.
- Implement `plot(plan)`
  ([\#1036](https://github.com/ropensci/drake/issues/1036)).
- [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md),
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md)
  now take arguments that allow behavior to be defined upon selection of
  nodes.
  ([\#1031](https://github.com/ropensci/drake/issues/1031),@mstr3336).
- Add a new `max_expand` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  to scale down dynamic branching
  ([\#1050](https://github.com/ropensci/drake/issues/1050),
  [@hansvancalster](https://github.com/hansvancalster)).

### Enhancements

- Document transformation functions in a way that avoids having to
  create true functions
  ([\#979](https://github.com/ropensci/drake/issues/979)).
- Avoid always invalidating the memoized layout when we set the knitr
  hash.
- Change the names of environments in
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  objects.
- Assert that `prework` is a language object, list of language objects,
  or character vector ([\#1](https://github.com/ropensci/drake/issues/1)
  at pat-s/multicore-debugging on GitHub,
  [@pat-s](https://github.com/pat-s)).
- Use an environment instead of a list for `config$layout`. Supports
  internal modifications by reference. Required for
  [\#685](https://github.com/ropensci/drake/issues/685).
- Clean up the code of the parallel backends.
- Make `dynamic` a formal argument of
  [`target()`](https://docs.ropensci.org/drake/reference/target.md).
- Always lock/unlock the environment target by target, allowing
  informative error messages to appear more readily
  ([\#1062](https://github.com/ropensci/drake/issues/1062),
  [@PedramNavid](https://github.com/PedramNavid))
- Automatically ignore `storr`s and decorated `storr`s
  ([\#1071](https://github.com/ropensci/drake/issues/1071)).
- Speed up memory management by avoiding a call to
  [`setdiff()`](https://generics.r-lib.org/reference/setops.html) and
  avoiding `names(config$envir_targets)`.

## Version 7.7.0

CRAN release: 2019-10-15

### Bug fixes

- Take the sum instead of the max in `dir_size()`. Incurs rehashing for
  some workflows, but should not invalidate any targets.

### New features

- Add a new
  [`which_clean()`](https://docs.ropensci.org/drake/reference/which_clean.md)
  function to preview which targets will be invalidated by
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md)
  ([\#1014](https://github.com/ropensci/drake/issues/1014),
  [@pat-s](https://github.com/pat-s)).
- Add serious import and export methods for the decorated `storr`
  ([\#1015](https://github.com/ropensci/drake/issues/1015),
  [@billdenney](https://github.com/billdenney),
  [@noamross](https://github.com/noamross)).
- Add a new `"diskframe"` format for larger-than-memory data
  ([\#1004](https://github.com/ropensci/drake/issues/1004),
  [@xiaodaigh](https://github.com/xiaodaigh)).
- Add a new
  [`drake_tempfile()`](https://docs.ropensci.org/drake/reference/drake_tempfile.md)
  function to help with `"diskframe"` format. It makes sure we are not
  copying large datasets across different physical storage media
  ([\#1004](https://github.com/ropensci/drake/issues/1004),
  [@xiaodaigh](https://github.com/xiaodaigh)).
- Add new function
  [`code_to_function()`](https://docs.ropensci.org/drake/reference/code_to_function.md)
  to allow for parsing script based workflows into functions so
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  can begin to manage the workflow and track dependencies.
  ([\#994](https://github.com/ropensci/drake/issues/994),
  [@thebioengineer](https://github.com/thebioengineer))

### Enhancements

- Coerce seeds to integers in `seed_trigger()`
  ([\#1013](https://github.com/ropensci/drake/issues/1013),
  [@CreRecombinase](https://github.com/CreRecombinase)).
- Hard wrap long labels in graph visuals
  ([\#1017](https://github.com/ropensci/drake/issues/1017)).
- Nest the history `txtq` API inside decorated `storr` API
  ([\#1020](https://github.com/ropensci/drake/issues/1020)).
- Reduce cyclomatic complexity of internal functions.
- Reduce retrievals of old target metadata to try to improve performance
  ([\#1027](https://github.com/ropensci/drake/issues/1027)).

## Version 7.6.2

CRAN release: 2019-09-14

### Bug fixes

- Remove README.md from CRAN altogether. Also remove all links from the
  news and vignette. The links trigger too many CRAN notes, which made
  the automated checks too brittle.
- Serialize formats that need serialization (like “keras”) before
  sending the data from HPC workers to the main process
  ([\#989](https://github.com/ropensci/drake/issues/989)).
- Check for custom-formatted files when checking checksums.
- Force fst-formatted targets to plain data frames. Same goes for the
  new “fst_dt” format.
- Change the meaning and behavior of `max_expand` in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
  `max_expand` is now the maximum number of targets produced by
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  and
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md).
  For
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  this reduces the number of targets (less cumbersome) and makes the
  subsample of targets more representative of the complete grid. It
  also. ensures consistent target naming when `.id` is `FALSE`
  ([\#1002](https://github.com/ropensci/drake/issues/1002)). Note:
  `max_expand` is not for production workflows anyway, so this change
  does not break anything important. Unfortunately, we do lose the speed
  boost in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  originally due to `max_expand`, but
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  is still fast, so that is not so bad.
- Drop specialized formats of `NULL` targets
  ([\#998](https://github.com/ropensci/drake/issues/998)).
- Prevent false grouping variables from partially tagging along in
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  ([\#1009](https://github.com/ropensci/drake/issues/1009)). The same
  fix should apply to
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  and
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md)
  too.
- Respect graph topology when recovering old grouping variables for
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  ([\#1010](https://github.com/ropensci/drake/issues/1010)).

### New features

- Add a new “fst_dt” format for `fst`-powered saving of `data.table`
  objects.
- Support a custom “caching” column of the plan to select main vs worker
  caching for each target individually
  ([\#988](https://github.com/ropensci/drake/issues/988)).
- Make `transform` a formal argument of
  [`target()`](https://docs.ropensci.org/drake/reference/target.md) so
  that users do not have to type “transform =” all the time in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  ([\#993](https://github.com/ropensci/drake/issues/993)).
- Migrate the documentation website from `ropensci.github.io/drake` to
  `docs.ropensci.org/drake`.

### Enhancements

- Document the HPC limitations of `target(format = "keras")`
  ([\#989](https://github.com/ropensci/drake/issues/989)).
- Remove the now-superfluous vignette.
- Wrap up console and text file logging functionality into a reference
  class ([\#964](https://github.com/ropensci/drake/issues/964)).
- Deprecate the `verbose` argument in various caching functions. The
  location of the cache is now only printed in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). This
  made the previous feature easier to implement.
- Carry forward nested grouping variables in
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  ([\#1008](https://github.com/ropensci/drake/issues/1008)).
- Improve the encapsulation of hash tables in the decorated `storr`
  ([\#968](https://github.com/ropensci/drake/issues/968)).

## Version 7.6.1

CRAN release: 2019-08-19

### Bug fixes

- CRAN hotfix: remove a broken link in the README.

## Version 7.6.0

### Bug fixes

- Make `drake_plan(transform = slice())` understand `.id` and grouping
  variables ([\#963](https://github.com/ropensci/drake/issues/963)).
- Repair `clean(garbage_collection = TRUE, destroy = TRUE)`. Previously
  it destroyed the cache before trying to collect garbage.
- Ensure that
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md)
  passes informative error messages back to the calling process
  ([\#969](https://github.com/ropensci/drake/issues/969)).
- Avoid downloading full contents of URLs when rehashing
  ([\#982](https://github.com/ropensci/drake/issues/982))
- Retain upstream grouping variables of
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  and
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  on topologically side-by-side targets
  ([\#983](https://github.com/ropensci/drake/issues/983)).
- Manually enforce the correct ordering in `dsl_left_outer_join()` so
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  selects the right combinations of existing targets
  ([\#986](https://github.com/ropensci/drake/issues/986)). This bug was
  probably introduced in the solution to
  [\#983](https://github.com/ropensci/drake/issues/983).
- Make the output of
  [`progress()`](https://docs.ropensci.org/drake/reference/progress.md)
  more consistent, less dependent on whether `tidyselect` is installed.

### New features

- Support specialized data storage via a decorated cache and `format`
  argument of
  [`target()`](https://docs.ropensci.org/drake/reference/target.md)
  ([\#971](https://github.com/ropensci/drake/issues/971)). This allows
  users to leverage faster ways to save and load targets, such as
  `write_fst()` for data frames and `save_model_hdf5()` for Keras
  models. It also improves memory because it prevents `storr` from
  making a serialized in-memory copy of large data objects.
- Add `tidyselect` functionality for `...` in
  [`progress()`](https://docs.ropensci.org/drake/reference/progress.md),
  analogous to
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md),
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md),
  and [`clean()`](https://docs.ropensci.org/drake/reference/clean.md).
- Support S3 for user-defined generics
  ([\#959](https://github.com/ropensci/drake/issues/959)). If the
  generic `do_stuff()` and the method `stuff.your_class()` are defined
  in `envir`, and if `do_stuff()` has a call to `UseMethod("stuff")`,
  then `drake`’s code analysis will detect `stuff.your_class()` as a
  dependency of `do_stuff()`.
- Add authentication support for
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  URLs. Requires the new `curl_handles` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  ([\#981](https://github.com/ropensci/drake/issues/981)).

### Enhancements

- Document DSL keywords as if they were true functions:
  [`target()`](https://docs.ropensci.org/drake/reference/target.md),
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`split()`](https://docs.ropensci.org/drake/reference/transformations.md),
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md),
  and
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  ([\#979](https://github.com/ropensci/drake/issues/979)).
- Do garbage collection between the unloading and loading phases of
  memory management.
- Keep
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files in
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) unless
  `garbage_collection` is `TRUE`. That way, `make(recover = TRUE)` is a
  true “undo button” for
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md).
  `clean(garbage_collection = TRUE)` still removes data in the cache, as
  well as any
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files from targets currently being cleaned.
- The menu in
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) only
  appears if `garbage_collection` is `TRUE`. Also, this menu is added to
  `rescue_cache(garbage_collection = TRUE)`.
- Reorganize the internal code files and functions to make development
  easier.
- Move the history inside the cache folder `.drake/`. The old
  `.drake_history/` folder was awkward. Old histories are migrated
  during
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
  and
  [`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md).
- Add lifecycle badges to exported functions.

## Version 7.5.2

CRAN release: 2019-07-21

### Bug fixes

- Eliminate accidental creations of `.drake_history` in
  [`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md),
  [`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md),
  and the examples in the help files.

## Version 7.5.1

### Bug fixes

- Change .drake_history\$ to ^.drake_history\$ in .Rbuildignore appease
  CRAN checks.
- Repair help file examples.

## Version 7.5.0

### New features

- Add automated data recovery
  ([\#945](https://github.com/ropensci/drake/issues/945)). This is still
  experimental and disabled by default. Requires `make(recover = TRUE)`.
- Add new functions
  [`recoverable()`](https://docs.ropensci.org/drake/reference/recoverable.md)
  and
  [`r_recoverable()`](https://docs.ropensci.org/drake/reference/r_make.md)
  to show targets that are outdated but recoverable via
  `make(recover = TRUE)`.
- Track the history and provenance of targets, viewable with
  [`drake_history()`](https://docs.ropensci.org/drake/reference/drake_history.md).
  Powered by `txtq`
  ([\#918](https://github.com/ropensci/drake/issues/918),
  [\#920](https://github.com/ropensci/drake/issues/920)).
- Add a new
  [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md)
  function, similar to
  [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md).
  [`no_deps()`](https://docs.ropensci.org/drake/reference/no_deps.md)
  suppresses dependency detection but still tracks changes to the
  literal code ([\#910](https://github.com/ropensci/drake/issues/910)).
- Add a new “autoclean” memory strategy
  ([\#917](https://github.com/ropensci/drake/issues/917)).
- Export
  [`transform_plan()`](https://docs.ropensci.org/drake/reference/transform_plan.md).
- Allow a custom `seed` column of `drake` plans to set custom seeds
  ([\#947](https://github.com/ropensci/drake/issues/947)).
- Add a new `seed` trigger to optionally ignore changes to the target
  seed ([\#947](https://github.com/ropensci/drake/issues/947)).

### Enhancements

- In
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  interpret custom columns as non-language objects
  ([\#942](https://github.com/ropensci/drake/issues/942)).
- Suggest and assert `clustermq` \>= 0.8.8.
- Log the target name in a special column in the console log file
  ([\#909](https://github.com/ropensci/drake/issues/909)).
- Rename the “memory” memory strategy to “preclean” (with deprecation;
  [\#917](https://github.com/ropensci/drake/issues/917)).
- Deprecate `ensure_workers` in
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  and [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Warn when the user supplies additional arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) after
  `config` is already supplied.
- Prevent users from running
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) from
  inside the cache
  ([\#927](https://github.com/ropensci/drake/issues/927)).
- Add `CITATION` file with JOSS paper.
- In
  [`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md),
  include the seed and change the names.
- Allow the user to set a different seed in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). All
  this does is invalidate old targets.
- Use `set_hash()` and `get_hash()` in `storr` to double the speed of
  progress tracking.

### Bug fixes

- In the static code analysis for dependency detection, ignore list
  elements referenced with `$`
  ([\#938](https://github.com/ropensci/drake/issues/938)).
- Minor: handle strings embedded in language objects
  ([\#934](https://github.com/ropensci/drake/issues/934)).
- Minor: supply `xxhash64` as the default hash algorithm for non-`storr`
  hashing if the driver does not have a hash algorithm.

## Version 7.4.0

CRAN release: 2019-06-07

### Mildly breaking changes

These changes are technically breaking changes, but they should only
affect advanced users.

- [`rescue_cache()`](https://docs.ropensci.org/drake/reference/rescue_cache.md)
  no longer returns a value.

### Bug fixes

- Restore compatibility with `clustermq`
  ([\#898](https://github.com/ropensci/drake/issues/898)). Suggest
  version \>= 0.8.8 but allow 0.8.7 as well.
- Ensure `drake` recomputes `config$layout` when `knitr` reports change
  ([\#887](https://github.com/ropensci/drake/issues/887)).
- Do not rehash large imported files every
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  ([\#878](https://github.com/ropensci/drake/issues/878)).
- Repair parsing of long tidy eval inputs in the DSL
  ([\#878](https://github.com/ropensci/drake/issues/878)).
- Clear up cache confusion when a custom cache exists adjacent to the
  default cache ([\#883](https://github.com/ropensci/drake/issues/883)).
- Accept targets as symbols in
  [`r_drake_build()`](https://docs.ropensci.org/drake/reference/r_make.md).
- Log progress during
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md)
  ([\#889](https://github.com/ropensci/drake/issues/889)).
- Repair
  [`expose_imports()`](https://docs.ropensci.org/drake/reference/expose_imports.md):
  do not do the `environment<-` trick unless the object is a
  non-primitive function.
- Use different static analyses of
  [`assign()`](https://rdrr.io/r/base/assign.html) vs
  [`delayedAssign()`](https://rdrr.io/r/base/delayedAssign.html).
- Fix a superfluous code analysis warning incurred by multiple
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  files and other strings
  ([\#896](https://github.com/ropensci/drake/issues/896)).
- Make [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md)
  work inside
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md),
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md),
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md),
  and
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md).

### New features

- Add experimental support for URLs in
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  and
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md).
  `drake` now treats
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)/[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  files as URLS if they begin with “<http://>”, “<https://>”, or
  “<ftp://>”. The fingerprint is a concatenation of the ETag and
  last-modified timestamp. If neither can be found or if there is no
  internet connection, `drake` throws an error.
- Implement new memory management strategies `"unload"` and `"none"`,
  which do not attempt to load a target’s dependencies from memory
  ([\#897](https://github.com/ropensci/drake/issues/897)).
- Allow users to give each target its own memory strategy
  ([\#897](https://github.com/ropensci/drake/issues/897)).
- Add
  [`drake_slice()`](https://docs.ropensci.org/drake/reference/drake_slice.md)
  to help split data across multiple targets. Related:
  [\#77](https://github.com/ropensci/drake/issues/77),
  [\#685](https://github.com/ropensci/drake/issues/685),
  [\#833](https://github.com/ropensci/drake/issues/833).
- Introduce a new
  [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md)
  function, which is now recommended instead of
  [`get_cache()`](https://docs.ropensci.org/drake/reference/get_cache.md)
  ([\#883](https://github.com/ropensci/drake/issues/883)).
- Introduce a new
  [`r_deps_target()`](https://docs.ropensci.org/drake/reference/r_make.md)
  function.
- Add RStudio addins for
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md),
  [`r_vis_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md),
  and
  [`r_outdated()`](https://docs.ropensci.org/drake/reference/r_make.md)
  ([\#892](https://github.com/ropensci/drake/issues/892)).

### Enhancements

- Deprecate
  [`get_cache()`](https://docs.ropensci.org/drake/reference/get_cache.md)
  in favor of
  [`drake_cache()`](https://docs.ropensci.org/drake/reference/drake_cache.md).
- Show the path to the cache in the
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) menu
  prompt.
- Stop removing the console log file on each call to
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Log the node name (short host name) and process ID in the console log
  file.
- Log the name of the calling function in the console log file,
  e.g. “begin make()” and “end make()”. Applies to all functions that
  accept a `config` argument.
- Memory management: set `use_cache` to `FALSE` in `storr` function
  calls for saving and loading targets. Also, at the end of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), call
  `flush_cache()` (and then [`gc()`](https://rdrr.io/r/base/gc.html) if
  garbage collection is enabled).
- Mention [`callr::r()`](https://callr.r-lib.org/reference/r.html)
  within commands as a safe alternative to `lock_envir = FALSE` in the
  self-invalidation section of the
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) help
  file.
- Use file size to help decide when to rehash
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)/[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)/[`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  files. We now rehash files if the file is less than 100 KB or the time
  stamp changed or the **file size** changed.

## Version 7.3.0

CRAN release: 2019-05-19

### Bug fixes

- Accommodate `rlang`’s new interpolation operator `{{`, which was
  causing [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  to fail when
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  commands are enclosed in curly braces
  ([\#864](https://github.com/ropensci/drake/issues/864)).
- Move “`config$lock_envir <- FALSE`” from `loop_build()` to
  `backend_loop()`. This makes sure `config$envir` is correctly locked
  in `make(parallelism = "clustermq")`.
- Convert factors to characters in the optional `.data` argument of
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  and
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  in the DSL.
- In the DSL of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  repair `cross(.data = !!args)`, where `args` is an optional data frame
  of grouping variables.
- Handle trailing slashes in
  [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)/[`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  directories for Windows
  ([\#855](https://github.com/ropensci/drake/issues/855)).
- Make `.id_chr` work with
  [`combine()`](https://docs.ropensci.org/drake/reference/transformations.md)
  in the DSL ([\#867](https://github.com/ropensci/drake/issues/867)).
- Do not try `make_spinner()` unless the version of `cli` is at least
  1.1.0.

### New features

- Add functions
  [`text_drake_graph()`](https://docs.ropensci.org/drake/reference/text_drake_graph.md)
  (and
  [`r_text_drake_graph()`](https://docs.ropensci.org/drake/reference/r_make.md)
  and
  [`render_text_drake_graph()`](https://docs.ropensci.org/drake/reference/render_text_drake_graph.md)).
  Uses text art to print a dependency graph to the terminal window.
  Handy for when users SSH into remote machines without X Window
  support.
- Add a new `max_expand` argument to
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  an optional upper bound on the lengths of grouping variables for
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  and
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  in the DSL. Comes in handy when you have a massive number of targets
  and you want to test on a miniature version of your workflow before
  you scale up to production.

### Enhancements

- Delay the initialization of `clustermq` workers for as long as
  possible. Before launching them, build/check targets locally until we
  reach an outdated target with `hpc` equal to `FALSE`. In other words,
  if no targets actually require `clustermq` workers, no workers get
  created.
- In `make(parallelism = "future")`, reset the `config$sleep()` backoff
  interval whenever a new target gets checked.
- Add a “done” message to the console log file when the workflow has
  completed.
- Replace `CodeDepends` with a base R solution in
  [`code_to_plan()`](https://docs.ropensci.org/drake/reference/code_to_plan.md).
  Fixes a CRAN note.
- The DSL (transformations in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md))
  is no longer experimental.
- The `callr` API
  ([`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) and
  friends) is no longer experimental.
- Deprecate the wildcard/text-based functions for creating plans:
  [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md),
  [`expand_plan()`](https://docs.ropensci.org/drake/reference/expand_plan.md),
  [`map_plan()`](https://docs.ropensci.org/drake/reference/map_plan.md),
  [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md),
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md),
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md),
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md).
- Change some deprecated functions to defunct:
  [`deps()`](https://docs.ropensci.org/drake/reference/deps.md),
  [`max_useful_jobs()`](https://docs.ropensci.org/drake/reference/max_useful_jobs.md),
  and
  [`migrate_drake_project()`](https://docs.ropensci.org/drake/reference/migrate_drake_project.md).

## Version 7.2.0

CRAN release: 2019-04-19

### Mildly breaking changes

- In the DSL (e.g. `drake_plan(x = target(..., transform = map(...)))`
  avoid inserting extra dots in target names when the grouping variables
  are character vectors
  ([\#847](https://github.com/ropensci/drake/issues/847)). Target names
  come out much nicer this way, but those name changes will invalidate
  some targets (i.e. they need to be rebuilt with
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)).

### Bug fixes

- Use `config$jobs_preprocess` (local jobs) in several places where
  `drake` was incorrectly using `config$jobs` (meant for targets).
- Allow `loadd(x, deps = TRUE, config = your_config)` to work even if
  `x` is not cached
  ([\#830](https://github.com/ropensci/drake/issues/830)). Required
  disabling `tidyselect` functionality when `deps` `TRUE`. There is a
  new note in the help file about this, and an informative console
  message prints out on `loadd(deps = TRUE, tidyselect = TRUE)`. The
  default value of `tidyselect` is now `!deps`.
- Minor: avoid printing messages and warnings twice to the console
  ([\#829](https://github.com/ropensci/drake/issues/829)).
- Ensure compatibility with `testthat` \>= 2.0.1.9000.

### New features

- In
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  transformations, allow the user to refer to a target’s own name using
  a special `.id_chr` symbol, which is treated like a character string.
- Add a `transparency` argument to
  [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  and
  [`render_drake_ggraph()`](https://docs.ropensci.org/drake/reference/render_drake_ggraph.md)
  to disable transparency in the rendered graph. Useful for R
  installations without transparency support.

### Enhancements

- Use a custom layout to improve node positions and aspect ratios of
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  displays. Only activated in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  when there are at least 10 nodes distributed in both the vertical and
  horizontal directions.
- Allow nodes to be dragged both vertically and horizontally in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md).
- Prevent dots from showing up in target names when you supply grouping
  variables to transforms in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  ([\#847](https://github.com/ropensci/drake/issues/847)).
- Do not keep `drake` plans
  ([`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md))
  inside
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  objects. When other bottlenecks are removed, this will reduce the
  burden on memory (re
  [\#800](https://github.com/ropensci/drake/issues/800)).
- Do not retain the `targets` argument inside
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  objects. This is to reduce memory consumption.
- Deprecate the `layout` and `direction` arguments of
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md).
  Direction is now always left to right and the layout is always
  Sugiyama.
- Write the cache log file in CSV format (now `drake_cache.csv` by
  default) to avoid issues with spaces (e.g. entry names with spaces in
  them, such as “file report.Rmd”)\`.

## Version 7.1.0

CRAN release: 2019-04-07

### Bug fixes

- In `drake` 7.0.0, if you run
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) in
  interactive mode and respond to the menu prompt with an option other
  than `1` or `2`, targets will still build.
- Make sure file outputs show up in `drake_graph()`. The bug came from
  `append_output_file_nodes()`, a utility function of
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md).
- Repair `r_make(r_fn = callr::r_bg())` re
  [\#799](https://github.com/ropensci/drake/issues/799).
- Allow
  [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  and
  [`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md)
  to work when the graph has no edges.

### New features

- Add a new
  [`use_drake()`](https://docs.ropensci.org/drake/reference/use_drake.md)
  function to write the `make.R` and `_drake.R` files from the “main
  example”. Does not write other supporting scripts.
- With an optional logical `hpc` column in your
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  you can now select which targets to deploy to HPC and which to run
  locally.
- Add a `list` argument to
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md),
  just like
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md).
- Add a new RStudio addin: ‘loadd target at cursor’ which can be bound a
  keyboard shortcut to load the target identified by the symbol at the
  cursor position to the global environment.

### Enhancements

- [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
  and
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
  can now handle entire directories,
  e.g. `file_in("your_folder_of_input_data_files")` and
  `file_out("directory_with_a_bunch_of_output_files")`.
- Send less data from `config` to HPC workers.
- Improve
  [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  - Hide node labels by default and render the arrows behind the nodes.
  - Print an informative error message when the user supplies a `drake`
    plan to the `config` argument of a function.
  - By default, use gray arrows and a black-and-white background with no
    gridlines.
- For the
  [`map()`](https://docs.ropensci.org/drake/reference/transformations.md)
  and
  [`cross()`](https://docs.ropensci.org/drake/reference/transformations.md)
  transformations in the DSL, prevent the accidental sorting of targets
  by name ([\#786](https://github.com/ropensci/drake/issues/786)).
  Needed `merge(sort = FALSE)` in `dsl_left_outer_join()`.
- Simplify verbosity. The `verbose` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) now
  takes values 0, 1, and 2, and maximum verbosity in the console prints
  targets, retries, failures, and a spinner. The console log file, on
  the other hand, dumps maximally verbose runtime info regardless of the
  `verbose` argument.
- In previous versions, functions generated with
  `f <- Rcpp::cppFunction(...)` did not stay up to date from session to
  session because the addresses corresponding to anonymous pointers were
  showing up in `deparse(f)`. Now, `drake` ignores those pointers, and
  `Rcpp` functions compiled inline appear to stay up to date. This
  problem was more of an edge case than a bug.
- Prepend time stamps with sub-second times to the lines of the console
  log file.
- In
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  deprecate the `tidy_evaluation` argument in favor of the new and more
  concise `tidy_eval`. To preserve back compatibility for now, if you
  supply a non-`NULL` value to `tidy_evaluation`, it overwrites
  `tidy_eval`.
- Reduce the object size of
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  objects by assigning closure of `config$sleep` to
  [`baseenv()`](https://rdrr.io/r/base/environment.html).

## Version 7.0.0

CRAN release: 2019-03-10

### Breaking changes

- The enhancements that increase cache access speed also invalidate
  targets in old projects. Workflows built with drake \<= 6.2.1 will
  need to run from scratch again.
- In `drake` plans, the `command` and `trigger` columns are now lists of
  language objects instead of character vectors.
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  friends still work if you have character columns, but the default
  output of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  has changed to this new format.
- All parallel backends (`parallelism` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)) except
  “clustermq” and “future” are removed. A new “loop” backend covers
  local serial execution.
- A large amount of deprecated functionality is now defunct, including
  several functions
  ([`built()`](https://docs.ropensci.org/drake/reference/built.md),
  [`find_project()`](https://docs.ropensci.org/drake/reference/find_project.md),
  [`imported()`](https://docs.ropensci.org/drake/reference/imported.md),
  and
  [`parallel_stages()`](https://docs.ropensci.org/drake/reference/parallel_stages.md);
  full list at [\#564](https://github.com/ropensci/drake/issues/564))
  and the single-quoted file API.
- Set the default value of `lock_envir` to `TRUE` in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  So [`make()`](https://docs.ropensci.org/drake/reference/make.md) will
  automatically quit in error if the act of building a target tries to
  change upstream dependencies.
- [`make()`](https://docs.ropensci.org/drake/reference/make.md) no
  longer returns a value. Users will need to call
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  separately to get the old return value of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Require the `jobs` argument to be of length 1
  ([`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)).
  To parallelize the imports and other preprocessing steps, use
  `jobs_preprocess`, also of length 1.
- Get rid of the “kernels” `storr` namespace. As a result, `drake` is
  faster, but users will no longer be able to load imported functions
  using [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
  or [`readd()`](https://docs.ropensci.org/drake/reference/readd.md).
- In [`target()`](https://docs.ropensci.org/drake/reference/target.md),
  users must now explicitly name all the arguments except `command`,
  e.g. `target(f(x), trigger = trigger(condition = TRUE))` instead of
  `target(f(x), trigger(condition = TRUE))`.
- Fail right away in
  [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md)
  when the result has duplicated target names. This makes `drake`’s API
  more predictable and helps users catch malformed workflows earlier.
- [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) only
  loads targets listed in the plan. It no longer loads imports or file
  hashes.
- The return values of
  [`progress()`](https://docs.ropensci.org/drake/reference/progress.md),
  [`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md),
  [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md),
  and
  [`predict_workers()`](https://docs.ropensci.org/drake/reference/predict_workers.md)
  are now data frames.
- Change the default value of `hover` to `FALSE` in visualization
  functions. Improves speed.

### Bug fixes

- Allow
  [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md)
  to work with lists of plans (`bind_plans(list(plan1, plan2))` was
  returning `NULL` in `drake` 6.2.0 and 6.2.1).
- Ensure that `get_cache(path = "non/default/path", search = FALSE)`
  looks for the cache in `"non/default/path"` instead of
  [`getwd()`](https://rdrr.io/r/base/getwd.html).
- Remove strict dependencies on package `tibble`.
- Pass the correct data structure to `ensure_loaded()` in `meta.R` and
  `triggers.R` when ensuring the dependencies of the `condition` and
  `change` triggers are loaded.
- Require a `config` argument to
  [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)
  and `loadd(deps = TRUE)`.

### New features

- Introduce a new experimental domain-specific language for generating
  large plans ([\#233](https://github.com/ropensci/drake/issues/233)).
  Details in the “Plans” chapter of the manual.
- Implement a `lock_envir` argument to safeguard reproducibility. More
  discussion: [\#619](https://github.com/ropensci/drake/issues/619),
  [\#620](https://github.com/ropensci/drake/issues/620).
- The new
  [`from_plan()`](https://docs.ropensci.org/drake/reference/from_plan.md)
  function allows the users to reference custom plan columns from within
  commands. Changes to values in these columns columns do not invalidate
  targets.
- Add a menu prompt
  ([\#762](https://github.com/ropensci/drake/issues/762)) to safeguard
  against [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  pitfalls in interactive mode
  ([\#761](https://github.com/ropensci/drake/issues/761)). Appears once
  per session. Disable with `options(drake_make_menu = FALSE)`.
- Add new API functions
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md),
  [`r_outdated()`](https://docs.ropensci.org/drake/reference/r_make.md),
  etc. to run `drake` functions more reproducibly in a clean session.
  See the help file of
  [`r_make()`](https://docs.ropensci.org/drake/reference/r_make.md) for
  details.
- [`progress()`](https://docs.ropensci.org/drake/reference/progress.md)
  gains a `progress` argument for filtering results. For example,
  `progress(progress = "failed")` will report targets that failed.

### Enhancements

- **Large speed boost**: move away from `storr`’s key mangling in favor
  of `drake`’s own encoding of file paths and namespaced functions for
  `storr` keys.
- Exclude symbols `.`, `..`, and `.gitignore` from being target names
  (consequence of the above).
- Use only one hash algorithm per `drake` cache, which the user can set
  with the `hash_algorithm` argument of
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md),
  [`storr::storr_rds()`](https://richfitz.github.io/storr/reference/storr_rds.html),
  and various other cache functions. Thus, the concepts of a “short hash
  algorithm” and “long hash algorithm” are deprecated, and the functions
  [`long_hash()`](https://docs.ropensci.org/drake/reference/long_hash.md),
  [`short_hash()`](https://docs.ropensci.org/drake/reference/short_hash.md),
  [`default_long_hash_algo()`](https://docs.ropensci.org/drake/reference/default_long_hash_algo.md),
  [`default_short_hash_algo()`](https://docs.ropensci.org/drake/reference/default_short_hash_algo.md),
  and
  [`available_hash_algos()`](https://docs.ropensci.org/drake/reference/available_hash_algos.md)
  are deprecated. Caches are still back-compatible with `drake` \> 5.4.0
  and \<= 6.2.1.
- Allow the `magrittr` dot symbol to appear in some commands sometimes.
- Deprecate the `fetch_cache` argument in all functions.
- Remove packages `DBI` and `RSQLite` from “Suggests”.
- Define a special `config$eval <- new.env(parent = config$envir)` for
  storing built targets and evaluating commands in the plan. Now,
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) no
  longer modifies the user’s environment. This move is a long-overdue
  step toward purity.
- Remove dependency on the `codetools` package.
- Deprecate and remove the `session` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  Details: in [\#623](https://github.com/ropensci/drake/issues/623).
- Deprecate the `graph` and `layout` arguments to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  The change simplifies the internals, and memoization allows us to do
  this.
- Warn the user if running
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) in a
  subdirectory of the `drake` project root (determined by the location
  of the `.drake` folder in relation to the working directory).
- In the code analysis, explicitly prohibit targets from being
  dependencies of imported functions.
- Increase options for the `verbose` argument, including the option to
  print execution and total build times.
- Separate the building of targets from the processing of imports.
  Imports are processed with rudimentary staged parallelism
  (`mclapply()` or `parLapply()`, depending on the operating system).
- Ignore the imports when it comes to build times. Functions
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md),
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md),
  etc. focus on only the targets.
- Deprecate many API functions, including
  [`plan_analyses()`](https://docs.ropensci.org/drake/reference/plan_analyses.md),
  [`plan_summaries()`](https://docs.ropensci.org/drake/reference/plan_summaries.md),
  [`analysis_wildcard()`](https://docs.ropensci.org/drake/reference/analysis_wildcard.md),
  [`cache_namespaces()`](https://docs.ropensci.org/drake/reference/cache_namespaces.md),
  [`cache_path()`](https://docs.ropensci.org/drake/reference/cache_path.md),
  [`check_plan()`](https://docs.ropensci.org/drake/reference/check_plan.md),
  [`dataset_wildcard()`](https://docs.ropensci.org/drake/reference/dataset_wildcard.md),
  [`drake_meta()`](https://docs.ropensci.org/drake/reference/drake_meta.md),
  [`drake_palette()`](https://docs.ropensci.org/drake/reference/drake_palette.md),
  [`drake_tip()`](https://docs.ropensci.org/drake/reference/drake_tip.md),
  [`recover_cache()`](https://docs.ropensci.org/drake/reference/recover_cache.md),
  [`cleaned_namespaces()`](https://docs.ropensci.org/drake/reference/cleaned_namespaces.md),
  [`target_namespaces()`](https://docs.ropensci.org/drake/reference/target_namespaces.md),
  [`read_drake_config()`](https://docs.ropensci.org/drake/reference/read_drake_config.md),
  [`read_drake_graph()`](https://docs.ropensci.org/drake/reference/read_drake_graph.md),
  and
  [`read_drake_plan()`](https://docs.ropensci.org/drake/reference/read_drake_plan.md).
- Deprecate
  [`target()`](https://docs.ropensci.org/drake/reference/target.md) as a
  user-side function. From now on, it should only be called from within
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
- [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md)
  now throws an error, not a warning, if called in the incorrect
  context. Should be called only inside commands in the user’s `drake`
  plan.
- Replace `*expr*()` `rlang` functions with their `*quo*()`
  counterparts. We still keep
  [`rlang::expr()`](https://rlang.r-lib.org/reference/expr.html) in the
  few places where we know the expressions need to be evaluated in
  `config$eval`.
- The `prework` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  can now be an expression (language object) or list of expressions.
  Character vectors are still acceptable.
- At the end of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md), print
  messages about triggers etc. only if `verbose >= 2L`.
- Deprecate and rename
  [`in_progress()`](https://docs.ropensci.org/drake/reference/in_progress.md)
  to
  [`running()`](https://docs.ropensci.org/drake/reference/running.md).
- Deprecate and rename
  [`knitr_deps()`](https://docs.ropensci.org/drake/reference/knitr_deps.md)
  to
  [`deps_knitr()`](https://docs.ropensci.org/drake/reference/deps_knitr.md).
- Deprecate and rename
  [`dependency_profile()`](https://docs.ropensci.org/drake/reference/dependency_profile.md)
  to
  [`deps_profile()`](https://docs.ropensci.org/drake/reference/deps_profile.md).
- Deprecate and rename
  [`predict_load_balancing()`](https://docs.ropensci.org/drake/reference/predict_load_balancing.md)
  to
  [`predict_workers()`](https://docs.ropensci.org/drake/reference/predict_workers.md).
- Deprecate
  [`this_cache()`](https://docs.ropensci.org/drake/reference/this_cache.md)
  and defer to
  [`get_cache()`](https://docs.ropensci.org/drake/reference/get_cache.md)
  and
  [`storr::storr_rds()`](https://richfitz.github.io/storr/reference/storr_rds.html)
  for simplicity.
- Change the default value of `hover` to `FALSE` in visualization
  functions. Improves speed. Also a breaking change.
- Deprecate
  [`drake_cache_log_file()`](https://docs.ropensci.org/drake/reference/drake_cache_log_file.md).
  We recommend using
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) with the
  `cache_log_file` argument to create the cache log. This way ensures
  that the log is always up to date with
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) results.

## Version 6.2.1

CRAN release: 2018-12-10

Version 6.2.1 is a hotfix to address the failing automated CRAN checks
for 6.2.0. Chiefly, in CRAN’s Debian R-devel (2018-12-10) check
platform, errors of the form “length \> 1 in coercion to logical”
occurred when either argument to `&&` or `||` was not of length 1
(e.g. `nzchar(letters) && length(letters)`). In addition to fixing these
errors, version 6.2.1 also removes a problematic link from the vignette.

## Version 6.2.0

### New features

- Add a `sep` argument to
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md),
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md),
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md),
  [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md),
  [`expand_plan()`](https://docs.ropensci.org/drake/reference/expand_plan.md),
  [`plan_analyses()`](https://docs.ropensci.org/drake/reference/plan_analyses.md),
  and
  [`plan_summaries()`](https://docs.ropensci.org/drake/reference/plan_summaries.md).
  Allows the user to set the delimiter for generating new target names.
- Expose a `hasty_build` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  Here, the user can set the function that builds targets in “hasty
  mode” (`make(parallelism = "hasty")`).
- Add a new
  [`drake_envir()`](https://docs.ropensci.org/drake/reference/drake_envir.md)
  function that returns the environment where `drake` builds targets.
  Can only be accessed from inside the commands in the workflow plan
  data frame. The primary use case is to allow users to remove
  individual targets from memory at predetermined build steps.

### Bug fixes

- Ensure compatibility with `tibble` 2.0.0.
- Stop returning `0s` from `predict_runtime(targets_only = TRUE)` when
  some targets are outdated and others are not.
- Remove `sort(NULL)` warnings from `create_drake_layout()`. (Affects
  R-3.3.x.)

### Enhancements

- Remove strict dependencies on packages `evaluate`, `formatR`, `fs`,
  `future`, `parallel`, `R.utils`, `stats`, and `stringi`.
- **Large speed boost**: reduce repeated calls to
  [`parse()`](https://rdrr.io/r/base/parse.html) in
  `code_dependencies()`.
- **Large speed boost**: change the default value of `memory_strategy`
  (previously `pruning_strategy`) to `"speed"` (previously
  `"lookahead"`).
- Compute a special data structure in
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  (`config$layout`) just to store the code analysis results. This is an
  intermediate structure between the workflow plan data frame and the
  graph. It will help clean up the internals in future development.
- Improve memoized preprocessing: deparse all the functions in the
  environment so the memoization does not react so spurious changes in R
  internals. Related:
  [\#345](https://github.com/ropensci/drake/issues/345).
- Use the `label` argument to `future()` inside
  `make(parallelism = "future")`. That way , job names are target names
  by default if `job.name` is used correctly in the `batchtools`
  template file.
- Remove strict dependencies on packages `dplyr`, `evaluate`, `fs`,
  `future`, `magrittr`, `parallel`, `R.utils`, `stats`, `stringi`,
  `tidyselect`, and `withr`.
- Remove package `rprojroot` from “Suggests”.
- Deprecate the `force` argument in all functions except
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Change the name of `prune_envir()` to
  [`manage_memory()`](https://docs.ropensci.org/drake/reference/manage_memory.md).
- Deprecate and rename the `pruning_strategy` argument to
  `memory_strategy`
  ([`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)).
- Print warnings and messages to the `console_log_file` in real time
  ([\#588](https://github.com/ropensci/drake/issues/588)).
- Use HTML line breaks in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  hover text to display commands in the `drake` plan more elegantly.
- Speed up
  [`predict_load_balancing()`](https://docs.ropensci.org/drake/reference/predict_load_balancing.md)
  and remove its reliance on internals that will go away in 2019 via
  [\#561](https://github.com/ropensci/drake/issues/561).
- Remove support for the `worker` column of `config$plan` in
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)
  and
  [`predict_load_balancing()`](https://docs.ropensci.org/drake/reference/predict_load_balancing.md).
  This functionality will go away in 2019 via
  [\#561](https://github.com/ropensci/drake/issues/561).
- Change the names of the return value of
  [`predict_load_balancing()`](https://docs.ropensci.org/drake/reference/predict_load_balancing.md)
  to `time` and `workers`.
- Bring the documentation of
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md)
  and
  [`predict_load_balancing()`](https://docs.ropensci.org/drake/reference/predict_load_balancing.md)
  up to date.
- Deprecate
  [`drake_session()`](https://docs.ropensci.org/drake/reference/drake_session.md)
  and rename to
  [`drake_get_session_info()`](https://docs.ropensci.org/drake/reference/drake_get_session_info.md).
- Deprecate the `timeout` argument in the API of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  A value of `timeout` can be still passed to these functions without
  error, but only the `elapsed` and `cpu` arguments impose actual
  timeouts now.

## Version 6.1.0

CRAN release: 2018-10-26

### New features

- **Add a new
  [`map_plan()`](https://docs.ropensci.org/drake/reference/map_plan.md)
  function to easily create a workflow plan data frame to execute a
  function call over a grid of arguments.**
- Add a new
  [`plan_to_code()`](https://docs.ropensci.org/drake/reference/plan_to_code.md)
  function to turn `drake` plans into generic R scripts. New users can
  use this function to better understand the relationship between plans
  and code, and unsatisfied customers can use it to disentangle their
  projects from `drake` altogether. Similarly,
  [`plan_to_notebook()`](https://docs.ropensci.org/drake/reference/plan_to_notebook.md)
  generates an R notebook from a `drake` plan.
- Add a new
  [`drake_debug()`](https://docs.ropensci.org/drake/reference/drake_debug.md)
  function to run a target’s command in debug mode. Analogous to
  [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md).
- Add a `mode` argument to
  [`trigger()`](https://docs.ropensci.org/drake/reference/trigger.md) to
  control how the `condition` trigger factors into the decision to build
  or skip a target. See the
  [`?trigger`](https://docs.ropensci.org/drake/reference/trigger.md) for
  details.
- Add a new `sleep` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  to help the main process consume fewer resources during parallel
  processing.
- Enable the `caching` argument for the `"clustermq"` and
  `"clustermq_staged"` parallel backends. Now,
  `make(parallelism = "clustermq", caching = "main")` will do all the
  caching with the main process, and
  `make(parallelism = "clustermq", caching = "worker")` will do all the
  caching with the workers. The same is true for
  `parallelism = "clustermq_staged"`.
- Add a new `append` argument to
  [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md),
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md),
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md),
  and
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md).
  The `append` argument control whether the output includes the original
  `plan` in addition to the newly generated rows.
- Add new functions
  [`load_main_example()`](https://docs.ropensci.org/drake/reference/load_main_example.md),
  [`clean_main_example()`](https://docs.ropensci.org/drake/reference/clean_main_example.md),
  and
  [`clean_mtcars_example()`](https://docs.ropensci.org/drake/reference/clean_mtcars_example.md).
- Add a `filter` argument to
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md)
  and
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md)
  in order to restrict what we gather even when `append` is `TRUE`.
- Add a hasty mode: `make(parallelism = "hasty")` skips all of `drake`’s
  expensive caching and checking. All targets run every single time and
  you are responsible for saving results to custom output files, but
  almost all the by-target overhead is gone.

### Bug fixes

- Ensure commands in the plan are re-analyzed for dependencies when new
  imports are added
  ([\#548](https://github.com/ropensci/drake/issues/548)). Was a bug in
  version 6.0.0 only.
- Call [`path.expand()`](https://rdrr.io/r/base/path.expand.html) on the
  `file` argument to
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md)
  and
  [`render_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/render_sankey_drake_graph.md).
  That way, tildes in file paths no longer interfere with the rendering
  of static image files.
- Skip tests and examples if the required “Suggests” packages are not
  installed.
- Stop checking for non-standard columns. Previously, warnings about
  non-standard columns were incorrectly triggered by
  `evaluate_plan(trace = TRUE)` followed by
  [`expand_plan()`](https://docs.ropensci.org/drake/reference/expand_plan.md),
  [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md),
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md),
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md),
  or
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md).
  The more relaxed behavior also gives users more options about how to
  construct and maintain their workflow plan data frames.
- Use checksums in `"future"` parallelism to make sure files travel over
  network file systems before proceeding to downstream targets.
- Refactor and clean up checksum code.
- Skip more tests and checks if the optional `visNetwork` package is not
  installed.

### Enhancements

- Stop earlier in
  [`make_targets()`](https://docs.ropensci.org/drake/reference/make_targets.md)
  if all the targets are already up to date.
- Improve the documentation of the `seed` argument in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Set the default `caching` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  to `"main"` rather than `"worker"`. The default option should be the
  lower-overhead option for small workflows. Users have the option to
  make a different set of tradeoffs for larger workflows.
- Allow the `condition` trigger to evaluate to non-logical values as
  long as those values can be coerced to logicals.
- Require that the `condition` trigger evaluate to a vector of length 1.
- Keep non-standard columns in
  [`drake_plan_source()`](https://docs.ropensci.org/drake/reference/drake_plan_source.md).
- `make(verbose = 4)` now prints to the console when a target is stored.
- [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md)
  and
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md)
  now gather/reduce everything if no columns are specified.
- Change the default parallelization of the imports. Previously,
  `make(jobs = 4)` was equivalent to
  `make(jobs = c(imports = 4, targets = 4))`. Now, `make(jobs = 4)` is
  equivalent to `make(jobs = c(imports = 1, targets = 4))`. See issue
  [\#553](https://github.com/ropensci/drake/issues/553) for details.
- Add a console message for building the priority queue when `verbose`
  is at least 2.
- Condense
  [`load_mtcars_example()`](https://docs.ropensci.org/drake/reference/load_mtcars_example.md).
- Deprecate the `hook` argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- In
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md)
  and
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md),
  do not exclude targets with all `NA` gathering variables.

## Version 6.0.0

CRAN release: 2018-09-30

### Breaking changes

- Avoid serialization in `digest()` wherever possible. This puts old
  `drake` projects out of date, but it improves speed.
- Require R version \>= 3.3.0 rather than \>= 3.2.0. Tests and checks
  still run fine on 3.3.0, but the required version of the `stringi`
  package no longer compiles on 3.2.0.
- Be more discerning in detecting dependencies. In
  `code_dependencies()`, restrict the possible global variables to the
  ones mentioned in the new `globals` argument (turned off when `NULL`.
  In practical workflows, global dependencies are restricted to items in
  `envir` and proper targets in the plan. In
  [`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md),
  the `globals` slot of the output list is now a list of *candidate*
  globals, not necessarily actual globals (some may not be targets or
  variables in `envir`).

### Bug fixes

- In the call to [`unlink()`](https://rdrr.io/r/base/unlink.html) in
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md), set
  `recursive` and `force` to `FALSE`. This should prevent the accidental
  deletion of whole directories.
- Previously,
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md)
  deleted input-only files if no targets from the plan were cached. A
  patch and a unit test are included in this release.
- `loadd(not_a_target)` no longer loads every target in the cache.
- Exclude each target from its own dependency metadata in the “deps”
  `igraph` vertex attribute (fixes
  [\#503](https://github.com/ropensci/drake/issues/503)).
- Detect inline code dependencies in
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  file code chunks.
- Remove more calls to `sort(NULL)` that caused warnings in R 3.3.3.
- Fix a bug on R 3.3.3 where `analyze_loadd()` was sometimes quitting
  with “Error: attempt to set an attribute on NULL”.
- Do not call `digest::digest(file = TRUE)` on directories. Instead, set
  hashes of directories to `NA`. Users should still not directories as
  file dependencies.
- If files are declared as dependencies of custom triggers (“condition”
  and “change”) include them in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md).
  Previously, these files were missing from the visualization, but
  actual workflows worked just fine.
- Work around mysterious `codetools` failures in R 3.3 (add a
  [`tryCatch()`](https://rdrr.io/r/base/conditions.html) statement in
  `find_globals()`).

### New features

- Add a proper `clustermq`-based parallel backend:
  `make(parallelism = "clustermq")`.
- `evaluate_plan(trace = TRUE)` now adds a `*_from` column to show the
  origins of the evaluated targets. Try
  `evaluate_plan(drake_plan(x = rnorm(n__), y = rexp(n__)), wildcard = "n__", values = 1:2, trace = TRUE)`.
- Add functions
  [`gather_by()`](https://docs.ropensci.org/drake/reference/gather_by.md)
  and
  [`reduce_by()`](https://docs.ropensci.org/drake/reference/reduce_by.md),
  which gather on custom columns in the plan (or columns generated by
  `evaluate_plan(trace = TRUE)`) and append the new targets to the
  previous plan.
- Expose the `template` argument of `clustermq` functions (e.g. `Q()`
  and `workers()`) as an argument of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Add a new
  [`code_to_plan()`](https://docs.ropensci.org/drake/reference/code_to_plan.md)
  function to turn R scripts and R Markdown reports into workflow plan
  data frames.
- Add a new
  [`drake_plan_source()`](https://docs.ropensci.org/drake/reference/drake_plan_source.md)
  function, which generates lines of code for a
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  call. This
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  call produces the plan passed to
  [`drake_plan_source()`](https://docs.ropensci.org/drake/reference/drake_plan_source.md).
  The main purpose is visual inspection (we even have syntax
  highlighting via `prettycode`) but users may also save the output to a
  script file for the sake of reproducibility or simple reference.
- Deprecate
  [`deps_targets()`](https://docs.ropensci.org/drake/reference/deps_targets.md)
  in favor of a new
  [`deps_target()`](https://docs.ropensci.org/drake/reference/deps_target.md)
  function (singular) that behaves more like
  [`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md).

### Enhancements

- Smooth the edges in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md).
- Make hover text slightly more readable in in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md).
- Align hover text properly in
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  using the “title” node column.
- Optionally collapse nodes into clusters with
  `vis_drake_graph(collapse = TRUE)`.
- Improve
  [`dependency_profile()`](https://docs.ropensci.org/drake/reference/dependency_profile.md)
  show major trigger hashes side-by-side to tell the user if the
  command, a dependency, an input file, or an output file changed since
  the last
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Choose more appropriate places to check that the `txtq` package is
  installed.
- Improve the help files of
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md),
  giving specific usage guidance in prose.
- Memoize all the steps of
  [`build_drake_graph()`](https://docs.ropensci.org/drake/reference/build_drake_graph.md)
  and print to the console the ones that execute.
- Skip some tests if `txtq` is not installed.

## Version 5.4.0

CRAN release: 2018-08-07

- Overhaul the interface for triggers and add new trigger types
  (“condition” and “change”).
- Offload `drake`’s code examples to the `drake-examples` GitHub
  repository and make make
  [`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)
  and
  [`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md)
  download examples from there.
- Optionally show output files in graph visualizations. See the
  `show_output_files` argument to
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and friends.
- Repair output file checksum operations for distributed backends like
  `"clustermq_staged"` and `"future_lapply"`.
- Internally refactor the `igraph` attributes of the dependency graph to
  allow for smarter dependency/memory management during
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Enable
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  and
  [`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md)
  to save static image files via `webshot`.
- Deprecate
  [`static_drake_graph()`](https://docs.ropensci.org/drake/reference/static_drake_graph.md)
  and
  [`render_static_drake_graph()`](https://docs.ropensci.org/drake/reference/render_static_drake_graph.md)
  in favor of
  [`drake_ggraph()`](https://docs.ropensci.org/drake/reference/drake_ggraph.md)
  and
  [`render_drake_ggraph()`](https://docs.ropensci.org/drake/reference/render_drake_ggraph.md).
- Add a `columns` argument to
  [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md)
  so users can evaluate wildcards in columns other than the `command`
  column of `plan`.
- Name the arguments of
  [`target()`](https://docs.ropensci.org/drake/reference/target.md) so
  users do not have to (explicitly).
- Lay the groundwork for a special pretty print method for workflow plan
  data frames.

## Version 5.3.0

CRAN release: 2018-07-19

- Allow multiple output files per command.
- Add Sankey diagram visuals:
  [`sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/sankey_drake_graph.md)
  and
  [`render_sankey_drake_graph()`](https://docs.ropensci.org/drake/reference/render_sankey_drake_graph.md).
- Add
  [`static_drake_graph()`](https://docs.ropensci.org/drake/reference/static_drake_graph.md)
  and
  [`render_static_drake_graph()`](https://docs.ropensci.org/drake/reference/render_static_drake_graph.md)
  for `ggplot2`/`ggraph` static graph visualizations.
- Add `group` and `clusters` arguments to
  [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md),
  [`static_drake_graph()`](https://docs.ropensci.org/drake/reference/static_drake_graph.md),
  and
  [`drake_graph_info()`](https://docs.ropensci.org/drake/reference/drake_graph_info.md)
  to optionally condense nodes into clusters.
- Implement a `trace` argument to
  [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md)
  to optionally add indicator columns to show which targets got
  expanded/evaluated with which wildcard values.
- Rename the `always_rename` argument to `rename` in
  [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md).
- Add a `rename` argument to
  [`expand_plan()`](https://docs.ropensci.org/drake/reference/expand_plan.md).
- Implement `make(parallelism = "clustermq_staged")`, a
  `clustermq`-based staged parallelism backend (see
  [\#452](https://github.com/ropensci/drake/issues/452)).
- Implement `make(parallelism = "future_lapply_staged")`, a
  `future`-based staged parallelism backend (see
  [\#450](https://github.com/ropensci/drake/issues/450)).
- Depend on `codetools` rather than `CodeDepends` for finding global
  variables.
- Detect [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
  and [`readd()`](https://docs.ropensci.org/drake/reference/readd.md)
  dependencies in `knitr` reports referenced with
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  inside imported functions. Previously, this feature was only available
  in explicit
  [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
  calls in commands.
- Skip more tests on CRAN. White-list tests instead of blacklisting them
  in order to try to keep check time under the official 10-minute cap.
- Disallow wildcard names to grep-match other wildcard names or any
  replacement values. This will prevent careless mistakes and confusion
  when generating
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)s.
- Prevent persistent workers from hanging when a target fails.
- Move the example template files to `inst/hpc_template_files`.
- Deprecate
  [`drake_batchtools_tmpl_file()`](https://docs.ropensci.org/drake/reference/drake_batchtools_tmpl_file.md)
  in favor of
  [`drake_hpc_template_file()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_file.md)
  and
  [`drake_hpc_template_files()`](https://docs.ropensci.org/drake/reference/drake_hpc_template_files.md).
- Add a `garbage_collection` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md). If
  `TRUE`, [`gc()`](https://rdrr.io/r/base/gc.html) is called after every
  new build of a target.
- Remove redundant calls to `sanitize_plan()` in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
- Change
  [`tracked()`](https://docs.ropensci.org/drake/reference/tracked.md) to
  accept only a
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  object as an argument. Yes, it is technically a breaking change, but
  it is only a small break, and it is the correct API choice.
- Move visualization and hpc package dependencies to “Suggests:” rather
  than “Imports:” in the `DESCRIPTION` file.
- Allow processing of codeless `knitr` reports without warnings.

## Version 5.2.1

CRAN release: 2018-06-19

- Skip several long-running and low-priority tests on CRAN.

## Version 5.2.0

- Sequester staged parallelism in backends “mclapply_staged” and
  “parLapply_staged”. For the other `lapply`-like backends, `drake` uses
  persistent workers and a main process. In the case of
  `"future_lapply"` parallelism, the main process is a separate
  background process called by `Rscript`.
- Remove the appearance of staged parallelism from single-job
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)’s.
  (Previously, there were “check” messages and a call to
  `staged_parallelism()`.)
- Remove some remnants of staged parallelism internals.
- Allow different parallel backends for imports vs targets. For example,
  `make(parallelism = c(imports = "mclapply_staged", targets = "mclapply")`.
- Fix a bug in environment pruning. Previously, dependencies of
  downstream targets were being dropped from memory in `make(jobs = 1)`.
  Now, they are kept in memory until no downstream target needs them
  (for `make(jobs = 1)`).
- Improve
  [`predict_runtime()`](https://docs.ropensci.org/drake/reference/predict_runtime.md).
  It is a more sensible way to go about predicting runtimes with
  multiple jobs. Likely to be more accurate.
- Calls to [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  no longer leave targets in the user’s environment.
- Attempt to fix a Solaris CRAN check error. A test was previously
  failing on CRAN’s Solaris machine (R 3.5.0). In the test, one of the
  threads deliberately quits in error, and the R/Solaris installation
  did not handle this properly. The test should work now because it no
  longer uses any parallelism.
- Deprecate the `imports_only` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  in favor of `skip_targets`.
- Deprecate
  [`migrate_drake_project()`](https://docs.ropensci.org/drake/reference/migrate_drake_project.md).
- Deprecate
  [`max_useful_jobs()`](https://docs.ropensci.org/drake/reference/max_useful_jobs.md).
- For non-distributed parallel backends, stop waiting for all the
  imports to finish before the targets begin.
- Add an `upstream_only` argument to
  [`failed()`](https://docs.ropensci.org/drake/reference/failed.md) so
  users can list failed targets that do not have any failed
  dependencies. Naturally accompanies `make(keep_going = TRUE)`.
- Add an RStudio R Markdown template.
- Remove `plyr` as a dependency.
- Handle duplicated targets better in
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  and
  [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md).
- Add a true function
  [`target()`](https://docs.ropensci.org/drake/reference/target.md) to
  help create drake plans with custom columns.
- In
  [`drake_gc()`](https://docs.ropensci.org/drake/reference/drake_gc.md),
  clean out disruptive files in `storr`s with mangled keys (re:
  [\#198](https://github.com/ropensci/drake/issues/198)).
- Move all the vignettes to the up and coming user manual.
- Rename the “basic example” to the “mtcars example”.
- Deprecate
  [`load_basic_example()`](https://docs.ropensci.org/drake/reference/load_basic_example.md)
  in favor of
  [`load_mtcars_example()`](https://docs.ropensci.org/drake/reference/load_mtcars_example.md).
- Refocus the `README.md` file on the main example rather than the
  mtcars example.
- Use a `README.Rmd` file to generate `README.md`.
- Add function
  [`deps_targets()`](https://docs.ropensci.org/drake/reference/deps_targets.md).
- Deprecate function
  [`deps()`](https://docs.ropensci.org/drake/reference/deps.md) in favor
  of
  [`deps_code()`](https://docs.ropensci.org/drake/reference/deps_code.md)
- Add a `pruning_strategy` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  so the user can decide how `drake` keeps non-import dependencies in
  memory when it builds a target.
- Add optional custom (experimental) “workers” and “priorities” columns
  to the `drake` plans to help users customize scheduling.
- Add a `makefile_path` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  to avoid potential conflicts between user-side custom `Makefile`s and
  the one written by `make(parallelism = "Makefile")`.
- Document batch mode for long workflows in the HPC guide.
- Add a `console` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  so users can redirect console output to a file.
- Make it easier for the user to find out where a target in the cache
  came from:
  [`show_source()`](https://docs.ropensci.org/drake/reference/show_source.md),
  `readd(show_source = TRUE)`, `loadd(show_source = TRUE)`.

## Version 5.1.2

CRAN release: 2018-04-10

- In R 3.5.0, the `!!` operator from tidyeval and `rlang` is parsed
  differently than in R \<= 3.4.4. This change broke one of the tests in
  `tests/testthat/tidy-eval.R` The main purpose of `drake`’s 5.1.2
  release is to fix the broken test.
- Fix an elusive `R CMD check` error from building the pdf manual with
  LaTeX.
- In
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md),
  allow users to customize target-level columns using
  [`target()`](https://docs.ropensci.org/drake/reference/target.md)
  inside the commands.
- Add a new
  [`bind_plans()`](https://docs.ropensci.org/drake/reference/bind_plans.md)
  function to concatenate the rows of drake plans and then sanitize the
  aggregate plan.
- Add an optional `session` argument to tell
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) to build
  targets in a separate, isolated main R session. For example,
  `make(session = callr::r_vanilla)`.

## Version 5.1.0

CRAN release: 2018-03-22

- Add a
  [`reduce_plan()`](https://docs.ropensci.org/drake/reference/reduce_plan.md)
  function to do pairwise reductions on collections of targets.
- Forcibly exclude the dot (`.`) from being a dependency of any target
  or import. This enforces more consistent behavior in the face of the
  current static code analysis functionality, which sometimes detects
  `.` and sometimes does not.
- Use [`ignore()`](https://docs.ropensci.org/drake/reference/ignore.md)
  to optionally ignore pieces of workflow plan commands and/or imported
  functions. Use `ignore(some_code)` to
  1.  Force `drake` to not track dependencies in `some_code`, and
  2.  Ignore any changes in `some_code` when it comes to deciding which
      target are out of date.
- Force `drake` to only look for imports in environments inheriting from
  `envir` in
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) (plus
  explicitly namespaced functions).
- Force [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
  to ignore foreign imports (imports not explicitly found in `envir`
  when [`make()`](https://docs.ropensci.org/drake/reference/make.md)
  last imported them).
- Reduce default verbosity. Only targets are printed out by default.
  Verbosity levels are integers ranging from 0 through 4.
- Change [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md)
  so that only targets (not imports) are loaded if the `...` and `list`
  arguments are empty.
- Add check to drake_plan() to check for duplicate targets
- Add a `.gitignore` file containing `"*"` to the default `.drake/`
  cache folder every time
  [`new_cache()`](https://docs.ropensci.org/drake/reference/new_cache.md)
  is called. This means the cache will not be automatically committed to
  git. Users need to remove `.gitignore` file to allow unforced commits,
  and then subsequent
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)s on the
  same cache will respect the user’s wishes and not add another
  `.gitignore`. this only works for the default cache. Not supported for
  manual `storr`s.
- Add a new experimental `"future"` backend with a manual scheduler.
- Implement `dplyr`-style `tidyselect` functionality in
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md),
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md), and
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md).
  For
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md),
  there is an API change: for `tidyselect` to work, we needed to insert
  a new `...` argument as the first argument of
  [`build_times()`](https://docs.ropensci.org/drake/reference/build_times.md).
- Deprecate the single-quoting API for files. Users should now use
  formal API functions in their commands:
  - [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
    for file inputs to commands or imported functions (for imported
    functions, the input file needs to be an imported file, not a
    target).
  - [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)
    for output file targets (ignored if used in imported functions).
  - [`knitr_in()`](https://docs.ropensci.org/drake/reference/knitr_in.md)
    for `knitr`/`rmarkdown` reports. This tells `drake` to look inside
    the source file for target dependencies in code chunks (explicitly
    referenced with
    [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
    [`readd()`](https://docs.ropensci.org/drake/reference/readd.md)).
    Treated as a
    [`file_in()`](https://docs.ropensci.org/drake/reference/file_in.md)
    if used in imported functions.
- Change
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  so that it automatically fills in any target names that the user does
  not supply. Also, any
  [`file_out()`](https://docs.ropensci.org/drake/reference/file_out.md)s
  become the target names automatically (double-quoted internally).
- Make
  [`read_drake_plan()`](https://docs.ropensci.org/drake/reference/read_drake_plan.md)
  (rather than an empty
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md))
  the default `plan` argument in all functions that accept a `plan`.
- Add support for active bindings: `loadd(..., lazy = "bind")`. That
  way, when you have a target loaded in one R session and hit
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) in
  another R session, the target in your first session will automatically
  update.
- Use tibbles for workflow plan data frames and the output of
  [`dataframes_graph()`](https://docs.ropensci.org/drake/reference/dataframes_graph.md).
- Return warnings, errors, and other context of each build, all wrapped
  up with the usual metadata.
  [`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md)
  will take on the role of returning this metadata.
- Deprecate the
  [`read_drake_meta()`](https://docs.ropensci.org/drake/reference/read_drake_meta.md)
  function in favor of
  [`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md).
- Add a new
  [`expose_imports()`](https://docs.ropensci.org/drake/reference/expose_imports.md)
  function to optionally force `drake` detect deeply nested functions
  inside specific packages.
- Move the “quickstart.Rmd” vignette to “example-basic.Rmd”. The
  so-called “quickstart” didn’t end up being very quick, and it was all
  about the basic example anyway.
- Move
  [`drake_build()`](https://docs.ropensci.org/drake/reference/drake_build.md)
  to be an exclusively user-side function.
- Add a `replace` argument to
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) so
  that objects already in the user’s environment need not be replaced.
- When the graph cyclic, print out all the cycles.
- Prune self-referential loops (and duplicate edges) from the workflow
  graph. That way, recursive functions are allowed.
- Add a `seed` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md),
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md),
  and
  [`load_basic_example()`](https://docs.ropensci.org/drake/reference/load_basic_example.md).
  Also hard-code a default seed of `0`. That way, the pseudo-randomness
  in projects should be reproducible across R sessions.
- Cache the pseudo-random seed at the time the project is created and
  use that seed to build targets until the cache is destroyed.
- Add a new `drake_read_seed()` function to read the seed from the
  cache. Its examples illustrate what `drake` is doing to try to ensure
  reproducible random numbers.
- Evaluate the quasiquotation operator `!!` for the `...` argument to
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md).
  Suppress this behavior using `tidy_evaluation = FALSE` or by passing
  in commands passed through the `list` argument.
- Preprocess workflow plan commands with
  [`rlang::expr()`](https://rlang.r-lib.org/reference/expr.html) before
  evaluating them. That means you can use the quasiquotation operator
  `!!` in your commands, and
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) will
  evaluate them according to the tidy evaluation paradigm.
- Restructure `drake_example("basic")`, `drake_example("gsp")`, and
  `drake_example("packages")` to demonstrate how to set up the files for
  serious `drake` projects. More guidance was needed in light of
  [\#193](https://github.com/ropensci/drake/issues/193).
- Improve the examples of
  [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  in the help file
  ([`?drake_plan`](https://docs.ropensci.org/drake/reference/drake_plan.md)).

## Version 5.0.0

CRAN release: 2018-01-26

- Transfer `drake` to rOpenSci GitHub URL.
- Several functions now require an explicit `config` argument, which you
  can get from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  or [`make()`](https://docs.ropensci.org/drake/reference/make.md).
  Examples:
  - outdated()
  - missed()
  - rate_limiting_times()
  - predict_runtime()
  - vis_drake_graph()
  - dataframes_graph()
- Always process all the imports before building any targets. This is
  part of the solution to
  [\#168](https://github.com/ropensci/drake/issues/168): if imports and
  targets are processed together, the full power of parallelism is taken
  away from the targets. Also, the way parallelism happens is now
  consistent for all parallel backends.
- Major speed improvement: dispense with internal inventories and rely
  on `cache$exists()` instead.
- Let the user define a trigger for each target to customize when
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) decides
  to build targets.
- Document triggers and other debugging/testing tools in the new “debug”
  vignette.
- Restructure the internals of the `storr` cache in a way that is not
  back-compatible with projects from versions 4.4.0 and earlier. The
  main change is to make more intelligent use of `storr` namespaces,
  improving efficiency (both time and storage) and opening up
  possibilities for new features. If you attempt to run drake \>= 5.0.0
  on a project from drake \<= 4.0.0, drake will stop you before any
  damage to the cache is done, and you will be instructed how to migrate
  your project to the new drake.
- Use `formatR::tidy_source()` instead of
  [`parse()`](https://rdrr.io/r/base/parse.html) in `tidy_command()`
  (originally `tidy()` in `R/dependencies.R`). Previously, `drake` was
  having problems with an edge case: as a command, the literal string
  `"A"` was interpreted as the symbol `A` after tidying. With
  `tidy_source()`, literal quoted strings stay literal quoted strings in
  commands. This may put some targets out of date in old projects, yet
  another loss of back compatibility in version 5.0.0.
- Speed up clean() by refactoring the cache inventory and using light
  parallelism.
- Implement
  [`rescue_cache()`](https://docs.ropensci.org/drake/reference/rescue_cache.md),
  exposed to the user and used in
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md). This
  function removes dangling orphaned files in the cache so that a broken
  cache can be cleaned and used in the usual ways once more.
- Change the default `cpu` and `elapsed` arguments of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) to
  `NULL`. This solves an elusive bug in how drake imposes timeouts.
- Allow users to set target-level timeouts (overall, cpu, and elapsed)
  with columns in the workflow plan data frame.
- Document timeouts and retries in the new “debug” vignette.
- Add a new `graph` argument to functions
  [`make()`](https://docs.ropensci.org/drake/reference/make.md),
  [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md),
  and [`missed()`](https://docs.ropensci.org/drake/reference/missed.md).
- Export a new `prune_graph()` function for igraph objects.
- Delete long-deprecated functions `prune()` and `status()`.
- Deprecate and rename functions:
  - [`analyses()`](https://docs.ropensci.org/drake/reference/analyses.md)
    =\>
    [`plan_analyses()`](https://docs.ropensci.org/drake/reference/plan_analyses.md)
  - [`as_file()`](https://docs.ropensci.org/drake/reference/as_file.md)
    =\>
    [`as_drake_filename()`](https://docs.ropensci.org/drake/reference/as_drake_filename.md)
  - [`backend()`](https://docs.ropensci.org/drake/reference/backend.md)
    =\>
    [`future::plan()`](https://future.futureverse.org/reference/plan.html)
  - [`build_graph()`](https://docs.ropensci.org/drake/reference/build_graph.md)
    =\>
    [`build_drake_graph()`](https://docs.ropensci.org/drake/reference/build_drake_graph.md)
  - [`check()`](https://docs.ropensci.org/drake/reference/check.md) =\>
    [`check_plan()`](https://docs.ropensci.org/drake/reference/check_plan.md)
  - [`config()`](https://docs.ropensci.org/drake/reference/config.md)
    =\>
    [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md)
  - [`evaluate()`](https://docs.ropensci.org/drake/reference/evaluate.md)
    =\>
    [`evaluate_plan()`](https://docs.ropensci.org/drake/reference/evaluate_plan.md)
  - [`example_drake()`](https://docs.ropensci.org/drake/reference/example_drake.md)
    =\>
    [`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)
  - [`examples_drake()`](https://docs.ropensci.org/drake/reference/examples_drake.md)
    =\>
    [`drake_examples()`](https://docs.ropensci.org/drake/reference/drake_examples.md)
  - [`expand()`](https://docs.ropensci.org/drake/reference/expand.md)
    =\>
    [`expand_plan()`](https://docs.ropensci.org/drake/reference/expand_plan.md)
  - [`gather()`](https://docs.ropensci.org/drake/reference/gather.md)
    =\>
    [`gather_plan()`](https://docs.ropensci.org/drake/reference/gather_plan.md)
  - [`plan()`](https://docs.ropensci.org/drake/reference/plan.md),
    [`workflow()`](https://docs.ropensci.org/drake/reference/workflow.md),
    [`workplan()`](https://docs.ropensci.org/drake/reference/workplan.md)
    =\>
    [`drake_plan()`](https://docs.ropensci.org/drake/reference/drake_plan.md)
  - [`plot_graph()`](https://docs.ropensci.org/drake/reference/plot_graph.md)
    =\>
    [`vis_drake_graph()`](https://docs.ropensci.org/drake/reference/vis_drake_graph.md)
  - [`read_config()`](https://docs.ropensci.org/drake/reference/read_config.md)
    =\>
    [`read_drake_config()`](https://docs.ropensci.org/drake/reference/read_drake_config.md)
  - [`read_graph()`](https://docs.ropensci.org/drake/reference/read_graph.md)
    =\>
    [`read_drake_graph()`](https://docs.ropensci.org/drake/reference/read_drake_graph.md)
  - [`read_plan()`](https://docs.ropensci.org/drake/reference/read_plan.md)
    =\>
    [`read_drake_plan()`](https://docs.ropensci.org/drake/reference/read_drake_plan.md)
  - [`render_graph()`](https://docs.ropensci.org/drake/reference/render_graph.md)
    =\>
    [`render_drake_graph()`](https://docs.ropensci.org/drake/reference/render_drake_graph.md)
  - [`session()`](https://docs.ropensci.org/drake/reference/session.md)
    =\>
    [`drake_session()`](https://docs.ropensci.org/drake/reference/drake_session.md)
  - [`summaries()`](https://docs.ropensci.org/drake/reference/summaries.md)
    =\>
    [`plan_summaries()`](https://docs.ropensci.org/drake/reference/plan_summaries.md)
- Disallow `output` and `code` as names in the workflow plan data frame.
  Use `target` and `command` instead. This naming switch has been
  formally deprecated for several months prior.
- Deprecate the ..analysis.. and ..dataset.. wildcards in favor of
  analysis\_\_ and dataset\_\_, respectively. The new wildcards are
  stylistically better an pass linting checks.
- Add new functions
  [`drake_quotes()`](https://docs.ropensci.org/drake/reference/drake_quotes.md),
  [`drake_unquote()`](https://docs.ropensci.org/drake/reference/drake_unquote.md),
  and
  [`drake_strings()`](https://docs.ropensci.org/drake/reference/drake_strings.md)
  to remove the silly dependence on the `eply` package.
- Add a `skip_safety_checks` flag to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
  Increases speed.
- In `sanitize_plan()`, remove rows with blank targets ““.
- Add a `purge` argument to
  [`clean()`](https://docs.ropensci.org/drake/reference/clean.md) to
  optionally remove all target-level information.
- Add a `namespace` argument to
  [`cached()`](https://docs.ropensci.org/drake/reference/cached.md) so
  users can inspect individual `storr` namespaces.
- Change `verbose` to numeric: 0 = print nothing, 1 = print progress on
  imports only, 2 = print everything.
- Add a new `next_stage()` function to report the targets to be made in
  the next parallelizable stage.
- Add a new `session_info` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).
  Apparently,
  [`sessionInfo()`](https://rdrr.io/r/utils/sessionInfo.html) is a
  bottleneck for small
  [`make()`](https://docs.ropensci.org/drake/reference/make.md)s, so
  there is now an option to suppress it. This is mostly for the sake of
  speeding up unit tests.
- Add a new `log_progress` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) to
  suppress progress logging. This increases storage efficiency and
  speeds some projects up a tiny bit.
- Add an optional `namespace` argument to
  [`loadd()`](https://docs.ropensci.org/drake/reference/readd.md) and
  [`readd()`](https://docs.ropensci.org/drake/reference/readd.md). You
  can now load and read from non-default `storr` namespaces.
- Add
  [`drake_cache_log()`](https://docs.ropensci.org/drake/reference/drake_cache_log.md),
  [`drake_cache_log_file()`](https://docs.ropensci.org/drake/reference/drake_cache_log_file.md),
  and `make(..., cache_log_file = TRUE)` as options to track changes to
  targets/imports in the drake cache.
- Detect knitr code chunk dependencies in response to commands with
  [`rmarkdown::render()`](https://pkgs.rstudio.com/rmarkdown/reference/render.html),
  not just [`knit()`](https://rdrr.io/pkg/knitr/man/knit.html).
- Add a new general best practices vignette to clear up misconceptions
  about how to use `drake` properly.

## Version 4.4.0

CRAN release: 2017-11-05

- Extend
  [`plot_graph()`](https://docs.ropensci.org/drake/reference/plot_graph.md)
  to display subcomponents. Check out arguments `from`, `mode`, `order`,
  and `subset`. The graph visualization vignette has demonstrations.
- Add `"future_lapply"` parallelism: parallel backends supported by the
  `future` and `future.batchtools` packages. See
  [`?backend`](https://docs.ropensci.org/drake/reference/backend.md) for
  examples and the parallelism vignette for an introductory tutorial.
  More advanced instruction can be found in the `future` and
  `future.batchtools` packages themselves.
- Cache diagnostic information of targets that fail and retrieve
  diagnostic info with
  [`diagnose()`](https://docs.ropensci.org/drake/reference/diagnose.md).
- Add an optional `hook` argument to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) to wrap
  around `build()`. That way, users can more easily control the side
  effects of distributed jobs. For example, to redirect error messages
  to a file in
  `make(..., parallelism = "Makefile", jobs = 2, hook = my_hook)`,
  `my_hook` should be something like
  `function(code){withr::with_message_sink("messages.txt", code)}`.
- Remove console logging for “parLapply” parallelism. `drake` was
  previously using the `outfile` argument for PSOCK clusters to generate
  output that could not be caught by
  [`capture.output()`](https://rdrr.io/r/utils/capture.output.html). It
  was a hack that should have been removed before.
- Remove console logging for “parLapply” parallelism. `drake` was
  previously using the `outfile` argument for PSOCK clusters to generate
  output that could not be caught by
  [`capture.output()`](https://rdrr.io/r/utils/capture.output.html). It
  was a hack that should have been removed before.
- If ‘verbose’ is ‘TRUE’ and all targets are already up to date (nothing
  to build), then
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) and
  [`outdated()`](https://docs.ropensci.org/drake/reference/outdated.md)
  print “All targets are already up to date” to the console.
- Add new examples in ‘inst/examples’, most of them demonstrating how to
  use the `"future_lapply"` backends.
- New support for timeouts and retries when it comes to building
  targets.
- Failed targets are now recorded during the build process. You can see
  them in
  [`plot_graph()`](https://docs.ropensci.org/drake/reference/plot_graph.md)
  and
  [`progress()`](https://docs.ropensci.org/drake/reference/progress.md).
  Also see the new
  [`failed()`](https://docs.ropensci.org/drake/reference/failed.md)
  function, which is similar to
  [`in_progress()`](https://docs.ropensci.org/drake/reference/in_progress.md).
- Speed up the overhead of `parLapply` parallelism. The downside to this
  fix is that `drake` has to be properly installed. It should not be
  loaded with `devtools::load_all()`. The speedup comes from lightening
  the first `clusterExport()` call in `run_parLapply()`. Previously, we
  exported every single individual `drake` function to all the workers,
  which created a bottleneck. Now, we just load `drake` itself in each
  of the workers, which works because `build()` and
  [`do_prework()`](https://docs.ropensci.org/drake/reference/do_prework.md)
  are exported.
- Change default value of `overwrite` to `FALSE` in
  [`load_basic_example()`](https://docs.ropensci.org/drake/reference/load_basic_example.md).
- Warn when overwriting an existing `report.Rmd` in
  [`load_basic_example()`](https://docs.ropensci.org/drake/reference/load_basic_example.md).
- Tell the user the location of the cache using a console message.
  Happens on every call to `get_cache(..., verbose = TRUE)`.
- Increase efficiency of internal preprocessing via
  `lightly_parallelize()` and `lightly_parallelize_atomic()`. Now,
  processing happens faster, and only over the unique values of a
  vector.
- Add a new
  [`make_with_config()`](https://docs.ropensci.org/drake/reference/make_with_config.md)
  function to do the work of
  [`make()`](https://docs.ropensci.org/drake/reference/make.md) on an
  existing internal configuration list from
  [`drake_config()`](https://docs.ropensci.org/drake/reference/drake_config.md).
- Add a new function
  [`drake_batchtools_tmpl_file()`](https://docs.ropensci.org/drake/reference/drake_batchtools_tmpl_file.md)
  to write a `batchtools` template file from one of the examples
  ([`drake_example()`](https://docs.ropensci.org/drake/reference/drake_example.md)),
  if one exists.

## Version 4.3.0: 2017-10-17

CRAN release: 2017-10-18

Version 4.3.0 has: - Reproducible random numbers
([\#56](https://github.com/ropensci/drake/issues/56)) - Automatic
detection of knitr dependencies
([\#9](https://github.com/ropensci/drake/issues/9)) - More vignettes -
Bug fixes

## Version 4.2.0: 2017-09-29

CRAN release: 2017-09-29

Version 4.2.0 will be released today. There are several improvements to
code style and performance. In addition, there are new features such as
cache/hash externalization and runtime prediction. See the new storage
and timing vignettes for details. This release has automated checks for
back-compatibility with existing projects, and I also did manual back
compatibility checks on serious projects.

## Version 3.0.0: 2017-05-03

CRAN release: 2017-05-09

Version 3.0.0 is coming out. It manages environments more intelligently
so that the behavior of
[`make()`](https://docs.ropensci.org/drake/reference/make.md) is more
consistent with evaluating your code in an interactive session.

## Version 1.0.1: 2017-02-28

CRAN release: 2017-02-27

Version 1.0.1 is on CRAN! I’m already working on a massive update,
though. 2.0.0 is cleaner and more powerful.
