# Setup cache path

Setup cache path

## Usage

``` r
cache_setup(full_path = NULL, temp_dir = FALSE)

cache_info()
```

## Arguments

- full_path:

  (character) the full path to use for storing cached files.

- temp_dir:

  (logical) if `TRUE` use a randomly assigned `tempdir` (and `full_path`
  is ignored), if `FALSE`, you can use `full_path`.

## Value

the full cache path, a directory (character)

## Details

On opening, by default a temporary directory is created for caching
files. To have files cached elsewhere, give the full path of where to
cache files. Adding `temp_dir = TRUE` will again use a temporary
dirctory for cacheing.

## See also

Other cache:
[`cache_delete()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md),
[`cache_details()`](https://docs.ropensci.org/rerddap/reference/cache_details.md),
[`cache_list()`](https://docs.ropensci.org/rerddap/reference/cache_list.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# default path
cache_setup()

# you can define your own path
cache_setup(path = "foobar")

# set a tempdir - better for programming with to avoid prompt
cache_setup(temp_dir = TRUE)

# cache info
cache_info()
} # }
```
