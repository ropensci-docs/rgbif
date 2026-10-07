# Get a GBIF dataset from a doi

Get a GBIF dataset from a doi

## Usage

``` r
dataset_doi(
  doi = NULL,
  limit = 20,
  start = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- doi:

  the doi of the dataset you wish to lookup.

- limit:

  Controls the number of results in the page.

- start:

  Determines the offset for the search results.

- curlopts:

  options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

## Value

A `list`.

## Details

This function allows for dataset lookup using a doi. Be aware that some
doi have more than one dataset associated with them.

## Examples

``` r
if (FALSE) { # \dontrun{
dataset_doi('10.15468/igasai')
} # }
```
