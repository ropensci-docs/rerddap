# Convert a CF Standard Name to/from a GCMD Science Keyword

Convert a CF Standard Name to/from a GCMD Science Keyword

## Usage

``` r
key_words(cf = NULL, gcmd = NULL, url = eurl(), ...)
```

## Arguments

- cf:

  character; A cf standard name
  http://cfconventions.org/Data/cf-standard-names/27/build/cf-standard-name-table.html

- gcmd:

  character; A GCMD science keyword
  http://gcmd.gsfc.nasa.gov/learn/keyword_list.html

- url:

  A URL for an ERDDAP™ server. Default:
  https://upwell.pfeg.noaa.gov/erddap/. See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Examples

``` r
 if (FALSE) { # \dontrun{
key_words(cf = "air_pressure")
cat(key_words(cf = "air_pressure"))

# a different ERDDAP™ server
# key_words(cf = "air_pressure", url = servers()$url[6])
} # }
```
