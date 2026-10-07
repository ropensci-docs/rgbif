# List datasets that are deleted or have no endpoint.

List datasets that are deleted or have no endpoint.

## Usage

``` r
dataset_duplicate(limit = 20, start = NULL, curlopts = list(http_version = 2))

dataset_noendpoint(limit = 20, start = NULL, curlopts = list(http_version = 2))
```

## Arguments

- limit:

  Controls the number of results in the page.

- start:

  Determines the start for the search results.

- curlopts:

  options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

## Value

A `list`.

## Details

Get a list of deleted datasets or datasets with no endpoint. You get the
full and no parameters aside from `limit` and `start` are accepted.

## Examples

``` r
if (FALSE) { # \dontrun{
dataset_noendpoint(limit=3)
} # }
```
