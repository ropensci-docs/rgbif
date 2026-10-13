# Get citation for datasets used

Get citation for datasets used

## Usage

``` r
gbif_citation(x)
```

## Arguments

- x:

  (character) Result of call to
  [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md),
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md).

## Value

list with S3 class assigned, used by a print method to pretty print
citation information. Though you can unclass the output or just index to
the named items as needed.

## Details

The function is deprecated for use with
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
and
[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
results, and is deprecated for use with datasetKeys and gbifids.
Instead, we encourage you to use
[`derived_dataset()`](https://docs.ropensci.org/rgbif/reference/derived_dataset.md)
instead.

[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md)
and
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
results are still supported.

## Examples

``` r
if (FALSE) { # \dontrun{
# Downloads
## occ_download_get()
# d1 <- occ_download(pred("country", "BG"), pred_gte("year", 2020))
# occ_download_meta(d1) # wait until status = succeeded
# d1 <- occ_download_get(d1, overwrite = TRUE)
# gbif_citation(d1)

## occ_download_meta()
# key <- "0000122-171020152545675"
# res <- occ_download_meta(key)
# gbif_citation(res)
} # }
```
