# Wait for an occurrence download to be done

Wait for an occurrence download to be done

## Usage

``` r
occ_download_wait(
  x,
  status_ping = 5,
  curlopts = list(http_version = 2),
  quiet = FALSE
)
```

## Arguments

- x:

  and object of class `occ_download` or downloadkey

- status_ping:

  (integer) seconds between each
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  request. default is 5, and cannot be \< 3

- curlopts:

  (list) curl options, as named list, passed on to
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)

- quiet:

  (logical) suppress messages. default: `FALSE`

## Value

an object of class `occ_download_meta`, see
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
for details

## Note

[`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
is similar, but handles many requests at once; `occ_download_wait`
handles one request at a time

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
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
if (FALSE) { # \dontrun{
x <- occ_download(
  pred("taxonKey", 9206251),
  pred_in("country", c("US", "MX")),
  pred_gte("year", 1971)
)
res <- occ_download_wait(x)
occ_download_meta(x)

# works also with a downloadkey
occ_download_wait("0000066-140928181241064") 

} # }
```
