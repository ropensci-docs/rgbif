# Facet GBIF occurrences

Facet GBIF occurrences

## Usage

``` r
occ_facet(facet, facetMincount = NULL, curlopts = list(http_version = 2), ...)
```

## Arguments

- facet:

  (character) a character vector of length 1 or greater. Required.

- facetMincount:

  (numeric) minimum number of records to be included in the faceting
  results

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

- ...:

  Facet parameters, such as for paging based on each facet variable,
  e.g., `country.facetLimit`

## Value

A list of tibbles (data.frame's) for each facet (each element of the
facet parameter).

## Details

All fields can be faceted on except for last "lastInterpreted",
"eventDate", and "geometry"

If a faceted variable is not found, it is silently dropped, returning
nothing for that query

## See also

[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
also has faceting ability, but can include occurrence data in addition
to facets.

## Examples

``` r
if (FALSE) { # \dontrun{
occ_facet(facet = "country")

# facetMincount - minimum number of records to be included
#   in the faceting results
occ_facet(facet = "country", facetMincount = 30000000L)
occ_facet(facet = c("country", "basisOfRecord"))

# paging with many facets
occ_facet(
  facet = c("country", "basisOfRecord", "hasCoordinate"),
  country.facetLimit = 3,
  basisOfRecord.facetLimit = 6
)

# paging
## limit
occ_facet(facet = "country", country.facetLimit = 3)
## offset
occ_facet(facet = "country", country.facetLimit = 3,
  country.facetOffset = 3)

# Pass on curl options
occ_facet(facet = "country", country.facetLimit = 3,
  curlopts = list(verbose = TRUE))
} # }
```
