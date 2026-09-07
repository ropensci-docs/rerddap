# Changelog

## rerddap 1.3.0

CRAN release: 2026-07-03

- ‘griddap()’ can now download the data as parquet files
- A new function which estimates the size of a ‘griddap()’ download
  without having to make the request.
- Some improvemments in the vignette

## rerddap 1.2.3

CRAN release: 2026-02-26

Fixed minor bug when using ‘tabledap()’ with “parquet” option

## rerddap 1.2.2

CRAN release: 2026-01-15

- Table of contents added to vignette
- Interactive map example added to vignette
- Fixed some bad URLs in vignette
- Minor tweaks in return value when some errors are encountered

## rerddap 1.2.1

CRAN release: 2025-03-19

- Improved “safety” of some function calls to insure graceful endings if
  resource not available
- Updated some of the examples in the vignette

## rerddap 1.2.0

CRAN release: 2024-12-11

- tabledap() requests can now be downloaded as a parquet file, making
  for a much smaller download
- units have been added to tabledap() output as attributes
- griddap() bug fixed when a coordinate has a very large value, such as
  for some projected data.
- browse() now returns the URL if base::interactive is FALSE, as the
  documentation states

## rerddap 1.1.0

CRAN release: 2024-01-12

- ‘tabledap()’ responses now have the datatype given in the file .dds

## rerddap 1.0.4

CRAN release: 2023-08-23

- fixes problem with time bounds check and “last”

## rerddap 1.0.3

CRAN release: 2023-06-30

- Provides exta checks on time bounds.
- Fixes some typos and a mistake showing ‘global_search()’ in vignette

## rerddap 1.0.2

CRAN release: 2023-02-07

Ensure ‘\[’ and ’\]’ properly encoded in URL

## rerddap 1.0.1

CRAN release: 2022-12-11

Changed default cacheing behavior and ‘cache_setup()’

## rerddap 1.0.0

CRAN release: 2022-10-03

- griddap dataframe now uses the same coordinate names returned in
  ‘rerddap::info()’
- all grids can now be “melted” into a dataframe, not just lat-lon grids
- fixed some bugs accessing some datasets not on lat-lon grid
- vignette now included in package.

## rerddap 0.8.0

CRAN release: 2021-11-19

- Added global search function
- fixed bug when dataset has a decreasing coordinate that is not
  latitude or longitude

## rerddap 0.7.6

CRAN release: 2021-08-18

#### MINOR IMPROVEMENTS

- fixed a bug in dealing with trailing slashes in URLs

## rerddap 0.7.4

CRAN release: 2021-03-05

#### MINOR IMPROVEMENTS

- fix a broken test

## rerddap 0.7.0

CRAN release: 2020-11-03

#### MINOR IMPROVEMENTS

- vignettes only on package documentation site now
  ([\#87](https://github.com/ropensci/rerddap/issues/87))
- `server()` (to fetch known ERDDAP™ server URLs) now uses the list
  maintained by `irishmarineinstitute/awesome-erddap` on GitHub
  ([\#86](https://github.com/ropensci/rerddap/issues/86))
- better error handling for
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md):
  if no dimension arguments passed, we error saying so (and no http
  requests made); in addition, if a dataset is passed to
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md),
  to which the output of
  [`info()`](https://docs.ropensci.org/rerddap/reference/info.md) was
  also passed, then we can check if the dataset has griddap data or not,
  and fail saying so if not
  ([\#91](https://github.com/ropensci/rerddap/issues/91))
- [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  and
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md):
  if [`info()`](https://docs.ropensci.org/rerddap/reference/info.md)
  output passed to these two funcitons, we will now use the url within
  that info output, and use a message telling the user we are doing so;
  now you don’t have to set the url if you pass info output
  ([\#92](https://github.com/ropensci/rerddap/issues/92))

## rerddap 0.6.5

CRAN release: 2019-07-20

#### BUG FIXES

- fix a `convert_units` test that was failing because remote service had
  changed the response

## rerddap 0.6.4

CRAN release: 2019-07-01

#### BUG FIXES

- fix to internal fxn `err_handle()` for handling http errors - ERDDAP™
  servers changed to some weird JSON-ish type format
  ([\#85](https://github.com/ropensci/rerddap/issues/85))

## rerddap 0.6.0

CRAN release: 2019-05-08

#### MINOR IMPROVEMENTS

- change all
  [`tibble::as_data_frame`](https://tibble.tidyverse.org/reference/deprecated.html)/[`tibble::data_frame`](https://tibble.tidyverse.org/reference/deprecated.html)
  to
  [`tibble::as_tibble`](https://tibble.tidyverse.org/reference/as_tibble.html)
  ([\#79](https://github.com/ropensci/rerddap/issues/79))
- [`info()`](https://docs.ropensci.org/rerddap/reference/info.md) gains
  new element in its output list, `base_url`, the base url for the
  ERDDAP™ server under consideration
  ([\#80](https://github.com/ropensci/rerddap/issues/80))
- improved docs for
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  with respect to what’s returned from the function
  ([\#81](https://github.com/ropensci/rerddap/issues/81))
- fix some test fixtures to use preserve exact bytes so that cran checks
  on debian clang devel don’t fail
  ([\#83](https://github.com/ropensci/rerddap/issues/83))
- add .github files: contributing, issue template, pull request template

#### BUG FIXES

- fix for lat/lon parsing within
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  to account for cases when min and max are reversed from the order they
  should be in ([\#78](https://github.com/ropensci/rerddap/issues/78))
- fix to
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  to parse additioanl dimensions returned; previously we were only
  returning time, lat, and lon, plus one more
  ([\#82](https://github.com/ropensci/rerddap/issues/82)) thanks
  [@afredstonhermann](https://github.com/afredstonhermann)

## rerddap 0.5.0

CRAN release: 2019-02-01

#### MINOR IMPROVEMENTS

- added new `Caching` section to package level manual file
  ([`?rerddap`](https://docs.ropensci.org/rerddap/reference/rerddap.md))
  about caching ([\#52](https://github.com/ropensci/rerddap/issues/52))
- use markdown docs in package
  ([\#75](https://github.com/ropensci/rerddap/issues/75))
- replace `httr` with `crul`
  ([\#54](https://github.com/ropensci/rerddap/issues/54))
- cache most tests with HTTP requests using `vcr`
  ([\#76](https://github.com/ropensci/rerddap/issues/76))
- add test for `read` parameter in
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  ([\#47](https://github.com/ropensci/rerddap/issues/47))
- use default url via
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md); used
  as default in main functions; set default url with env vars, see
  [`?eurl`](https://docs.ropensci.org/rerddap/reference/eurl.md)
  ([\#41](https://github.com/ropensci/rerddap/issues/41))
- improve handling and reporting back to user of ERDDAP™ server errors
  ([\#70](https://github.com/ropensci/rerddap/issues/70))
  ([\#73](https://github.com/ropensci/rerddap/issues/73))
- change to
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md):
  when nc format gridded datasets have latitude and longitude we “melt”
  them into a data.frame for easy downstream consumption. When nc format
  gridded datasets do not have latitude and longitude components, we do
  not read in the data, throw a warning saying so. You can readin the nc
  file yourself with the file path
  ([\#74](https://github.com/ropensci/rerddap/issues/74))
- for for
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  to support cases in wihch lat/lon runs north to south and south to
  north ([\#68](https://github.com/ropensci/rerddap/issues/68))

#### BUG FIXES

- [`memory()`](https://docs.ropensci.org/rerddap/reference/disk.md)
  usage in
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  wasn’t working. fixed now
  ([\#77](https://github.com/ropensci/rerddap/issues/77))

## rerddap 0.4.2

CRAN release: 2017-05-12

#### NEW FEATURES

- Now using `hoardr` to manage caching paths and such
  ([\#60](https://github.com/ropensci/rerddap/issues/60)). Also now
  asking users where they want to cache files, either in a `rappdirs`
  user cache dir or a temp directory. Now on tests and examples we use
  temp dirs.
- Related to above, new functions
  [`cache_info()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)
  to get cache path and number of cached files, and
  [`cache_setup()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)
  to set cache path.
- Related to above,
  [`cache_details()`](https://docs.ropensci.org/rerddap/reference/cache_details.md),
  [`cache_list()`](https://docs.ropensci.org/rerddap/reference/cache_list.md),
  and
  [`cache_delete()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md)
  lose their `cache_path` parameter - now cache path is set package wide
  and we use the same cache path, so no need to set in the fxn call.

#### MINOR IMPROVEMENTS

- Fixes to a number of
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  and
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
  examples to use datasets that still exist (previous examples used
  datasets that are no gone)

## rerddap 0.4.0

CRAN release: 2017-04-25

#### NEW FEATURES

- New vignette added that goes in to much more depth than the original
  vignette ([\#51](https://github.com/ropensci/rerddap/issues/51)) thx
  to [@rmendels](https://github.com/rmendels)
- [`info()`](https://docs.ropensci.org/rerddap/reference/info.md)
  function gains new attribute `url` with the base url for the ERDDAP™
  server used ([\#42](https://github.com/ropensci/rerddap/issues/42))
- Replaced usage of internal compact data.frame code to use `tibble`
  package ([\#45](https://github.com/ropensci/rerddap/issues/45))

#### MINOR IMPROVEMENTS

- Added another ERDDAP™ server to
  [`servers()`](https://docs.ropensci.org/rerddap/reference/servers.md)
  function ([\#49](https://github.com/ropensci/rerddap/issues/49))
- Changed base URLs for default ERDDAP™ server from `http` to `https`
  ([\#50](https://github.com/ropensci/rerddap/issues/50))
- Added note to docs for
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  and
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
  for how to best deal with 500 server errors
  ([\#48](https://github.com/ropensci/rerddap/issues/48))
- Replaced all `dplyr::rbind_all` uses with
  [`dplyr::bind_rows`](https://dplyr.tidyverse.org/reference/bind_rows.html)
  ([\#46](https://github.com/ropensci/rerddap/issues/46))

## rerddap 0.3.4

CRAN release: 2016-01-14

#### MINOR IMPROVEMENTS

- Removed use of `ncdf` package, which has been taken off CRAN. Using
  `ncdf4` now for all NetCDF file manipulation.
  ([\#35](https://github.com/ropensci/rerddap/issues/35))
- Failing better now with custom error catching
  ([\#31](https://github.com/ropensci/rerddap/issues/31))
- Added many internal checks for parameter inputs, warning or stopping
  as necessary - ERDDAP™ servers silently drop with no informative
  messages ([\#32](https://github.com/ropensci/rerddap/issues/32))

#### BUG FIXES

- Using now `file.info()$size` instead of
  [`file.size()`](https://rdrr.io/r/base/file.info.html) to be backwards
  compatible with R versions \< 3.2

## rerddap 0.3.0

CRAN release: 2015-10-10

#### NEW FEATURES

- Cache functions accept the outputs of
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  and
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
  so that the user can easily see cache details or delete the file from
  the cache without having to manually get the file name.
  ([\#30](https://github.com/ropensci/rerddap/issues/30))

#### MINOR IMPROVEMENTS

- All package dependencies now use `importFrom` so we only import
  functions we need instead of their global namespaces.

#### BUG FIXES

- Fixed bug in parsing data from netcdf files, affected the
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  function ([\#28](https://github.com/ropensci/rerddap/issues/28))

## rerddap 0.2.0

CRAN release: 2015-07-01

#### NEW FEATURES

- Added a suite of functions to manage local cached files
  ([\#17](https://github.com/ropensci/rerddap/issues/17))

#### MINOR IMPROVEMENTS

- Added new ERDDAP™ server to list of servers in the
  [`servers()`](https://docs.ropensci.org/rerddap/reference/servers.md)
  function ([\#21](https://github.com/ropensci/rerddap/issues/21))

#### BUG FIXES

- Fixed a few cases across a number of functions in which an empty list
  passed to `query` parmaeter in
  [`httr::GET()`](https://httr.r-lib.org/reference/GET.html) caused an
  error ([\#23](https://github.com/ropensci/rerddap/issues/23))
- Fixed retrieval of path to file written to disk by
  [`httr::write_disk()`](https://httr.r-lib.org/reference/write_disk.html)
  ([\#24](https://github.com/ropensci/rerddap/issues/24))
- `last` is a value accepted by ERDDAP™ servers, but internal functions
  weren’t checking correctly, fixed now.
  ([\#25](https://github.com/ropensci/rerddap/issues/25))
- [`as.info()`](https://docs.ropensci.org/rerddap/reference/info.md)
  wasn’t passing on the `url` parameter to the
  [`info()`](https://docs.ropensci.org/rerddap/reference/info.md)
  function. fixed now.
  ([\#26](https://github.com/ropensci/rerddap/issues/26))

## rerddap 0.1.0

CRAN release: 2015-05-11

#### NEW FEATURES

- released to CRAN
