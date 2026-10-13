# Enumerations.

Many parts of the GBIF API make use of enumerations, i.e. controlled
vocabularies for specific topics - and are available via these functions

## Usage

``` r
enumeration(x = NULL, curlopts = list(http_version = 2))

enumeration_country(curlopts = list(http_version = 2))
```

## Arguments

- x:

  A given enumeration.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

`enumeration` returns a character vector, while `enumeration_country`
returns a data.frame.

## Examples

``` r
if (FALSE) { # \dontrun{
# basic enumeration
enumeration()
enumeration("NameType")
enumeration("MetadataType")
enumeration("TypeStatus")

# country enumeration
enumeration_country()

# curl options
enumeration(curlopts = list(verbose=TRUE))
} # }
```
