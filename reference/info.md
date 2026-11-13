# Get information on an ERDDAP(TM) dataset.

Get information on an ERDDAP(TM) dataset.

## Usage

``` r
info(datasetid, url = eurl(), ...)

as.info(x, url)
```

## Arguments

- datasetid:

  Dataset id

- url:

  A URL for an ERDDAP(TM) server. Default:
  https://upwell.pfeg.noaa.gov/erddap/ - See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- ...:

  Further args passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)
  (must be a named parameter)

- x:

  A datasetid or the output of `info`

## Value

Prints a summary of the data on return, but you can index to various
information.

The data is a list of length two with:

- variables - Data.frame of variables and their types

- alldata - List of data variables and their full attributes

Where `alldata` element has many data.frame's, one for each variable,
with metadata for that variable. E.g., for griddap dataset
`noaa_pfeg_696e_ec99_6fa6`, `alldata` has:

- NC_GLOBAL

- time

- latitude

- longitude

- sss

## References

https://upwell.pfeg.noaa.gov/erddap/index.html

## Examples

``` r
if (FALSE) { # \dontrun{
# grid dap datasets
info('erdATastnhday')

(out <- ed_search(query='temperature'))
info(out$info$dataset_id[5])
info(out$info$dataset_id[15])
info(out$info$dataset_id[25])
info(out$info$dataset_id[150])
info(out$info$dataset_id[400])
info(out$info$dataset_id[678])

out <- info(datasetid='erdMBchla1day')
## See brief overview of the variables and range of possible values, if given
out$variables
## all information on longitude
out$alldata$longitude
## all information on chlorophyll
out$alldata$chlorophyll

# table dap datasets
(out <- ed_search(query='temperature', which = "table"))
info(out$info$dataset_id[1])
info(out$info$dataset_id[2])
info(out$info$dataset_id[3])
info(out$info$dataset_id[4])

info('erdCinpKfmBT')
out <- info('erdCinpKfmBT')
## See brief overview of the variables and range of possible values, if given
out$variables
## all information on longitude
out$alldata$longitude
## all information on Haliotis_corrugata_Mean_Density
out$alldata$Haliotis_corrugata_Mean_Density

# use a different ERDDAP(TM) server
## Marine Institute (Ireland)
info("IMI_CONN_2D", url = "http://erddap.marine.ie/erddap/")
} # }
```
