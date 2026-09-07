# Package index

## rerddap Package Description

- [`rerddap-package`](https://docs.ropensci.org/rerddap/reference/rerddap.md)
  [`rerddap`](https://docs.ropensci.org/rerddap/reference/rerddap.md) :
  rerddap

## Search

Functions to search for ERDDAP™ servers as well as to search ERDDAP™ for
datasets whose metadata match the given search.

- [`ed_search()`](https://docs.ropensci.org/rerddap/reference/ed_search.md)
  [`ed_datasets()`](https://docs.ropensci.org/rerddap/reference/ed_search.md)
  : Search for ERDDAP™ tabledep or griddap datasets
- [`ed_search_adv()`](https://docs.ropensci.org/rerddap/reference/ed_search_adv.md)
  : Advanced search for ERDDAP™ tabledep or griddap datasets
- [`global_search()`](https://docs.ropensci.org/rerddap/reference/global_search.md)
  : global_search
- [`servers()`](https://docs.ropensci.org/rerddap/reference/servers.md)
  : ERDDAP™ server URLS and other info

## Obtain basic dataset metadata

Obtain the basic dataset metadata to help in subsetting and downloading.

- [`info()`](https://docs.ropensci.org/rerddap/reference/info.md)
  [`as.info()`](https://docs.ropensci.org/rerddap/reference/info.md) :
  Get information on an ERDDAP(TM) dataset.
- [`browse()`](https://docs.ropensci.org/rerddap/reference/browse.md) :
  Browse a dataset webpage.

## Subset and Download Data

Functions to subset and download ERDDAP™ grids and tables.

- [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  : Get ERDDAP(TM) gridded data
- [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
  : Get ERDDAP™ tabledap data.
- [`estimate_griddap_size()`](https://docs.ropensci.org/rerddap/reference/estimate_griddap_size.md)
  : Estimate the size of a rerddap::griddap() request

## Optional Settings for Data Download

Optional settings for functions that subset and download ERDDAP™ grids
and tables.

- [`disk()`](https://docs.ropensci.org/rerddap/reference/disk.md)
  [`memory()`](https://docs.ropensci.org/rerddap/reference/disk.md) :
  Options for saving ERDDAP™ datasets.
- [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md) :
  Default ERDDAP™ server URL

## Cache Handling

Functions for dealing with ‘rerddap’ cache.

- [`cache_delete()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md)
  [`cache_delete_all()`](https://docs.ropensci.org/rerddap/reference/cache_delete.md)
  : Delete cached files
- [`cache_details()`](https://docs.ropensci.org/rerddap/reference/cache_details.md)
  : Get details of cached files
- [`cache_setup()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)
  [`cache_info()`](https://docs.ropensci.org/rerddap/reference/cache_setup.md)
  : Setup cache path
- [`cache_list()`](https://docs.ropensci.org/rerddap/reference/cache_list.md)
  : List cached files

## Various ERDDAP™ Based Utilities

Various ERDDAP™ based utilities for converting parameters.

- [`convert_time()`](https://docs.ropensci.org/rerddap/reference/convert_time.md)
  : Convert a UDUNITS compatible time to ISO time
- [`convert_units()`](https://docs.ropensci.org/rerddap/reference/convert_units.md)
  : Convert a CF Standard Name to/from a GCMD Science Keyword
- [`fipscounty()`](https://docs.ropensci.org/rerddap/reference/fipscounty.md)
  : Convert a FIPS County Code to/from a County Name
- [`key_words()`](https://docs.ropensci.org/rerddap/reference/key_words.md)
  : Convert a CF Standard Name to/from a GCMD Science Keyword
- [`version()`](https://docs.ropensci.org/rerddap/reference/version.md)
  : Get ERDDAP™ version

## Datasets

Datasets used in the the functions nd vignette.

- [`colors`](https://docs.ropensci.org/rerddap/reference/colors.md) :
  cmocean colors The cmocean color palette by Kristen Thyng as
  implemented in the R package "oce"
- [`institutions`](https://docs.ropensci.org/rerddap/reference/institutions.md)
  : institutions
- [`ioos_categories`](https://docs.ropensci.org/rerddap/reference/ioos_categories.md)
  : ioos_categories
- [`keywords`](https://docs.ropensci.org/rerddap/reference/keywords.md)
  : keywords
- [`longnames`](https://docs.ropensci.org/rerddap/reference/longnames.md)
  : longnames
- [`standardnames`](https://docs.ropensci.org/rerddap/reference/standardnames.md)
  : standardnames
- [`variablenames`](https://docs.ropensci.org/rerddap/reference/variablenames.md)
  : variablenames
