# Static code analysis

Static code analysis.

## Usage

``` r
walk_code(expr, results, locals, restrict)
```

## Arguments

- expr:

  A function or expression.

- results:

  A `drake_deps` object.

- locals:

  An environment, a hash table of local variables.

- restrict:

  An environment, a hash table for whitelisting global symbols.
