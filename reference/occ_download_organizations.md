# List organizations for a download

List organizations for a download

## Usage

``` r
occ_download_organizations(
  key,
  organizationTitle = NULL,
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

- organizationTitle:

  (character) Organization title filter. Optional.

- sortBy:

  (character) Sort field. One of `ORGANIZATION_TITLE`, `COUNTRY_CODE` or
  `RECORD_COUNT`. Optional.

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
  `organizationKey`, `organizationTitle`, `numberRecords`,
  `publishingCountryCode`

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_organizations(key="0024953-260519110011954")
occ_download_organizations(key="0024953-260519110011954", limit = 3)
occ_download_organizations(
  key="0024953-260519110011954",
  organizationTitle = "University of Alaska Museum of the North"
)
occ_download_organizations(key="0024953-260519110011954", sortBy = "RECORD_COUNT",
  sortOrder = "DESC")
} # }
```
