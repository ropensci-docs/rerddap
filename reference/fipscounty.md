# Convert a FIPS County Code to/from a County Name

Convert a FIPS County Code to/from a County Name

## Usage

``` r
fipscounty(county = NULL, code = NULL, url = eurl(), ...)
```

## Arguments

- county:

  character; A county name.

- code:

  numeric; A FIPS code.

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
fipscounty(code = "06053")
fipscounty(county = "CA, Monterey")
fipscounty(county = "OR, Multnomah")
} # }
```
