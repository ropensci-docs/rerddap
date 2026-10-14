# List cached files

List cached files

## Usage

``` r
cache_list()
```

## See also

Other cache:
[`cache_delete()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md),
[`cache_details()`](https://docs.ropensci.org/rerddap/reference/cache_details.md),
[`cache_setup()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# list files in cache
cache_list()

# List info for files
## download some data first
tabledap('erdCinpKfmBT')
griddap('erdVHNchlamday',
 time = c('2015-04-01','2015-04-10'),
 latitude = c(18, 21),
 longitude = c(-120, -119)
)

(x <- cache_list())
cache_details(x$nc[1])
cache_details(x$csv[1])
cache_details()

# delete files by name in cache
# cache_delete(x$nc[1])
# cache_delete(x$nc[2:3])
} # }
```
