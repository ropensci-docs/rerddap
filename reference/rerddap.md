# rerddap

General purpose R client for ERDDAP™ servers

## ERDDAP™ info

NOAA's ERDDAP™ service holds many datasets of interest. It's built on
top of OPenDAP. You can search for datasets via
[`ed_search()`](https://docs.ropensci.org/rerddap/reference/ed_search.md),
list datasets via
[`ed_datasets()`](https://docs.ropensci.org/rerddap/reference/ed_search.md),
get information on a single dataset via
[`info()`](https://docs.ropensci.org/rerddap/reference/info.md), then
get data you want for either tabledap type via
[`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md),
or for griddap type via
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)

## tabledap/griddap

tabledap and griddap have different interfaces to query for data, so
[`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
and
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
are separated out as separate functions even though some of the
internals are the same. In particular, with tabledap you can query
on/subset all variables, whereas with gridddap, you can only query
on/subset the dimension varibles (e.g., latitude, longitude, altitude).

## Data size

With griddap data via
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
you can get a lot of data quickly. Try small searches of a dataset to
start to get a sense for the data, then you can increase the amount of
data you get. See
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
for more details.

## Caching

rerddap by default caches the requests you make, so that if you happen
to make the same request again, the data is restored from the cache,
rather than having to go out and retrieve it remotely. For most
applications, this is good, as it can speed things up when doing a lot
of request in a script, and works because in most cases an ERDDAP™
request is "idempotent". This means that the the request will always
return the same thing no matter what requests came before - it doesn't
depend on state. However this is not true if the script uses either
"last" in
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md) or
"now" in
[`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
as these will return different values as time elapses and data are added
to the datasets. While it is desirable to have ERDDAP™ purely
idempotent, the "last" and "now" constructs are very helpful for people
using ERDDAP™ in dashboards, webpages, regular input to models and the
like, and the benefits far outweigh the problems. However, if you are
using either "last" or "now" in an rerddap based script, you want to be
very careful to clear the rerddap cache, otherwise the request will be
viewed as the same, and the data from the last request, rather than the
latest data, will be returned.

## See also

Useful links:

- <https://docs.ropensci.org/rerddap/>

- <https://github.com/ropensci/rerddap>

- Report bugs at <https://github.com/ropensci/rerddap/issues>

## Author

**Maintainer**: Roy Mendelssohn <roy.mendelssohn@noaa.gov>
\[contributor\]

Authors:

- Scott Chamberlain

Other contributors:

- Ben Tupper \[contributor\]

- Salvador Jesús Fernández Bejarano \[contributor\]
