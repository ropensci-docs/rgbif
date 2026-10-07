# Describes the fields available in GBIF downloads

Describes the fields available in GBIF downloads

## Usage

``` r
occ_download_describe(x = "dwca", curlopts = list(http_version = 2))
```

## Arguments

- x:

  a character string (default: "dwca"). Accepted values: "simpleCsv",
  "simpleAvro", "simpleParquet","speciesList", "sql".

- curlopts:

  list of named curl options passed on to HttpClient. see
  curl::curl_options for curl options.

## Value

a list.

## Details

The function returns a list with the fields available in GBIF downloads.
It is considered experimental by GBIF, so the output might change in the
future.

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_describe("dwca")$verbatimFields
occ_download_describe("dwca")$verbatimExtensions
occ_download_describe("simpleCsv")$fields
occ_download_describe("sql")$fields
} # }
```
