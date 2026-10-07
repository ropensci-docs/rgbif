# Search for catalog numbers, collection codes, collector names, and institution codes.

Search for catalog numbers, collection codes, collector names, and
institution codes.

## Usage

``` r
occ_metadata(
  type = "catalogNumber",
  q = NULL,
  limit = 5,
  pretty = TRUE,
  curlopts = list(http_version = 2)
)
```

## Arguments

- type:

  Type of data, one of catalogNumber, collectionCode, recordedBy, or
  institutionCode. Unique partial strings work too, like 'cat' for
  catalogNumber

- q:

  Search term

- limit:

  Number of results, default=5

- pretty:

  Pretty as true (Default) uses cat to print data, `FALSE` gives
  character strings.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## References

<https://www.gbif.org/developer/occurrence#search>

## Examples

``` r
if (FALSE) { # \dontrun{
# catalog number
occ_metadata(type = "catalogNumber", q=122)

# collection code
occ_metadata(type = "collectionCode", q=12)

# institution code
occ_metadata(type = "institutionCode", q='GB')

# recorded by
occ_metadata(type = "recordedBy", q='scott')

# data as character strings
occ_metadata(type = "catalogNumber", q=122, pretty=FALSE)

# Change number of results returned
occ_metadata(type = "catalogNumber", q=122, limit=10)

# Partial unique type strings work too
occ_metadata(type = "cat", q=122)

# Pass on curl options
occ_metadata(type = "cat", q=122, curlopts = list(verbose = TRUE))
} # }
```
