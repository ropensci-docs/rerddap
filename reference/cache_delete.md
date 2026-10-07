# Delete cached files

Delete cached files

## Usage

``` r
cache_delete(x, force = FALSE)

cache_delete_all(force = FALSE)
```

## Arguments

- x:

  File names

- force:

  (logical) Should files be force deleted? Default: `FALSE`

## See also

Other cache:
[`cache_details()`](https://docs.ropensci.org/rerddap/reference/cache_details.md),
[`cache_list()`](https://docs.ropensci.org/rerddap/reference/cache_list.md),
[`cache_setup()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# delete files by name in cache
# cache_delete('9911750294a039b8b517c8bf288978ea.csv')
# cache_delete(c('9911750294a039b8b517c8bf288978ea.csv',
#                'b26825b6737da13d6a52c28c8dfe690f.csv'))

# You can delete from the output of griddap or tabledap fxns
## tabledap
(table_res <- tabledap('erdCinpKfmBT'))
cache_delete(table_res)

## griddap
(out <- info('erdQMekm14day'))
(grid_res <- griddap(out,
 time = c('2015-12-28','2016-01-01'),
 latitude = c(24, 23),
 longitude = c(88, 90)
))
cache_delete(grid_res)
} # }
```
