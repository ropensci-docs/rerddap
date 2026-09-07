# Options for saving ERDDAP™ datasets.

Options for saving ERDDAP™ datasets.

## Usage

``` r
disk(path = NULL, overwrite = TRUE)

memory()
```

## Arguments

- path:

  Path to store files in. A directory, not a file. Default: the root
  cache path, see
  [`cache_setup`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)

- overwrite:

  (logical) Overwrite an existing file of the same name? Default: `TRUE`
