# Networks metadata.

Networks metadata.

## Usage

``` r
networks(
  data = "all",
  uuid = NULL,
  query = NULL,
  identifier = NULL,
  identifierType = NULL,
  limit = 100,
  start = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- data:

  The type of data to get. One or more of: 'contact', 'endpoint',
  'identifier', 'tag', 'machineTag', 'comment', 'constituents', or the
  special 'all'. Default: `'all'`

- uuid:

  UUID of the data network provider. This must be specified if data is
  anything other than 'all'. Only 1 can be passed in

- query:

  Query nodes. Only used when `data='all'`. Ignored otherwise.

- identifier:

  The value for this parameter can be a simple string or integer, e.g.
  `identifier=120`. This parameter doesn't seem to work right now.

- identifierType:

  Used in combination with the identifier parameter to filter
  identifiers by identifier type. See details. This parameter doesn't
  seem to work right now.

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

## Details

identifierType options:

- DOI No description.

- FTP No description.

- GBIF_NODE Identifies the node (e.g: `DK` for Denmark, `sp2000` for
  Species 2000).

- GBIF_PARTICIPANT Participant identifier from the GBIF IMS Filemaker
  system.

- GBIF_PORTAL Indicates the identifier originated from an auto_increment
  column in the portal.data_provider or portal.data_resource table
  respectively.

- HANDLER No description.

- LSID Reference controlled by a separate system, used for example by
  DOI.

- SOURCE_ID No description.

- UNKNOWN No description.

- URI No description.

- URL No description.

- UUID No description.

## References

<https://www.gbif.org/developer/registry#networks>

## Examples

``` r
if (FALSE) { # \dontrun{
networks()
networks(uuid='2b7c7b4f-4d4f-40d3-94de-c28b6fa054a6')

# curl options
networks(curlopts = list(verbose=TRUE))
} # }
```
