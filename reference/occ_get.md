# Get data for GBIF occurrences by occurrence key

Get data for GBIF occurrences by occurrence key

## Usage

``` r
occ_get(
  key,
  fields = "minimal",
  curlopts = list(http_version = 2),
  return = NULL,
  verbatim = NULL
)

occ_get_verbatim(key, fields = "minimal", curlopts = list(http_version = 2))
```

## Arguments

- key:

  (numeric/integer) one or more occurrence keys. required

- fields:

  (character) Default ("minimal") will return just taxon name, key,
  latitude, and longitude. 'all' returns all fields. Or specify each
  field you want returned by name, e.g. fields = c('name',
  'decimalLatitude','altitude').

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

- return:

  Defunct. All components are returned now; index to the one(s) you want

- verbatim:

  Defunct. verbatim records can now be retrieved using
  `occ_get_verbatim()`

## Value

For `occ_get` a list of lists. For `occ_get_verbatim` a data.frame

## References

<https://www.gbif.org/developer/occurrence#occurrence>

## Examples

``` r
if (FALSE) { # \dontrun{
occ_get(key=855998194)

# many occurrences
occ_get(key=c(101010, 240713150, 855998194))

# Verbatim data
occ_get_verbatim(key=855998194)
occ_get_verbatim(key=855998194, fields='all')
occ_get_verbatim(key=855998194,
 fields=c('scientificName', 'lastCrawled', 'county'))
occ_get_verbatim(key=c(855998194, 620594291))
occ_get_verbatim(key=c(855998194, 620594291), fields='all')
occ_get_verbatim(key=c(855998194, 620594291),
   fields=c('scientificName', 'decimalLatitude', 'basisOfRecord'))

# curl options, pass in a named list
occ_get(key=855998194, curlopts = list(verbose=TRUE))
} # }
```
