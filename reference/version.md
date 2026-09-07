# Get ERDDAP™ version

Get ERDDAP™ version

## Usage

``` r
version(url = eurl(), ...)
```

## Arguments

- url:

  A URL for an ERDDAP™ server. Default:
  https://upwell.pfeg.noaa.gov/erddap/ - See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Examples

``` r
if (FALSE) { # \dontrun{
version()
ss <- servers()
version(ss$url[2])
version(ss$url[3])
} # }
```
