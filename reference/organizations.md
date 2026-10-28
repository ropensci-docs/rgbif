# Organizations metadata.

Organizations metadata.

## Usage

``` r
organizations(
  data = "all",
  country = NULL,
  uuid = NULL,
  query = NULL,
  limit = 100,
  start = NULL,
  isEndorsed = NULL,
  networkKey = NULL,
  numPublishedDatasets = NULL,
  canModify = NULL,
  identifierType = NULL,
  identifier = NULL,
  machineTagNamespace = NULL,
  machineTagName = NULL,
  machineTagValue = NULL,
  modified = NULL,
  created = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- data:

  (character) The type of data to get. One or more of: 'organization',
  'contact', 'endpoint', 'identifier', 'tag', 'machineTag', 'comment',
  'hostedDataset', 'ownedDataset', 'deleted', 'pending',
  'nonPublishing', 'installation' or the special 'all'. Default: `'all'`

- country:

  (character) Filters by country.

- uuid:

  (character) UUID of the data node provider. This must be specified if
  data is anything other than 'all', 'deleted', 'pending', or
  'nonPublishing'.

- query:

  (character) Query nodes. Only used when `data='all'`

- limit:

  Number of records to return. Default: 100. Maximum: 1000.

- start:

  Record number to start at. Default: 0. Use in combination with `limit`
  to page through results.

- isEndorsed:

  (logical) Whether the organization is endorsed by a GBIF node.
  Optional.

- networkKey:

  (character) The UUID key of the network to filter organizations by.
  Optional.

- numPublishedDatasets:

  (integer) Filters by the number of published datasets. Optional.

- canModify:

  (logical) Whether the organization can be modified. Optional.

- identifierType:

  (character) Used in combination with the identifier parameter to
  filter identifiers by identifier type. One of: DOI, FTP, GBIF_NODE,
  GBIF_PARTICIPANT, GBIF_PORTAL, HANDLER, LSID, SOURCE_ID, UNKNOWN, URI,
  URL, UUID. Optional.

- identifier:

  (character) The value for this parameter can be a simple string or
  integer, e.g. `identifier=120`. Optional.

- machineTagNamespace:

  (character) Filters by machine tag namespace. Optional.

- machineTagName:

  (character) Filters by machine tag name. Optional.

- machineTagValue:

  (character) Filters by machine tag value. Optional.

- modified:

  (character) Filters by the date the organization was last modified.
  Optional.

- created:

  (character) Filters by the date the organization was created.
  Optional.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A list of length of two, consisting of a data.frame `meta` when uuid is
NULL, and `data` which can either be a list or a data.frame depending on
the requested type of data.

## References

<https://www.gbif.org/developer/registry#organizations>

## Examples

``` r
if (FALSE) { # \dontrun{
organizations(limit=5)
organizations(query="france", limit=5)
organizations(country = "SPAIN")
organizations(uuid="4b4b2111-ee51-45f5-bf5e-f535f4a1c9dc")
organizations(data='contact', uuid="4b4b2111-ee51-45f5-bf5e-f535f4a1c9dc")
organizations(data='pending')
organizations(data=c('contact','endpoint'),
  uuid="4b4b2111-ee51-45f5-bf5e-f535f4a1c9dc")
organizations(data="installation", uuid="96710dc8-fecb-440d-ae3e-c34ae8a9616f")    
organizations(isEndorsed=TRUE, limit=5)
organizations(networkKey="99d66b6c-9087-452f-a9d4-f15f2c2d0e7e", limit=5)

# Pass on curl options
organizations(query="spain", curlopts = list(verbose=TRUE))
} # }
```
