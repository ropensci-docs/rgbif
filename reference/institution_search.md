# Search GRSciColl institutions

Search GRSciColl institutions

## Usage

``` r
institution_search(
  query = NULL,
  type = NULL,
  institutionalGovernance = NULL,
  disciplines = NULL,
  discipline = NULL,
  name = NULL,
  fuzzyName = NULL,
  numberSpecimens = NULL,
  occurrenceCount = NULL,
  typeSpecimenCount = NULL,
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

institution_export(
  query = NULL,
  type = NULL,
  institutionalGovernance = NULL,
  disciplines = NULL,
  name = NULL,
  fuzzyName = NULL,
  numberSpecimens = NULL,
  occurrenceCount = NULL,
  typeSpecimenCount = NULL,
  institution = NULL,
  contentType = NULL,
  preservationType = NULL,
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
  format = "TSV",
  curlopts = list()
)
```

## Arguments

- query:

  (character) Simple full text search parameter. The value for this
  parameter can be a simple word or a phrase. Wildcards are not
  supported

- type:

  (character) Type of a GrSciColl institution Available values :
  BIOMEDICAL_RESEARCH_INSTITUTE, BOTANICAL_GARDEN, HERBARIUM,
  LIVING_ORGANISM_COLLECTION, MEDICAL_RESEARCH_INSTITUTE, MUSEUM,
  MUSEUM_HERBARIUM_PRIVATE_NON_PROFIT, OTHER_INSTITUTIONAL_TYPE,
  OTHER_TYPE_RESEARCH_INSTITUTION_BIOREPOSITORY, UNIVERSITY_COLLEGE,
  ZOO_AQUARIUM

- institutionalGovernance:

  (character) Instutional governance of a GrSciColl institution
  Available values : ACADEMIC_FEDERAL, ACADEMIC_FOR_PROFIT,
  ACADEMIC_LOCAL, ACADEMIC_NON_PROFIT, ACADEMIC_STATE, FEDERAL,
  FOR_PROFIT, LOCAL, NON_PROFIT, OTHER, STATE.

- disciplines:

  (character) Discipline of a GrSciColl institution. Check available
  values :
  https://techdocs.gbif.org/en/openapi/v1/registry#/Institutions/listInstitutions

- discipline:

  (character) Discipline of a GrSciColl institution. Optional parameter
  for filtering results.

- name:

  (character) Name of a GrSciColl institution or collection

- fuzzyName:

  (character) It searches by name fuzzily so the parameter doesn't have
  to be the exact name.

- numberSpecimens:

  (character) Number of specimens. It supports ranges and a `*` can be
  used as a wildcard.

- occurrenceCount:

  (character) Count of occurrences linked. It supports ranges and a `*`
  can be used as a wildcard.

- typeSpecimenCount:

  (character) Count of type specimens linked. It supports ranges and a
  `*` can be used as a wildcard.

- sourceId:

  (character) sourceId of MasterSourceMetadata

- source:

  (character) Source attribute of MasterSourceMetadata Available values
  : DATASET, ORGANIZATION, IH_IRN

- code:

  (character) Code of a GrSciColl institution or collection.

- alternativeCode:

  (character) Alternative code of a GrSciColl institution.

- contact:

  (character) Filters collections and institutions whose contacts
  contain the person key specified.

- contactUserId:

  (numeric) Filters institutions by the user ID of a contact. Optional
  parameter for filtering results.

- contactEmail:

  (character) Filters institutions by the email of a contact. Optional
  parameter for filtering results.

- institutionKey:

  (character) Keys of institutions to filter by.

- country:

  (character) Filters by country given as a ISO 639-1 (2 letter) country
  code.

- city:

  (character) Filters by the city of the address. It searches in both
  the physical and the mailing address.

- gbifRegion:

  (character) Filters by a gbif region. Available values : AFRICA, ASIA,
  EUROPE, NORTH_AMERICA, OCEANIA, LATIN_AMERICA, ANTARCTICA.

- machineTagNamespace:

  (character) Filters for entities with a machine tag in the specified
  namespace.

- machineTagName:

  (character) Filters for entities with a machine tag with the specified
  name (use in combination with the machineTagNamespace parameter).

- machineTagValue:

  (character) Filters for entities with a machine tag with the specified
  value (use in combination with the machineTagNamespace and
  machineTagName parameters).

- identifier:

  (character) An identifier of the type given by the `identifierType`
  parameter, for example a DOI or UUID.

- identifierType:

  (character) An identifier type for the identifier parameter. Available
  values : URL, LSID, HANDLER, DOI, UUID, FTP, URI, UNKNOWN,
  GBIF_PORTAL, GBIF_NODE, GBIF_PARTICIPANT, GRSCICOLL_ID, GRSCICOLL_URI,
  IH_IRN, ROR, GRID, CITES, SYMBIOTA_UUID, WIKIDATA, NCBI_BIOCOLLECTION,
  ISIL, CLB_DATASET_KEY.

- active:

  (logical) Active status of a GrSciColl institution or collection.

- displayOnNHCPortal:

  (logical) Flag to show this record in the NHC portal.

- masterSourceType:

  (character) The master source type of a GRSciColl institution or
  collection. Available values : GRSCICOLL, GBIF_REGISTRY, IH.

- replacedBy:

  (character) Key of the entity that replaced another entity.

- sortBy:

  (character) Field to sort the results by. It only supports the fields
  contained in the enum. Available values : NUMBER_SPECIMENS.

- sortOrder:

  (character) Sort order to use with the sortBy parameter. Available
  values : ASC, DESC.

- offset:

  (numeric) Determines the offset for the search results.

- limit:

  (numeric) Controls the number of results in the page. Default 20.

- format:

  (character) Format of the export. Default is "TSV". Only used for
  institution_export.

- curlopts:

  (list) curlopts options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

- institution:

  (character) Filters collections by institution key or name. Optional
  parameter for filtering results. Only used for institution_export.

- contentType:

  (character) Content type of a GrSciColl collection. Optional parameter
  for filtering results. Only used for institution_export.

- preservationType:

  (character) Preservation type of a GrSciColl collection. Optional
  parameter for filtering results. Only used for institution_export.

- accessionStatus:

  (character) Accession status of a GrSciColl collection. Optional
  parameter for filtering results. Only used for institution_export.

- personalCollection:

  (logical) Whether the collection is a personal collection. Optional
  parameter for filtering results. Only used for institution_export.

## Value

A `list`

## Details

Will return GRSciColl collections data. institution_export will return
all of the results in a single `tibble`, while institution_search will
return a sample of results.

## Examples

``` r
if (FALSE) { # \dontrun{
institution_search(query="Kansas",limit=1)
institution_search(numberSpecimens = "1000,*",limit=2)
institution_search(source = "IH_IRN") 
institution_search(country = "US;GB")
institution_search(typeSpecimenCount = "10,100")

} # }
```
