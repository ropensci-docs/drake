# Loadd target at cursor into global environment **\[stable\]**

This function provides an RStudio addin that will load the target at the
current cursor location from the cache into the global environment. This
is convenient during pipeline development when building off established
targets.

## Usage

``` r
rs_addin_loadd(context = NULL)
```

## Arguments

- context:

  an RStudio document context. Read from the active document if not
  supplied. This is used for testing purposes.

## Value

Nothing.

## Details

If you are using a non-standard `drake` cache, you must supply it to the
`"rstudio_drake_cache"` global option, e.g.
`options(rstudio_drake_cache = storr::storr_rds("my_cache"))`.
