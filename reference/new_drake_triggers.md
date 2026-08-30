# `drake_triggers` constructor

List of class `drake_triggers`.

## Usage

``` r
new_drake_triggers(
  command = TRUE,
  depend = TRUE,
  file = TRUE,
  seed = TRUE,
  format = TRUE,
  condition = FALSE,
  change = NULL,
  mode = "whitelist"
)
```

## Arguments

- command:

  Logical, command trigger.

- depend:

  Logical, depend trigger.

- file:

  Logical, file trigger.

- seed:

  Logical, seed trigger.

- format:

  Logical, format trigger.

- condition:

  Language object or object coercible to logical, condition trigger.

- change:

  Language object or literal value, change trigger.

- mode:

  Character, mode of condition trigger.

## Value

A `drake_triggers` object.

## Examples

``` r
if (FALSE) { # stronger than roxygen dontrun
new_drake_triggers()
}
```
