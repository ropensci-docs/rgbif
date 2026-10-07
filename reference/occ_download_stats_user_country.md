# Downloads by user country

Summarizes downloads by month, grouped by the user's country code.

## Usage

``` r
occ_download_stats_user_country(
  from = NULL,
  to = NULL,
  userCountry = NULL,
  publishingCountry = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- from:

  (character) Start date in format `YYYY-MM`. Optional.

- to:

  (character) End date in format `YYYY-MM`. Optional.

- userCountry:

  (character) ISO 2-letter country code. Optional.

- publishingCountry:

  (character) ISO 2-letter country code. Optional.

- curlopts:

  list of named curl options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).
  See
  [curl::curl_options](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A tibble with download counts by user country and month

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

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
[`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md),
[`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md),
[`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md),
[`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md),
[`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md),
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Run with no args to get monthly download counts for all of GBIF 
occ_download_stats_user_country()

# Filter by date range
occ_download_stats_user_country(from = "2023-01", to = "2023-12")

# Filter by user country
occ_download_stats_user_country(userCountry = "US")
} # }
```
