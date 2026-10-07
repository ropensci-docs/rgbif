# Search for datasets and dataset metadata.

Search for datasets and dataset metadata.

## Usage

``` r
datasets(
  data = "all",
  type = NULL,
  uuid = NULL,
  query = NULL,
  id = NULL,
  limit = 100,
  start = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- data:

  The type of data to get. One or more of: 'organization', 'contact',
  'endpoint', 'identifier', 'tag', 'machinetag', 'comment',
  'constituents', 'document', 'metadata', 'deleted', 'duplicate',
  'subDataset', 'withNoEndpoint', or the special 'all'. Default: `all`

- type:

  Type of dataset. Options: include occurrence, checklist, metadata, or
  sampling_event.

- uuid:

  UUID of the data node provider. This must be specified if data is
  anything other than `all`

- query:

  Query term(s). Only used when `data=all`

- id:

  A metadata document id.

- limit:

  Number of records to return. Default: 100. Maximum: 1000.

- start:

  Record number to start at. Default: 0. Use in combination with `limit`
  to page through results.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A list.

## References

<https://www.gbif.org/developer/registry#datasets>

## Examples

``` r
if (FALSE) { # \dontrun{
datasets(limit=5)
datasets(type="occurrence", limit=10)
datasets(uuid="a6998220-7e3a-485d-9cd6-73076bd85657")
datasets(data='contact', uuid="a6998220-7e3a-485d-9cd6-73076bd85657")
datasets(data='metadata', uuid="a6998220-7e3a-485d-9cd6-73076bd85657")
datasets(data='metadata', uuid="a6998220-7e3a-485d-9cd6-73076bd85657",
  id=598)
datasets(data=c('deleted','duplicate'))
datasets(data=c('deleted','duplicate'), limit=1)

# curl options
datasets(data=c('deleted','duplicate'), curlopts = list(verbose=TRUE))
} # }
```
