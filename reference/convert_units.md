# Convert a CF Standard Name to/from a GCMD Science Keyword

Convert a CF Standard Name to/from a GCMD Science Keyword

## Usage

``` r
convert_units(udunits = NULL, ucum = NULL, url = eurl(), ...)
```

## Arguments

- udunits:

  character; A UDUNITS character string
  https://www.unidata.ucar.edu/software/udunits/

- ucum:

  character; A UCUM character string https://ucum.org/ucum.html

- url:

  Base URL of the ERDDAP server. See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Examples

``` r
 if (FALSE) { # \dontrun{
convert_units(udunits = "degree_C meter-1")
convert_units(ucum = "Cel.m-1")
} # }
```
