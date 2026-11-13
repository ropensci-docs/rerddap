# Browse a dataset webpage.

Browse a dataset webpage.

## Usage

``` r
browse(x, url = eurl(), ...)
```

## Arguments

- x:

  datasetid or an object associated with a datasetid such
  [`info()`](https://docs.ropensci.org/rerddap/reference/info.md),
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  or
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)

- url:

  A URL for an ERDDAP™ server. Default:
  https://upwell.pfeg.noaa.gov/erddap/ - See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Further args passed on to
  [`utils::browseURL`](https://rdrr.io/r/utils/browseURL.html) (must be
  a named parameter)

## Value

if in interactive mode, opens a URL in your default browser; if not,
then prints the URL in the console

## Author

Ben Tupper <btupper@bigelow.org>

## Examples

``` r
if (FALSE) { # \dontrun{
if (interactive()) {
# browse by dataset_id
browse('erdATastnhday')

# browse info class
my_info <- info('erdATastnhday')
browse(my_info)

# browse tabledap class
my_tabledap <- tabledap('erdCalCOFIlrvsiz', fields=c('latitude','longitude','larvae_size',
   'itis_tsn'), 'time>=2011-10-25', 'time<=2011-10-31')
browse(my_tabledap)
}} # }
```
