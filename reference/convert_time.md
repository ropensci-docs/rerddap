# Convert a UDUNITS compatible time to ISO time

Convert a UDUNITS compatible time to ISO time

## Usage

``` r
convert_time(
  n = NULL,
  isoTime = NULL,
  units = "seconds since 1970-01-01T00:00:00Z",
  url = eurl(),
  method = "local",
  ...
)
```

## Arguments

- n:

  numeric; A unix time number.

- isoTime:

  character; A string time representation.

- units:

  character; Units to return. Default: "seconds since
  1970-01-01T00:00:00Z"

- url:

  Base URL of the ERDDAP™ server. See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- method:

  (character) One of local or web. Local simply uses
  [`as.POSIXct()`](https://rdrr.io/r/base/as.POSIXlt.html), while web
  method uses the ERDDAP™ time conversion service
  `/erddap/convert/time.txt`

- ...:

  Curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Details

When `method = "web"` time zone is GMT/UTC

## Examples

``` r
 if (FALSE) { # \dontrun{
# local conversions
convert_time(n = 473472000)
convert_time(isoTime = "1985-01-02T00:00:00Z")

# using an ERDDAP™ web service
convert_time(n = 473472000, method = "web")
convert_time(isoTime = "1985-01-02T00:00:00Z", method = "web")
} # }
```
