# List countries for a download

List countries for a download

## Usage

``` r
occ_download_countries(
  key,
  sortBy = NULL,
  sortOrder = NULL,
  limit = 20,
  start = 0,
  curlopts = list(http_version = 2)
)
```

## Arguments

- key:

  A key generated from a request, like that from
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

- sortBy:

  (character) Sort field. One of `COUNTRY_CODE` or `RECORD_COUNT`.
  Optional.

- sortOrder:

  (character) Sort order. One of `ASC` or `DESC`. Optional.

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

- results: a tibble with the results, with columns: `downloadKey`,
  `publishingCountryCode`, `numberRecords`

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_countries(key="0003983-140910143529206")
occ_download_countries(key="0003983-140910143529206", limit = 3)
occ_download_countries(key="0003983-140910143529206", limit = 3, start = 10)
occ_download_countries(key="0003983-140910143529206", sortBy = "RECORD_COUNT",
  sortOrder = "DESC")
} # }
```
