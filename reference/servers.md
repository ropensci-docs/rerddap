# ERDDAP™ server URLS and other info

ERDDAP™ server URLS and other info

## Usage

``` r
servers(...)
```

## Arguments

- ...:

  curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Value

data.frame with 3 columns:

- name (character): ERDDAP™ name

- url (character): ERDDAP™ url

- public (logical): whether it's public or not

## Examples

``` r
if (FALSE) { # \dontrun{
servers()
} # }
```
