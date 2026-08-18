# Get number of occurrence records.

Get number of occurrence records.

## Usage

``` r
occ_count(..., occurrenceStatus = "PRESENT", curlopts = list(http_version = 2))
```

## Arguments

- ...:

  parameters passed to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md).

- occurrenceStatus:

  (character) Default is "PRESENT". Specify whether search should return
  "PRESENT" or "ABSENT" data.

- curlopts:

  (list) curl options.

## Value

The occurrence count of the
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
query.

## Details

`occ_count()` is a short convenience wrapper for
`occ_search(limit=0)$meta$count`.

The current version (since rgbif 3.7.6) of `occ_count()` uses a
different GBIF API endpoint from previous versions. This change greatly
improves the usability of `occ_count()`. Legacy parameters
`georeferenced`, `type`, `date`, `to`, `from` are no longer supported
and not guaranteed to work correctly.

Multiple values of the type `c("a","b")` will give an error, but `"a;b"`
will work.

## See also

[`occ_count_year()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
[`occ_count_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
[`occ_count_pub_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
[`occ_count_basis_of_record()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# total occurrences mediated by GBIF
occ_count() # should be > 2 billion! 

# number of plant occurrences
occ_count(kingdomKey=name_backbone("Plantea")$usageKey) 
occ_count(scientificName = 'Ursus americanus')

occ_count(country="DK") # found in Denmark 
occ_count(country="DK;US") # found in Denmark and United States
occ_count(publishingCountry="US") # published by the United States
# number of repatriated eBird records in India
occ_count(repatriated = TRUE,country="IN") 
 
# Use COL XR alpha-numeric taxonKey
occ_count(taxonKey="Q2M4") # Calopteryx splendens occurrences
# or use numeric keys with GBIF Backbone  
occ_count(taxonKey=212, 
  checklistKey = "d7dddbf4-2cf0-4f39-9b2a-bb099caae36c") # bird occurrences
# between years 1800-1900
occ_count(basisOfRecord="PRESERVED_SPECIMEN", year="1800,1900") 
occ_count(recordedBy="John Waller") # recorded by John Waller
occ_count(decimalLatitude=0, decimalLongitude=0) # exactly on 0,0

# close to a known iso2 centroid
occ_count(distanceFromCentroidInMeters="0,2000") 
# close to a known iso2 centroid in Sweden
occ_count(distanceFromCentroidInMeters="0,2000",country="SE") 

occ_count(hasCoordinate=TRUE) # with coordinates
occ_count(protocol = "DIGIR") # published using DIGIR format
occ_count(mediaType = 'StillImage') # with images

# number of occurrences iucn status "critically endangered"
occ_count(iucnRedListCategory="CR") 
occ_count(verbatimScientificName="Calopteryx splendens;Calopteryx virgo")
occ_count(
geometry="POLYGON((24.70938 48.9221,24.71056 48.92175,24.71107
 48.92296,24.71002 48.92318,24.70938 48.9221))")

# getting a table of counts using the facets interface
# occurrence counts by year
occ_count(facet="year")
occ_count(facet="year",facetLimit=400)

# top scientificNames from Japan
occ_count(facet="scientificName",country="JP")
# top countries publishing specimen bird records between 1850 and 1880
occ_count(facet="scientificName",taxonKey=212,basisOfRecord="PRESERVED_SPECIMEN"
,year="1850,1880")

# Number of present or absence records of Elephants
occ_count(facet="occurrenceStatus",scientificName="Elephantidae")

# top 100 datasets publshing occurrences to GBIF
occ_count(facet="datasetKey",facetLimit=100)
# top datasets publishing country centroids on GBIF
occ_count(facet="datasetKey",distanceFromCentroidInMeters="0")

# common values for coordinateUncertaintyInMeters for museum specimens
occ_count(facet="coordinateUncertaintyInMeters",basisOfRecord="PRESERVED_SPECIMEN")

# number of iucn listed bird and insect occurrences in Mexico
occ_count(facet="iucnRedListCategory",taxonKey="212;216",country="MX")

# most common latitude values mediated by GBIF
occ_count(facet="decimalLatitude")

# top iNaturalist users publishing research-grade obs to GBIF
occ_count(facet="recordedBy",datasetKey="50c9509d-22c7-4a22-a47d-8c48425ef4a7")
# top 100 iNaturalist users from Ukraine
occ_count(facet="recordedBy",datasetKey="50c9509d-22c7-4a22-a47d-8c48425ef4a7"
,country="UA",facetLimit=100)

# top institutions publishing specimen occurrences to GBIF
occ_count(facet="institutionCode",basisOfRecord="PRESERVED_SPECIMEN")

} # }
```
