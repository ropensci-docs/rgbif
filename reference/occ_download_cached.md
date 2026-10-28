# Check for downloads already in your GBIF account

Check for downloads already in your GBIF account

## Usage

``` r
occ_download_cached(
  ...,
  body = NULL,
  type = "and",
  format = "DWCA",
  user = NULL,
  pwd = NULL,
  email = NULL,
  refresh = FALSE,
  age = 30,
  curlopts = list(http_version = 2)
)
```

## Arguments

- ...:

  For
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  and
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
  one or more objects of class `occ_predicate` or `occ_predicate_list`,
  created by `pred*` functions (see
  [download_predicate_dsl](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)).
  If you use this, don't use `body` parameter.

- body:

  if you prefer to pass in the payload yourself, use this parameter. If
  you use this, don't pass anything to the dots. Accepts either an R
  list, or JSON. JSON is likely easier, since the JSON library jsonlite
  requires that you unbox strings that shouldn't be auto-converted to
  arrays, which is a bit tedious for large queries. optional

- type:

  (character) One of equals (=), and (&), or (\|), lessThan (\<),
  lessThanOrEquals (\<=), greaterThan (\>), greaterThanOrEquals (\>=),
  in, within, not (!), like, isNotNull

- format:

  (character) The download format. One of 'DWCA' (default),
  'SIMPLE_CSV', or 'SPECIES_LIST'

- user:

  (character) User name within GBIF's website. Required. See
  "Authentication" below

- pwd:

  (character) User password within GBIF's website. Required. See
  "Authentication" below

- email:

  (character) Email address to receive download notice done email.
  Required. See "Authentication" below

- refresh:

  (logical) refresh your list of downloads. on the first request of each
  R session we'll cache your stored GBIF occurrence downloads locally.
  you can refresh this list by setting `refresh=TRUE`; if you're in the
  same R session, and you've done many download requests, then
  refreshing may be a good idea if you're using this function

- age:

  (integer) number of days after which you want a new download. default:
  30

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
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
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# these are examples from the package maintainer's account;
# outcomes will vary by user
occ_download_cached(pred_gte("elevation", 12000L))
occ_download_cached(pred("catalogNumber", 217880))
occ_download_cached(pred_gte("decimalLatitude", 65),
  pred_lte("decimalLatitude", -65), type="or")
occ_download_cached(pred_gte("elevation", 12000L))
occ_download_cached(pred_gte("elevation", 12000L), refresh = TRUE)
} # }
```
