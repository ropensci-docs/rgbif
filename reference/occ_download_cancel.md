# Cancel a download creation process.

Cancel a download creation process.

## Usage

``` r
occ_download_cancel(
  key,
  user = NULL,
  pwd = NULL,
  curlopts = list(http_version = 2)
)

occ_download_cancel_staged(
  user = NULL,
  pwd = NULL,
  limit = 20,
  start = 0,
  curlopts = list(http_version = 2)
)
```

## Arguments

- key:

  (character) A key generated from a request, like that from
  `occ_download`. Required.

- user:

  (character) User name within GBIF's website. Required. See Details.

- pwd:

  (character) User password within GBIF's website. Required. See
  Details.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

- limit:

  Number of records to return. Default: 20

- start:

  Record number to start at. Default: 0

## Details

Note, these functions only cancel a job in progress. If your download is
already prepared for you, this won't do anything to change that.

`occ_download_cancel` cancels a specific job by download key - returns
success message

`occ_download_cancel_staged` cancels all jobs with status `RUNNING` or
`PREPARING` - if none are found, returns a message saying so - if some
found, they are cancelled, returning message saying so

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
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
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# occ_download_cancel(key="0003984-140910143529206")
# occ_download_cancel_staged()
} # }
```
