# Occurrence download statistics

Retrieve statistics about GBIF occurrence downloads. Filters for
downloads matching the provided criteria, then provides counts by year,
month and dataset of the total number of downloads, and the total number
of records included in those downloads.

## Usage

``` r
occ_download_stats(
  from = NULL,
  to = NULL,
  publishingCountry = NULL,
  datasetKey = NULL,
  publishingOrgKey = NULL,
  limit = NULL,
  offset = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- from:

  (character) Start date in format `YYYY-MM`. Optional.

- to:

  (character) End date in format `YYYY-MM`. Optional.

- publishingCountry:

  (character) ISO 2-letter country code. Optional.

- datasetKey:

  (character) Dataset UUID. Optional.

- publishingOrgKey:

  (character) Publishing organization UUID. Optional.

- limit:

  (integer) Number of results to return. Optional.

- offset:

  (integer) Offset for pagination. Optional.

- curlopts:

  list of named curl options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).
  See
  [curl::curl_options](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A list with two slots:

- meta: a single row data.frame with columns: `offset`, `limit`,
  `endofrecords`, `count`

- results: a tibble with the results containing columns: `datasetKey`,
  `totalRecords`, `numberDownloads`, `year`, `month`

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
[`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Get summarized download statistics
occ_download_stats()

# Filter by date range and country
occ_download_stats(from = "2023-01", to = "2023-12", publishingCountry = "US")

# Filter by publishing organization iNaturalist
occ_download_stats(publishingOrgKey = "28eb1a3f-1c15-4a95-931a-4af90ecb574d")
} # }
```
