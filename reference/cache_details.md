# Get details of cached files

Get details of cached files

## Usage

``` r
cache_details(x)
```

## Arguments

- x:

  File names

## Details

Can be used to list details for all files, both .nc and .csv types, or
details for just individual files of class `tabledap`, `griddap_nc`, and
`griddap_csv`

## See also

Other cache:
[`cache_delete()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md),
[`cache_list()`](https://docs.ropensci.org/rerddap/reference/cache_list.md),
[`cache_setup()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# List details for all cached files
cache_details()
} # }
```
