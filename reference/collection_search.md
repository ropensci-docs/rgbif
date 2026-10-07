# Search GRSciColl collections

Search GRSciColl collections

## Usage

``` r
collection_search(
  query = NULL,
  name = NULL,
  fuzzyName = NULL,
  preservationType = NULL,
  contentType = NULL,
  numberSpecimens = NULL,
  occurrenceCount = NULL,
  typeSpecimenCount = NULL,
  accessionStatus = NULL,
  personalCollection = NULL,
  sourceId = NULL,
  source = NULL,
  code = NULL,
  alternativeCode = NULL,
  contact = NULL,
  contactUserId = NULL,
  contactEmail = NULL,
  institutionKey = NULL,
  country = NULL,
  city = NULL,
  gbifRegion = NULL,
  machineTagNamespace = NULL,
  machineTagName = NULL,
  machineTagValue = NULL,
  identifier = NULL,
  identifierType = NULL,
  active = NULL,
  displayOnNHCPortal = NULL,
  masterSourceType = NULL,
  replacedBy = NULL,
  sortBy = NULL,
  sortOrder = NULL,
  offset = NULL,
  limit = NULL,
  format = NULL,
  curlopts = list(http_version = 2)
)

collection_export(
  query = NULL,
  name = NULL,
  fuzzyName = NULL,
  preservationType = NULL,
  contentType = NULL,
  numberSpecimens = NULL,
  occurrenceCount = NULL,
  typeSpecimenCount = NULL,
  accessionStatus = NULL,
  personalCollection = NULL,
  sourceId = NULL,
  source = NULL,
  code = NULL,
  alternativeCode = NULL,
  contact = NULL,
  contactUserId = NULL,
  contactEmail = NULL,
  institution = NULL,
  institutionKey = NULL,
  country = NULL,
  city = NULL,
  gbifRegion = NULL,
  machineTagNamespace = NULL,
  machineTagName = NULL,
  machineTagValue = NULL,
  identifier = NULL,
  identifierType = NULL,
  active = NULL,
  displayOnNHCPortal = NULL,
  masterSourceType = NULL,
  replacedBy = NULL,
  sortBy = NULL,
  sortOrder = NULL,
  offset = NULL,
  limit = NULL,
  format = "TSV",
  curlopts = list()
)
```

## Arguments

- query:

  Simple full text search parameter. The value for this parameter can be
  a simple word or a phrase. Wildcards are not supported.

- name:

  Name of a GrSciColl institution or collection.

- fuzzyName:

  It searches by name fuzzily so the parameter doesn't have to be the
  exact name.

- preservationType:

  Preservation type of a GrSciColl collection. Accepts multiple values.

- contentType:

  Content type of a GrSciColl collection. See here for accepted values :
  https://techdocs.gbif.org/en/openapi/v1/registry#/Collections/listCollections

- numberSpecimens:

  Number of specimens. It supports ranges and a `*` can be used as a
  wildcard.

- occurrenceCount:

  (character) Count of occurrences linked. It supports ranges and a `*`
  can be used as a wildcard. Optional parameter for filtering results.

- typeSpecimenCount:

  (character) Count of type specimens linked. It supports ranges and a
  `*` can be used as a wildcard. Optional parameter for filtering
  results.

- accessionStatus:

  Accession status of a GrSciColl collection. Accepted values :
  INSTITUTIONAL, PROJECT

- personalCollection:

  Flag for personal GRSciColl collections.

- sourceId:

  sourceId of MasterSourceMetadata.

- source:

  Source attribute of MasterSourceMetadata. Accepted values : DATASET,
  ORGANIZATION, IH_IRN

- code:

  Code of a GrSciColl institution or collection.

- alternativeCode:

  Alternative code of a GrSciColl institution or collection.

- contact:

  Filters collections and institutions whose contacts contain the person
  key specified.

- contactUserId:

  (numeric) Filters collections by the user ID of a contact. Optional
  parameter for filtering results.

- contactEmail:

  (character) Filters collections by the email of a contact. Optional
  parameter for filtering results.

- institutionKey:

  Keys of institutions to filter by.

- country:

  Filters by country given as a ISO 639-1 (2 letter) country code.

- city:

  Filters by the city of the address. It searches in both the physical
  and the mailing address.

- gbifRegion:

  Filters by a gbif region Available values : AFRICA, ASIA, EUROPE,
  NORTH_AMERICA, OCEANIA, LATIN_AMERICA, ANTARCTICA.

- machineTagNamespace:

  Filters for entities with a machine tag in the specified namespace.

- machineTagName:

  Filters for entities with a machine tag with the specified name (use
  in combination with the machineTagNamespace parameter).

- machineTagValue:

  Filters for entities with a machine tag with the specified value (use
  in combination with the machineTagNamespace and machineTagName
  parameters).

- identifier:

  An identifier of the type given by the identifierType parameter, for
  example a DOI or UUID.

- identifierType:

  An identifier type for the identifier parameter. Available values :
  URL, LSID, HANDLER, DOI, UUID, FTP, URI, UNKNOWN, GBIF_PORTAL,
  GBIF_NODE, GBIF_PARTICIPANT, GRSCICOLL_ID, GRSCICOLL_URI, IH_IRN, ROR,
  GRID, CITES, SYMBIOTA_UUID, WIKIDATA, NCBI_BIOCOLLECTION, ISIL,
  CLB_DATASET_KEY.

- active:

  Active status of a GrSciColl institution or collection.

- displayOnNHCPortal:

  Flag to show this record in the NHC portal.

- masterSourceType:

  The master source type of a GRSciColl institution. or collection.
  Available values : GRSCICOLL, GBIF_REGISTRY, IH.

- replacedBy:

  Key of the entity that replaced another entity.

- sortBy:

  Field to sort the results by. It only supports the fields contained in
  the enum. Available values : NUMBER_SPECIMENS.

- sortOrder:

  Sort order to use with the sortBy parameter. Available values : ASC,
  DESC.

- offset:

  Determines the offset for the search results.

- limit:

  Controls the number of results in the page. Default 20.

- format:

  (character) Format of the export. Default is "TSV". Only used for
  collection_export.

- curlopts:

  curlopts options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

- institution:

  Name of institutions hosting collections.

## Value

a `list`

## Details

Will return GRSciColl collections data. collection_export will return
all of the results in a single `tibble`, while collection_search will
return a sample of results.

## References

https://scientific-collections.gbif.org/connected-systems#grscicoll-data-coming-from-other-sources

## Examples

``` r
if (FALSE) { # \dontrun{
  collection_search(query="insect",limit=2)
  collection_search(name="Insects;Entomology", limit=2)
  collection_search(numberSpecimens = "0,100", limit=1)
  collection_search(institutionKey = "6a6ac6c5-1b8a-48db-91a2-f8661274ff80"
  , limit = 1)
  collection_search(query = "insect", country = "US;GB", limit=1)
} # } 
```
