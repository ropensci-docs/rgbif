# Import a downloaded file from GBIF.

Import a downloaded file from GBIF.

## Usage

``` r
occ_download_import(
  x = NULL,
  key = NULL,
  path = ".",
  fill = FALSE,
  encoding = "UTF-8",
  ...
)

as.download(path = ".", key = NULL)

# S3 method for class 'character'
as.download(path = ".", key = NULL)

# S3 method for class 'download'
as.download(path = ".", key = NULL)
```

## Arguments

- x:

  The output of a call to `occ_download_get`

- key:

  A key generated from a request, like that from `occ_download`

- path:

  Path to unzip file to. Default: `"."` Writes to folder matching zip
  file name

- fill:

  (logical) (default: `FALSE`). If `TRUE` then in case the rows have
  unequal length, blank fields are implicitly filled. passed on to
  `fill` parameter in
  [data.table::fread](https://rdrr.io/pkg/data.table/man/fread.html).

- encoding:

  (character) encoding to read in data; passed to
  [`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html).
  default: "UTF-8". other allowed options: "Latin-1" and "unknown". see
  [`?data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html)
  docs

- ...:

  parameters passed on to
  [`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html).
  See `fread` docs for details. Some `fread` parameters that may be
  particular useful here are: `select` (select which columns to read in;
  others are dropped), `nrows` (only read in a certain number of rows)

## Value

a tibble (data.frame)

## Details

You can provide either x as input, or both key and path. We use
[`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html)
internally to read data.

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

## Problems reading data

You may run into errors when using `occ_download_import()`; most often
these are due to
[`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html)
not being able to parse the `occurrence.txt` file correctly. The `fill`
parameter passes down to
[`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html)
and the `...` allows you to pass on any other parameters that
[`data.table::fread()`](https://rdrr.io/pkg/data.table/man/fread.html)
accepts. Read the docs for `fread` for help.

## countryCode result column and Namibia

The country code for Namibia is `"NA"`. Unfortunately in R an `"NA"`
string will be read in to R as an NA/missing. To avoid this, in this
function we read in the data, then convert an NA/missing values to the
character string `"NA"`. When a country code is truly missing it will be
an empty string.

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
[`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md),
[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md),
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
# First, kick off at least 1 download, then wait for the job to be complete
# Then use your download keys
res <- occ_download_get(key="0000066-140928181241064", overwrite=TRUE)
occ_download_import(res)

occ_download_get(key="0000066-140928181241064", overwrite = TRUE) %>%
  occ_download_import

# coerce a file path to the right class to feed to occ_download_import
# as.download("0000066-140928181241064.zip")
# as.download(key = "0000066-140928181241064")
# occ_download_import(as.download("0000066-140928181241064.zip"))

# download a dump that has a CSV file
# res <- occ_download_get(key = "0001369-160509122628363", overwrite=TRUE)
# occ_download_import(res)
# occ_download_import(key = "0001369-160509122628363")

# download and import a species list (in csv format)
# x <- occ_download_get("0000172-190415153152247")
# occ_download_import(x)
} # }
```
