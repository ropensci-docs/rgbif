# Get a download from GBIF.

Get a download from GBIF.

## Usage

``` r
occ_download_get(key, path = ".", overwrite = FALSE, ...)
```

## Arguments

- key:

  A key generated from a request, like that from `occ_download`

- path:

  Path to write zip file to. Default: `"."`, with a `.zip` appended to
  the end.

- overwrite:

  Will only overwrite existing path if TRUE.

- ...:

  named curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html).
  see
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Details

Downloads the zip file to a directory you specify on your machine.
[`crul::HttpClient()`](https://docs.ropensci.org/crul/reference/HttpClient.html)
is used internally to write the zip file to disk. See
[crul::writing-options](https://docs.ropensci.org/crul/reference/writing-options.html).
This function only downloads the file. See `occ_download_import` to open
a downloaded file in your R session. The speed of this function is of
course proportional to the size of the file to download. For example, a
58 MB file on my machine took about 26 seconds.

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

This function used to check for HTTP response content type, but it has
changed enough that we no longer check it. If you run into issues with
this function, open an issue in the GitHub repository.

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
[`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md),
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
occ_download_get("0000066-140928181241064")
occ_download_get("0003983-140910143529206", overwrite = TRUE)
} # }
```
