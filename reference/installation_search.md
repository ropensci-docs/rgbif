# Search for installations

Search for installations

## Usage

``` r
installation_search(
  query = NULL,
  type = NULL,
  identifierType = NULL,
  identifier = NULL,
  machineTagNamespace = NULL,
  machineTagName = NULL,
  machineTagValue = NULL,
  modified = NULL,
  limit = 20,
  offset = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- query:

  A search query string.

- type:

  Choose from : IPT_INSTALLATION, DGIR INSTALLATION, TAPIR_INSTALLATION,
  BIOCASE_INSTALLATION, HTTP_INSTALLATION, SYMBIOTA_INSTALLATION,
  EARTHCAPE_INSTALLATION, MDT_INSTALLATION. Only accepts one value.

- identifierType:

  Choose from : URL, LSID, HANDLER, DOI, UUID, FTP, URI, UNKNOWN,
  GBIF_PORTAL, GBIF_NODE, GBIF_PARTICIPANT, GRSCICOLL_ID, GRSCICOLL_URI,
  IH_IRN, ROR, GRID, CITES, SYMBIOTA_UUID, WIKIDATA, NCBI_BIOCOLLECTION,
  ISIL, CLB_DATASET_KEY.

- identifier:

  An identifier of the type given by the identifierType parameter, for
  example a DOI or UUID.

- machineTagNamespace:

  Filters for entities with a machine tag in the specified namespace.

- machineTagName:

  Filters for entities with a machine tag with the specified name (use
  in combination with the machineTagNamespace parameter).

- machineTagValue:

  Filters for entities with a machine tag with the specified value (use
  in combination with the machineTagNamespace and machineTagName
  parameters).

- modified:

  The modified date of the dataset. Accepts ranges and a `*` can be used
  as a wildcard, e.g. modified=2023-04-01,`*`

- limit:

  The maximum number of results to return. Defaults to 20.

- offset:

  The offset of the first result to return.

- curlopts:

  A list of curl options to pass to the request.

## Value

A `list`

## Examples

``` r
if (FALSE) { # \dontrun{
installation_search() 
installation_search(query="Estonia")
installation_search(type="IPT_INSTALLATION") 
installation_search(modified="2023-04-01,*")

} # }
```
