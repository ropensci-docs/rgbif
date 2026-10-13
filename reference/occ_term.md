# Get occurrence terms.

Get occurrence terms.

## Usage

``` r
occ_term(curlopts = list(http_version = 2))
```

## Arguments

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A `data.frame` with occurrence term definitions.

## References

<https://www.gbif.org/developer/occurrence>

## Examples

``` r
if (FALSE) { # \dontrun{
occ_term()

# Pass on curl options
occ_term(curlopts = list(verbose = TRUE))
} # }
```
