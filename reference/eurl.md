# Default ERDDAP™ server URL

Default ERDDAP™ server URL

## Usage

``` r
eurl()
```

## Details

default url is https://upwell.pfeg.noaa.gov/erddap/

You can set a default using an environment variable so you don't have to
pass anything to the URL parameter in your function calls.

In your .Renviron file or similar set a URL for the environment variable
`RERDDAP_DEFAULT_URL`, like
`RERDDAP_DEFAULT_URL=https://upwell.pfeg.noaa.gov/erddap/`

It's important that you include a trailing slash in your URL

## Examples

``` r
eurl()
#> [1] "https://upwell.pfeg.noaa.gov/erddap/"
Sys.setenv(RERDDAP_DEFAULT_URL = "https://google.com")
Sys.getenv("RERDDAP_DEFAULT_URL")
#> [1] "https://google.com"
eurl()
#> [1] "https://google.com/"
Sys.unsetenv("RERDDAP_DEFAULT_URL")
eurl()
#> [1] "https://upwell.pfeg.noaa.gov/erddap/"
```
