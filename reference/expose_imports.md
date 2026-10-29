# Deprecated: expose package functions and objects for analysis with drake. **\[deprecated\]**

Deprecated on 2020-06-24.

## Usage

``` r
expose_imports(
  package,
  character_only = FALSE,
  envir = parent.frame(),
  jobs = 1
)
```

## Arguments

- package:

  Name of the package, either a symbol or a string, depending on
  `character_only`.

- character_only:

  Logical, whether to interpret `package` as a character string or a
  symbol (quoted vs unquoted).

- envir:

  Environment to load the exposed package imports. You will later pass
  this `envir` to
  [`make()`](https://docs.ropensci.org/drake/reference/make.md).

- jobs:

  Number of parallel jobs for the parallel processing of the imports.

## Value

The environment that the exposed imports are loaded into. Defaults to
your R workspace.

## Details

Deprecated. This function assigns the objects and functions from the
package environment to the user's environment (usually global) so
`drake` can watch them for changes. This used to be the standard way to
make `drake` compatible with workflows implemented as custom analysis
packages. Now, the recommendation is to supply
`getNamespace("yourPackage")` to the `envir` argument of
[`make()`](https://docs.ropensci.org/drake/reference/make.md) and
friends. Read `https://github.com/ropensci/drake/issues/1286`,
especially
`https://github.com/ropensci/drake/issues/1286#issuecomment-649088321`,
\# nolint for details.

## Examples

``` r
# nolint start
if (FALSE) { # \dontrun{
isolate_example("contain side effects", {
# Consider a simple plan that depends on the biglm package.
# library(biglm)
plan <- drake_plan(model = biglm(y ~ x, data = huge_dataset))
# Even if you load the biglm package, drake still ignores
# the biglm() function as a dependency. The function is missing
# from the graph:
# vis_drake_graph(plan)
# And if you install an updated version of biglm with a revised
# biglm() function, this will not cause drake::make(plan)
# to rerun the model.
# This is because biglm() is not in your environment.
# ls()
# biglm() exists in its own special package environment,
# which drake does not scan.
# ls("package:biglm")
# To depend on biglm(), use expose_imports(biglm)
# to bring the objects and functions in biglm into
# your own (non-package) environment.
# expose_imports(biglm)
# Now, the biglm() function should be in your environment.
# ls()
# biglm() now appears in the graph.
# vis_drake_graph(plan)
# And subsequent make()s respond to changes to biglm()
# and its dependencies.
})
} # }
# nolint end
```
