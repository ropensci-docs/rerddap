# global_search

Search for ERDDAP™ tabledap or griddap datasets from a list of ERDDAP™
servers based on search terms.

## Usage

``` r
global_search(query, server_list, which_service)
```

## Arguments

- query:

  (character) Search terms

- server_list:

  (list of character) List of ERDDAP™ servers to search

- which_service:

  (character) One of tabledep or griddap.

## Value

If successful a dataframe wih columns:

- title - the dataset title

- dataset_id - the datasetid on that ERDDAP™ server

- url - base url of dataset ERDDAP™ server

if urls are valid, no match is found, will return no match found else
returns error message

## Details

Uses the 'reddap' function ed_search() to search over the list of
servers

## See also

[`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html)

## Examples

``` r
# get list of servers know by
# https://irishmarineinstitute.github.io/awesome-erddap
# e_servers <- servers()$url
# select a couple to search
# e_servers <- e_servers[c(1, 40)]
# to meet CRAN time limits will only search 1 place
e_servers <- "https://coastwatch.pfeg.noaa.gov/erddap/"
test_query <- 'C-HARM v1 2-Day Forecast'
query_results <- global_search(test_query, e_servers, "griddap")
```
