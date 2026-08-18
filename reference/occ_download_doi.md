# Get download meta data from a doi

Get download meta data from a doi

## Usage

``` r
occ_download_doi(doi = NULL, curlopts = list(http_version = 2))
```

## Arguments

- doi:

  (character) the doi of the download you want to get metadata for.

- curlopts:

  (list) named list of curl options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

## Value

a list.

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_doi("10.15468/dl.zdfkkf")

occ_download_doi("10.15468/dl.zdfkkf")$key %>%
occ_download_get() %>%
occ_download_import() 

} # }
```
