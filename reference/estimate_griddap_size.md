# Estimate the size of a rerddap::griddap() request

Uses coordinate metadata from an ERDDAP info() object to estimate how
many grid cells will be returned and the total uncompressed byte count
for each requested data variable. No network request is made.

## Usage

``` r
estimate_griddap_size(
  info,
  ...,
  fields = "all",
  stride = 1L,
  spacing = list(),
  verbose = TRUE
)
```

## Arguments

- info:

  An object returned by rerddap::info().

- ...:

  Named dimension constraints, one per coordinate variable to constrain.
  Names must exactly match the coordinate variable names in the dataset
  (as returned by dimvars(info)). Each value is c(min, max); for time
  use ISO 8601 strings.

- fields:

  Character vector of data variable names, or "all" (default).

- stride:

  Integer scalar or named list of per-dimension stride values, using the
  same convention as griddap(). Default 1.

- spacing:

  Optional named list to override auto-detected spacing for one or more
  dimensions. For time, supply seconds as time_sec (e.g. spacing =
  list(time_sec = 86400)). For other dimensions use the coordinate
  variable name (e.g. spacing = list(latitude = 0.01, xi_rho = 1)).

- verbose:

  Logical; print a formatted summary (default TRUE).

## Value

Invisibly, a named list containing per-dimension point counts, spacing
values, per-variable byte estimates, and total bytes.

## Details

Coordinate dimension names are taken directly from the info object using
the same logic as rerddap:::dimvars() — the set-difference between all
keys in info\$alldata and the data variable names plus "NC_GLOBAL". This
means any coordinate system works: geographic lat/lon, projected x/y,
sigma-layer depth, ROMS xi_rho/eta_rho, etc.

Dimension constraints are passed via ... using the exact coordinate
variable names reported by the dataset, the same way griddap() accepts
them. Each constraint is a numeric (or character for time) vector of
length 2: c(min, max).

Spacing is resolved in this order for each dimension:

1.  User-supplied override in the spacing argument.

2.  For time: (t_max - t_min) / (nValues - 1) derived from the
    dimension's nValues row and actual_range attribute. This correctly
    handles running composites where time steps are daily even though
    the composite window is e.g. 8 days.

3.  NC_GLOBAL attributes: geospatial_lat_resolution,
    geospatial_lon_resolution, time_coverage_resolution (ISO 8601).

4.  Coordinate variable attributes: point_spacing, resolution, spacing.

5.  For time: averageSpacing string from the nValues row as a last
    resort.

6.  If the constraint min == max the dimension contributes 1 point.

7.  Otherwise: NA — a warning is issued and 1 point is assumed.

## Examples

``` r
if (FALSE) { # \dontrun{
  library(rerddap)

  myURL <- "https://coastwatch.pfeg.noaa.gov/erddap/"
  response <- try(httr::HEAD(myURL, httr::timeout(10)), silent = TRUE)
  if (inherits(response, "try-error")) {
     stop("The ERDDAP\u2122 server is not responding")
  }
  info <- rerddap::info("erdMH1chla8day", url = myURL)
  estimate_griddap_size(info,
    latitude  = c(30, 50),
    longitude = c(-140, -110),
    time      = c("2020-01-01", "2020-12-31"))
} # }
```
