# Nodes metadata.

Nodes metadata.

## Usage

``` r
nodes(
  data = "all",
  uuid = NULL,
  query = NULL,
  identifier = NULL,
  identifierType = NULL,
  limit = 100,
  start = NULL,
  isocode = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- data:

  The type of data to get. One or more of: 'organization', 'endpoint',
  'identifier', 'tag', 'machineTag', 'comment', 'pendingEndorsement',
  'country', 'dataset', 'installation', or the special 'all'. Default:
  `'all'`

- uuid:

  UUID of the data node provider. This must be specified if data is
  anything other than 'all'.

- query:

  Query nodes. Only used when `data='all'`

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

- isocode:

  A 2 letter country code. Only used if data='country'.

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

<https://www.gbif.org/developer/registry#nodes>

## Examples

``` r
if (FALSE) { # \dontrun{
nodes(limit=5)
nodes(uuid="1193638d-32d1-43f0-a855-8727c94299d8")
nodes(data='identifier', uuid="03e816b3-8f58-49ae-bc12-4e18b358d6d9")
nodes(data=c('identifier','organization','comment'),
  uuid="03e816b3-8f58-49ae-bc12-4e18b358d6d9")

uuids = c("8cb55387-7802-40e8-86d6-d357a583c596",
  "02c40d2a-1cba-4633-90b7-e36e5e97aba8",
  "7a17efec-0a6a-424c-b743-f715852c3c1f",
  "b797ce0f-47e6-4231-b048-6b62ca3b0f55",
  "1193638d-32d1-43f0-a855-8727c94299d8",
  "d3499f89-5bc0-4454-8cdb-60bead228a6d",
  "cdc9736d-5ff7-4ece-9959-3c744360cdb3",
  "a8b16421-d80b-4ef3-8f22-098b01a89255",
  "8df8d012-8e64-4c8a-886e-521a3bdfa623",
  "b35cf8f1-748d-467a-adca-4f9170f20a4e",
  "03e816b3-8f58-49ae-bc12-4e18b358d6d9",
  "073d1223-70b1-4433-bb21-dd70afe3053b",
  "07dfe2f9-5116-4922-9a8a-3e0912276a72",
  "086f5148-c0a8-469b-84cc-cce5342f9242",
  "0909d601-bda2-42df-9e63-a6d51847ebce",
  "0e0181bf-9c78-4676-bdc3-54765e661bb8",
  "109aea14-c252-4a85-96e2-f5f4d5d088f4",
  "169eb292-376b-4cc6-8e31-9c2c432de0ad",
  "1e789bc9-79fc-4e60-a49e-89dfc45a7188",
  "1f94b3ca-9345-4d65-afe2-4bace93aa0fe")

res <- lapply(uuids, function(x) nodes(x, data='identifier')$data)
res <- res[!sapply(res, NROW)==0]
res[1]

# Pass on curl options
nodes(limit=20, curlopts=list(verbose=TRUE))
} # }
```
