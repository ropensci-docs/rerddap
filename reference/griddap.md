# Get ERDDAP(TM) gridded data

Get ERDDAP(TM) gridded data

## Usage

``` r
griddap(
  datasetx,
  ...,
  fields = "all",
  stride = 1,
  fmt = "nc",
  url = eurl(),
  store = disk(),
  read = TRUE,
  callopts = list()
)
```

## Arguments

- datasetx:

  Anything coercable to an object of class info. So the output of a call
  to [`info`](https://docs.ropensci.org/rerddap/reference/info.md), or a
  datasetid, which will internally be passed through
  [`info`](https://docs.ropensci.org/rerddap/reference/info.md)

- ...:

  Dimension arguments. See examples. Can be any 1 or more of the
  dimensions for the particular dataset - and the dimensions vary by
  dataset. For each dimension, pass in a vector of length two, with min
  and max value desired. at least 1 required.

- fields:

  (character) Fields to return, in a character vector.

- stride:

  (integer) How many values to get. 1 = get every value, 2 = get every
  other value, etc. Default: 1 (i.e., get every value)

- fmt:

  (character) One of nc (for netcdf), csv, or parquet. Default: nc

- url:

  A URL for an ERDDAP™ server. Default:
  https://upwell.pfeg.noaa.gov/erddap/ - See
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) for
  more information

- store:

  One of [`disk`](https://docs.ropensci.org/rerddap/reference/disk.md)
  (default) or
  [`memory`](https://docs.ropensci.org/rerddap/reference/disk.md). You
  can pass options to
  [`disk`](https://docs.ropensci.org/rerddap/reference/disk.md). Beware:
  if you choose `fmt="nc"`, we force `store=disk()` because nc files
  have to be written to disk.

- read:

  (logical) Read data into memory or not. Does not apply when `store`
  parameter is set to memory (which reads data into memory). For large
  csv, or especially netcdf files, you may want to set this to `FALSE`,
  which simply returns a summary of the dataset - and you can read in
  data piecemeal later. Default: `TRUE`

- callopts:

  Curl options passed on to
  [`verb-GET`](https://docs.ropensci.org/crul/reference/verb-GET.html)

## Value

An object of class `griddap_csv` if csv chosen or `griddap_nc` if nc
file format chosen.

- `griddap_csv`: a data.frame created from the downloaded csv data

- `griddap_nc`: a list, with slots "summary" and "data". "summary" is
  the unclassed output from
  [`ncdf4::nc_open`](https://rdrr.io/pkg/ncdf4/man/nc_open.html), from
  which you can do any netcdf operations you like. "data" is a
  data.frame created from the netcdf data. the data.frame may be empty
  if there were problems parsing the netcdf data

Both have the attributes: datasetid (the dataset id), path (the path on
file for the csv or nc file), url (the url requested to the ERDDAP
server)

If `read=FALSE`, the data.frame for `griddap_csv` and the data.frame in
the "data" slot is empty for `griddap_nc`

## Details

Details:

If you run into an error like "HTTP Status 500 - There was a
(temporary?) problem. Wait a minute, then try again.". it's likely they
are hitting up against a size limit, and they should reduce the amount
of data they are requesting either via space, time, or variables. Pass
in `config = verbose()` to the request, and paste the URL into your
browser to see if the output is garbled to examine if there's a problem
with servers or this package

## Dimensions and Variables

ERDDAP™ grid dap data has this concept of dimenions vs. variables.
Dimensions are things like time, latitude, longitude, altitude, and
depth. Whereas variables are the measured variables, e.g., temperature,
salinity, air.

You can't separately adjust values for dimensions for different
variables. So, here's how it's gonna work:

Pass in lower and upper limits you want for each dimension as a vector
(e.g., `c(1,2)`), or leave to defaults (i.e., don't pass anything to a
dimension). Then pick which variables you want returned via the `fields`
parameter. If you don't pass in options to the `fields` parameter, you
get all variables back.

To get the dimensions and variables, along with other metadata for a
dataset, run
[`info`](https://docs.ropensci.org/rerddap/reference/info.md), and each
will be shown, with their min and max values, and some other metadata.

## Where does the data go?

You can choose where data is stored. Be careful though. You can easily
get a single file of hundreds of MB's (upper limit: 2 GB) in size with a
single request. To the `store` parameter, pass
[`memory`](https://docs.ropensci.org/rerddap/reference/disk.md) if you
want to store the data in memory (saved as a data.frame), or pass
[`disk`](https://docs.ropensci.org/rerddap/reference/disk.md) if you
want to store on disk in a file. Note that
[`memory`](https://docs.ropensci.org/rerddap/reference/disk.md) and
[`disk`](https://docs.ropensci.org/rerddap/reference/disk.md) are not
character strings, but function calls.
[`memory`](https://docs.ropensci.org/rerddap/reference/disk.md) does not
accept any inputs, while
[`disk`](https://docs.ropensci.org/rerddap/reference/disk.md) does.
Possibly will add other options, like “sql” for storing in a SQL
database.

## Non-lat/lon grid data

Some gridded datasets have latitude/longitude components, but some do
not. When nc format gridded datasets have latitude and longitude we
"melt" them into a data.frame for easy downstream consumption. When nc
format gridded datasets do not have latitude and longitude components,
we do not read in the data, throw a warning saying so. You can readin
the nc file yourself with the file path. CSV format is not affected by
this issue as CSV data is easily turned into a data.frame regardless of
whether latitude/longitude data are present.

## References

https://upwell.pfeg.noaa.gov/erddap/rest.html

## Examples

``` r
if (FALSE) { # \dontrun{
# single variable dataset
## You can pass in the outpu of a call to info
(out <- info('erdVHNchlamday'))
## Or, pass in a dataset id
(res <- griddap('erdVHNchlamday',
 time = c('2015-04-01','2015-04-10'),
 latitude = c(18, 21),
 longitude = c(-120, -119)
))

# multi-variable dataset
(out <- info('erdQMekm14day'))
(res <- griddap(out,
 time = c('2015-12-28','2016-01-01'),
 latitude = c(24, 23),
 longitude = c(88, 90)
))
(res <- griddap(out, time = c('2015-12-28','2016-01-01'),
   latitude = c(24, 23), longitude = c(88, 90), fields = 'mod_current'))
(res <- griddap(out, time = c('2015-12-28','2016-01-01'),
   latitude = c(24, 23), longitude = c(88, 90), fields = 'mod_current',
   stride = c(1,2,1,2)))
(res <- griddap(out, time = c('2015-12-28','2016-01-01'),
   latitude = c(24, 23), longitude = c(88, 90),
   fields = c('mod_current','u_current')))


# Write to memory (within R), or to disk
(out <- info('erdQSwindmday'))
## disk, by default (to prevent bogging down system w/ large datasets)
## you can also pass in path and overwrite options to disk()
(res <- griddap(out,
 time = c('2006-07-11','2006-07-20'),
 longitude = c(166, 170),
 store = disk()
))
## the 2nd call is much faster as it's mostly just the time of reading in
## the table from disk
system.time( griddap(out,
 time = c('2006-07-11','2006-07-15'),
 longitude = c(10, 15),
 store = disk()
) )
system.time( griddap(out,
 time = c('2006-07-11','2006-07-15'),
 longitude = c(10, 15),
 store = disk()
) )

## memory - you have to choose fmt="csv" if you use memory
(res <- griddap("erdMBchla1day",
 time = c('2015-01-01','2015-01-03'),
 latitude = c(14, 15),
 longitude = c(125, 126),
 fmt = "csv", store = memory()
))

## Use ncdf4 package to parse data
info("erdMBchla1day")
(res <- griddap("erdMBchla1day",
 time = c('2015-01-01','2015-01-03'),
 latitude = c(14, 15),
 longitude = c(125, 126)
))

# Get data in csv format
## by default, we get netcdf format data
(res <- griddap('erdMBchla1day',
 time = c('2015-01-01','2015-01-03'),
 latitude = c(14, 15),
 longitude = c(125, 126),
 fmt = "csv"
))

# Use a different ERDDAP™ server url
## NOAA IOOS PacIOOS
url = "https://cwcgom.aoml.noaa.gov/erddap/"
out <- info("miamiacidification", url = url)
(res <- griddap(out,
 time = c('2019-11-01','2019-11-03'),
 latitude = c(15, 16),
 longitude = c(-90, -88)
))
## pass directly into griddap() - if you pass a datasetid string directly
## you must pass in the url or you'll be querying the default ERDDAP™ url,
## which isn't the one you want if you're not using the default ERDDAP™ url
griddap("miamiacidification", url = url,
 time = c('2019-11-01','2019-11-03'),
 latitude = c(15, 16),
 longitude = c(-90, -88)
)

# Using 'last'
## with time
griddap('erdVHNchlamday',
 time = c('last-5','last'),
 latitude = c(18, 21),
 longitude = c(-120, -119)
)
## with latitude
griddap('erdVHNchlamday',
  time = c('2015-04-01','2015-04-10'),
  latitude = c('last', 'last'),
  longitude = c(-120, -119)
)
## with longitude
griddap('erdVHNchlamday',
  time = c('2015-04-01','2015-04-10'),
  latitude = c(18, 21),
  longitude = c('last', 'last')
)

# datasets without lat/lon grid and with fmt=nc
# FIXME: this dataset is gone
# (x <- info('glos_tds_5912_ca66_3f41'))
# res <- griddap(x,
#   time = c('2018-04-01','2018-04-10'),
#   ny = c(1, 2),
#   nx = c(3, 5)
# )
## data.frame is empty
# res$data
## read in from the nc file path
# ncdf4::nc_open(res$summary$filename)
} # }
```
