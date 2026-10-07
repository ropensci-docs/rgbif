# Download requests in a queue

Download requests in a queue

## Usage

``` r
occ_download_queue(..., .list = list(), status_ping = 10)
```

## Arguments

- ...:

  any number of
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  requests

- .list:

  any number of
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  requests

- status_ping:

  (integer) seconds between pings checking status of the download
  request. generally larger numbers for larger requests. default: 10
  (i.e., 10 seconds). must be 10 or greater

## Value

a list of `occ_download` class objects, see
[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md)
to fetch data

## Details

This function is a convenience wrapper around
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
allowing the user to kick off any number of requests, while abiding by
GBIF rules of 3 concurrent requests per user.

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

## How it works

It works by using lazy evaluation to collect your requests into a queue
(but does not use lazy evaluation if use the `.list` parameter). Then it
kicks of the first 3 requests. Then in a while loop, we check status of
those requests, and when any request finishes (see `When is a job done?`
below), we kick off the next, and so on. So in theory, there may not
always strictly be 3 running concurrently, but the function will usually
provide for 3 running concurrently.

## When is a job done?

We mark a job as done by checking the `/occurrence/download/` API route
with our
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
function. If the status of the job is any of "succeeded", "killed", or
"cancelled", then we mark the job as done and move on to other jobs in
the queue.

## Beware

This function is still in development. There's a lot of complexity to
this problem. We'll be rolling out fixes and improvements in future
versions of the package, so expect to have to adjust your code with new
versions.

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
[`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md),
[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md),
[`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md),
[`occ_download_list()`](https://docs.ropensci.org/rgbif/reference/occ_download_list.md),
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md),
[`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md),
[`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md),
[`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md),
[`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md),
[`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md),
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
if (interactive()) { # dont run in automated example runs, too costly
# passing occ_download() requests via ...
out <- occ_download_queue(
  occ_download(pred('taxonKey', 5231190), pred("year", 1976)),
  occ_download(pred('taxonKey', 5231190), pred("year", 2001)),
  occ_download(pred('taxonKey', 5231190), pred("year", 2001),
    pred_lte("month", 8)),
  occ_download(pred('taxonKey', 5229208), pred("year", 2011)),
  occ_download(pred('taxonKey', 2480946), pred("year", 2015)),
  occ_download(pred("country", "NZ"), pred("year", 1999),
    pred("month", 3)),
  occ_download(pred("catalogNumber", "Bird.27847588"),
    pred("year", 1998), pred("month", 2))
)

# supports <= 3 requests too
out <- occ_download_queue(
  occ_download(pred("country", "NZ"), pred("year", 1999), pred("month", 3)),
  occ_download(pred("catalogNumber", "Bird.27847588"), pred("year", 1998),
    pred("month", 2))
)

# using pre-prepared requests via .list
keys <- c(7905507, 5384395, 8911082)
queries <- list()
for (i in seq_along(keys)) {
  queries[[i]] <- occ_download_prep(
    pred("taxonKey", keys[i]),
    pred_in("basisOfRecord", c("HUMAN_OBSERVATION","OBSERVATION")),
    pred("hasCoordinate", TRUE),
    pred("hasGeospatialIssue", FALSE),
    pred("year", 1993)
  )
}
out <- occ_download_queue(.list = queries)
out

# another pre-prepared example
yrs <- 1930:1934
queries <- list()
for (i in seq_along(yrs)) {
  queries[[i]] <- occ_download_prep(
    pred("taxonKey", 2877951),
    pred_in("basisOfRecord", c("HUMAN_OBSERVATION","OBSERVATION")),
    pred("hasCoordinate", TRUE),
    pred("hasGeospatialIssue", FALSE),
    pred("year", yrs[i])
  )
}
out <- occ_download_queue(.list = queries)
out
}} # }
```
