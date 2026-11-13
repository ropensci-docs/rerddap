# Search for ERDDAP™ tabledep or griddap datasets

Search for ERDDAP™ tabledep or griddap datasets

## Usage

``` r
ed_search(
  query,
  page = NULL,
  page_size = NULL,
  which = "griddap",
  url = eurl(),
  ...
)

ed_datasets(which = "tabledap", url = eurl())
```

## Arguments

- query:

  (character) Search terms

- page:

  (integer) Page number

- page_size:

  (integer) Results per page

- which:

  (character) One of tabledep or griddap.

- url:

  A URL for an ERDDAP™ server. Default:
  https://upwell.pfeg.noaa.gov/erddap/ - See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)
  (must be named parameters)

## References

https://upwell.pfeg.noaa.gov/erddap/index.html

## Examples

``` r
if (FALSE) { # \dontrun{
(out <- ed_search(query='temperature'))
out$alldata[[1]]
(out <- ed_search(query='size'))
out$info

# List datasets
ed_datasets('table')
ed_datasets('grid')

# use a different ERDDAP™ server
## Marine Institute (Ireland)
ed_search("temperature", url = "http://erddap.marine.ie/erddap/")
} # }
```
