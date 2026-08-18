# Legacy alternative to occ_search

Legacy alternative to occ_search

## Usage

``` r
occ_data(
  taxonKey = NULL,
  scientificName = NULL,
  country = NULL,
  publishingCountry = NULL,
  hasCoordinate = NULL,
  typeStatus = NULL,
  recordNumber = NULL,
  lastInterpreted = NULL,
  continent = NULL,
  geometry = NULL,
  geom_big = "asis",
  geom_size = 40,
  geom_n = 10,
  recordedBy = NULL,
  recordedByID = NULL,
  identifiedByID = NULL,
  basisOfRecord = NULL,
  datasetKey = NULL,
  eventDate = NULL,
  catalogNumber = NULL,
  year = NULL,
  month = NULL,
  decimalLatitude = NULL,
  decimalLongitude = NULL,
  elevation = NULL,
  depth = NULL,
  institutionCode = NULL,
  collectionCode = NULL,
  hasGeospatialIssue = NULL,
  issue = NULL,
  search = NULL,
  mediaType = NULL,
  subgenusKey = NULL,
  repatriated = NULL,
  phylumKey = NULL,
  kingdomKey = NULL,
  classKey = NULL,
  orderKey = NULL,
  familyKey = NULL,
  genusKey = NULL,
  speciesKey = NULL,
  establishmentMeans = NULL,
  degreeOfEstablishment = NULL,
  protocol = NULL,
  license = NULL,
  organismId = NULL,
  publishingOrg = NULL,
  stateProvince = NULL,
  waterBody = NULL,
  locality = NULL,
  occurrenceStatus = "PRESENT",
  gadmGid = NULL,
  coordinateUncertaintyInMeters = NULL,
  verbatimScientificName = NULL,
  eventId = NULL,
  identifiedBy = NULL,
  networkKey = NULL,
  verbatimTaxonId = NULL,
  occurrenceId = NULL,
  organismQuantity = NULL,
  organismQuantityType = NULL,
  relativeOrganismQuantity = NULL,
  iucnRedListCategory = NULL,
  lifeStage = NULL,
  isInCluster = NULL,
  distanceFromCentroidInMeters = NULL,
  skip_validate = TRUE,
  limit = 500,
  start = 0,
  curlopts = list(http_version = 2)
)
```

## Arguments

- taxonKey:

  (numeric) A taxon key from the GBIF backbone. All included and synonym
  taxa are included in the search, so a search for aves with
  taxononKey=212 will match all birds, no matter which species. You can
  pass many keys to `occ_search(taxonKey=c(1,212))`.

- scientificName:

  A scientific name from the GBIF backbone. All included and synonym
  taxa are included in the search.

- country:

  (character) The 2-letter country code (ISO-3166-1) in which the
  occurrence was recorded.
  [`enumeration_country()`](https://docs.ropensci.org/rgbif/reference/enumeration.md).

- publishingCountry:

  The 2-letter country code (as per ISO-3166-1) of the country in which
  the occurrence was recorded. See
  [`enumeration_country()`](https://docs.ropensci.org/rgbif/reference/enumeration.md).

- hasCoordinate:

  (logical) Return only occurrence records with lat/long data (`TRUE`)
  or all records (`FALSE`, default).

- typeStatus:

  Type status of the specimen. One of many
  [options](https://www.gbif.org/occurrence/search?type_status=PARATYPE).

- recordNumber:

  Number recorded by collector of the data, different from GBIF record
  number.

- lastInterpreted:

  Date the record was last modified in GBIF, in ISO 8601 format: yyyy,
  yyyy-MM, yyyy-MM-dd, or MM-dd. Supports range queries,
  'smaller,larger' (e.g., '1990,1991', whereas '1991,1990' wouldn't
  work).

- continent:

  The source supplied continent.

  - "africa"

  - "antarctica"

  - "asia"

  - "europe"

  - "north_america"

  - "oceania"

  - "south_america"

  Continent is not inferred but only populated if provided by the
  dataset publisher. Applying this filter may exclude many relevant
  records.

- geometry:

  (character) Searches for occurrences inside a polygon in Well Known
  Text (WKT) format. A WKT shape written as either

  - "POINT"

  - "LINESTRING"

  - "LINEARRING"

  - "POLYGON"

  - "MULTIPOLYGON"

  For Example, "POLYGON((37.08 46.86,38.06 46.86,38.06 47.28,37.08
  47.28, 37.0 46.8))". See also the section **WKT** below.

- geom_big:

  (character) One"bbox" or "asis" (default).

- geom_size:

  (integer) An integer indicating size of the cell. Default: 40.

- geom_n:

  (integer) An integer indicating number of cells in each dimension.
  Default: 10.

- recordedBy:

  (character) The person who recorded the occurrence.

- recordedByID:

  (character) Identifier (e.g. ORCID) for the person who recorded the
  occurrence

- identifiedByID:

  (character) Identifier (e.g. ORCID) for the person who provided the
  taxonomic identification of the occurrence.

- basisOfRecord:

  (character) The specific nature of the data record. See
  [here](https://dwc.tdwg.org/terms/#dwc:basisOfRecord).

  - "FOSSIL_SPECIMEN"

  - "HUMAN_OBSERVATION"

  - "MATERIAL_CITATION"

  - "MATERIAL_SAMPLE"

  - "LIVING_SPECIMEN"

  - "MACHINE_OBSERVATION"

  - "OBSERVATION"

  - "PRESERVED_SPECIMEN"

  - "OCCURRENCE"

- datasetKey:

  (character) The occurrence dataset uuid key. That can be found in the
  dataset page url. For example, "7e380070-f762-11e1-a439-00145 eb45e9a"
  is the key for [Natural History Museum (London) Collection
  Specimens](https://www.gbif.org/dataset/7e380070-f762-11e1-a439-00145eb45e9a).

- eventDate:

  (character) Occurrence date in ISO 8601 format: yyyy, yyyy-MM,
  yyyy-MM-dd, or MM-dd. Supports range queries, 'smaller,larger'
  ('1990,1991', whereas '1991,1990' wouldn't work).

- catalogNumber:

  (character) An identifier of any form assigned by the source within a
  physical collection or digital dataset for the record which may not
  unique, but should be fairly unique in combination with the
  institution and collection code.

- year:

  The 4 digit year. A year of 98 will be interpreted as AD 98. Supports
  range queries, 'smaller,larger' (e.g., '1990,1991', whereas 1991,
  1990' wouldn't work).

- month:

  The month of the year, starting with 1 for January. Supports range
  queries, 'smaller,larger' (e.g., '1,2', whereas '2,1' wouldn't work).

- decimalLatitude:

  Latitude in decimals between -90 and 90 based on WGS84. Supports range
  queries, 'smaller,larger' (e.g., '25,30', whereas '30,25' wouldn't
  work).

- decimalLongitude:

  Longitude in decimals between -180 and 180 based on WGS84. Supports
  range queries (e.g., '-0.4,-0.2', whereas '-0.2,-0.4' wouldn't work).

- elevation:

  Elevation in meters above sea level. Supports range queries,
  'smaller,larger' (e.g., '5,30', whereas '30,5' wouldn't work).

- depth:

  Depth in meters relative to elevation. For example 10 meters below a
  lake surface with given elevation. Supports range queries,
  'smaller,larger' (e.g., '5,30', whereas '30,5' wouldn't work).

- institutionCode:

  An identifier of any form assigned by the source to identify the
  institution the record belongs to.

- collectionCode:

  (character) An identifier of any form assigned by the source to
  identify the physical collection or digital dataset uniquely within
  the text of an institution.

- hasGeospatialIssue:

  (logical) Includes/excludes occurrence records which contain spatial
  issues (as determined in our record interpretation), i.e.
  `hasGeospatialIssue=TRUE` returns only those records with spatial
  issues while `hasGeospatialIssue=FALSE` includes only records without
  spatial issues. The absence of this parameter returns any record with
  or without spatial issues.

- issue:

  (character) One or more of many possible issues with each occurrence
  record. Issues passed to this parameter filter results by the issue.
  One of many
  [options](https://gbif.github.io/gbif-api/apidocs/org/gbif/api/vocabulary/OccurrenceIssue.html).
  See [here](https://data-blog.gbif.org/post/issues-and-flags/) for
  definitions.

- search:

  (character) Query terms. The value for this parameter can be a simple
  word or a phrase. For example,
  [search="puma"](https://www.gbif.org/occurrence/search?q=puma)

- mediaType:

  (character) Media type of "MovingImage", "Sound", or "StillImage".

- subgenusKey:

  (numeric) Subgenus classification key.

- repatriated:

  (character) Searches for records whose publishing country is different
  to the country where the record was recorded in.

- phylumKey:

  (numeric) Phylum classification key.

- kingdomKey:

  (numeric) Kingdom classification key.

- classKey:

  (numeric) Class classification key.

- orderKey:

  (numeric) Order classification key.

- familyKey:

  (numeric) Family classification key.

- genusKey:

  (numeric) Genus classification key.

- speciesKey:

  (numeric) Species classification key.

- establishmentMeans:

  (character) provides information about whether an organism or
  organisms have been introduced to a given place and time through the
  direct or indirect activity of modern humans.

  - "Introduced"

  - "Native"

  - "NativeReintroduced"

  - "Vagrant"

  - "Uncertain"

  - "IntroducedAssistedColonisation"

- degreeOfEstablishment:

  (character) Provides information about degree to which an Organism
  survives, reproduces, and expands its range at the given place and
  time. One of many
  [options](https://www.gbif.org/occurrence/search?advanced=1&degree_of_establishment=Managed).

- protocol:

  (character) Protocol or mechanism used to provide the occurrence
  record. One of many
  [options](https://www.gbif.org/occurrence/search?protocol=DWC_ARCHIVE&advanced=1).

- license:

  (character) The type license applied to the dataset or record.

  - "CC0_1_0"

  - "CC_BY_4_0"

  - "CC_BY_NC_4_0"

- organismId:

  (numeric) An identifier for the Organism instance (as opposed to a
  particular digital record of the Organism). May be a globally unique
  identifier or an identifier specific to the data set.

- publishingOrg:

  (character) The publishing organization key (a UUID).

- stateProvince:

  (character) The name of the next smaller administrative region than
  country (state, province, canton, department, region, etc.) in which
  the Location occurs.

- waterBody:

  (character) The name of the water body in which the locations occur

- locality:

  (character) The specific description of the place.

- occurrenceStatus:

  (character) Default is "PRESENT". Specify whether search should return
  "PRESENT" or "ABSENT" data.

- gadmGid:

  (character) The gadm id of the area occurrences are desired from.
  https://gadm.org/.

- coordinateUncertaintyInMeters:

  A number or range between 0-1,000,000 which specifies the desired
  coordinate uncertainty. A coordinateUncertainty InMeters=1000 will be
  interpreted all records with exactly 1000m. Supports range queries,
  'smaller,larger' (e.g., '1000,10000', whereas '10000,1000' wouldn't
  work).

- verbatimScientificName:

  (character) Scientific name as provided by the source.

- eventId:

  (character) identifier(s) for a sampling event.

- identifiedBy:

  (character) names of people, groups, or organizations.

- networkKey:

  (character) The occurrence network key (a uuid) who assigned the Taxon
  to the subject.

- verbatimTaxonId:

  (character) The taxon identifier provided to GBIF by the data
  publisher.

- occurrenceId:

  (character) occurrence id from source.

- organismQuantity:

  A number or range which specifies the desired organism quantity. An
  organismQuantity=5 will be interpreted all records with exactly 5.
  Supports range queries, smaller,larger (e.g., '5,20', whereas '20,5'
  wouldn't work).

- organismQuantityType:

  (character) The type of quantification system used for the quantity of
  organisms. For example, "individuals" or "biomass".

- relativeOrganismQuantity:

  (numeric) A relativeOrganismQuantity=0.1 will be interpreted all
  records with exactly 0.1 The relative measurement of the quantity of
  the organism (a number between 0-1). Supports range queries,
  "smaller,larger" (e.g., '0.1,0.5', whereas '0.5,0.1' wouldn't work).

- iucnRedListCategory:

  (character) The IUCN threat status category.

  - "NE" (Not Evaluated)

  - "DD" (Data Deficient)

  - "LC" (Least Concern)

  - "NT" (Near Threatened)

  - "VU" (Vulnerable)

  - "EN" (Endangered)

  - "CR" (Critically Endangered)

  - "EX" (Extinct)

  - "EW" (Extinct in the Wild)

- lifeStage:

  (character) the life stage of the occurrence. One of many
  [options](https://www.gbif.org/occurrence/search?advanced=1&life_stage=Tadpole).

- isInCluster:

  (logical) identify potentially related records on GBIF.

- distanceFromCentroidInMeters:

  A number or range. A value of "2000,\*" means at least 2km from known
  centroids. A value of "0" would mean occurrences exactly on known
  centroids. A value of "0,2000" would mean within 2km of centroids. Max
  value is 5000.

- skip_validate:

  (logical) whether to skip wellknown::validate_wkt call or not. passed
  down to check_wkt(). Default: TRUE

- limit:

  Number of records to return. Default: 500. Note that the per request
  maximum is 300, but since we set it at 500 for the function, we do two
  requests to get you the 500 records (if there are that many). Note
  that there is a hard maximum of 100,000, which is calculated as the
  `limit+start`, so `start=99,000` and `limit=2000` won't work

- start:

  Record number to start at. Use in combination with limit to page
  through results. Note that we do the paging internally for you, but
  you can manually set the `start` parameter

- curlopts:

  (list)

## Value

An object of class `gbif_data`, which is a S3 class list, with slots for
metadata (`meta`) and the occurrence data itself (`data`), and with
attributes listing the user supplied arguments and whether it was a
"single" or "many" search; that is, if you supply two values of the
`datasetKey` parameter to searches are done, and it's a "many". `meta`
is a list of length four with offset, limit, endOfRecords and count
fields. `data` is a tibble (aka data.frame)

## Details

This function is a legacy alternative to
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md).
It is not recommended to use `occ_data()` as it is not as flexible as
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md).
New search terms will not be added to this function and it is only
supported for legacy reasons.
