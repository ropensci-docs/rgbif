# List datasets for a download

List datasets for a download

## Usage

``` r
occ_download_datasets(
  key,
  limit = 20,
  start = 0,
  curlopts = list(http_version = 2)
)
```

## Arguments

- key:

  A key generated from a request, like that from
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

- limit:

  (integer/numeric) Number of records to return. Default: 20, Max: 1000

- start:

  (integer/numeric) Record number to start at. Default: 0

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

a list with two slots:

- meta: a single row data.frame with columns: `offset`, `limit`,
  `endofrecords`, `count`

- results: a tibble with the results, of three columns: `downloadKey`,
  `datasetKey`, `numberRecords`

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
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
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_datasets(key="0003983-140910143529206")
occ_download_datasets(key="0003983-140910143529206", limit = 3)
occ_download_datasets(key="0003983-140910143529206", limit = 3, start = 10)
} # }
```
