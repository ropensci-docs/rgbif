# Download predicate DSL (domain specific language)

Download predicate DSL (domain specific language)

## Usage

``` r
pred(key, value, checklistKey = NULL)

pred_gt(key, value)

pred_gte(key, value)

pred_lt(key, value)

pred_lte(key, value)

pred_not(...)

pred_like(key, value)

pred_within(value)

pred_isnull(key)

pred_notnull(key)

pred_or(..., .list = list())

pred_and(..., .list = list())

pred_in(key, value, checklistKey = NULL)

pred_default()
```

## Arguments

- key:

  (character) the key for the predicate. See "Keys" below

- value:

  (various) the value for the predicate

- checklistKey:

  (character) A checklistKey to use for downloading using alternative
  taxonomies. Can be used with any taxonomic rank key (taxonKey,
  classKey, phylumKey, orderKey, familyKey, genusKey, subgenusKey,
  speciesKey, acceptedTaxonKey, kingdomKey). The default is COL
  (Catalogue of Life) Extended Release
  (`"7ddf754f-d193-4cc9-b351-99906754a03b"`). To use GBIF Backbone
  Taxonomy, pass `"d7dddbf4-2cf0-4f39-9b2a-bb099caae36c"`.

- ..., .list:

  For `pred_or()` or `pred_and()`, one or more objects of class
  `occ_predicate`, created by any `pred*` function

## predicate methods and their equivalent types

`pred*` functions are named for the 'type' of operation they do,
following the terminology used by GBIF, see
https://www.gbif.org/developer/occurrence#predicates

Function names are given, with the equivalent GBIF type value (e.g.,
`pred_gt` and `greaterThan`)

The following functions take one key and one value:

- `pred`: equals

- `pred_lt`: lessThan

- `pred_lte`: lessThanOrEquals

- `pred_gt`: greaterThan

- `pred_gte`: greaterThanOrEquals

- `pred_like`: like

The following function is only for geospatial queries, and only accepts
a WKT string:

- `pred_within`: within

The following function is only for stating the you don't want a key to
be null, so only accepts one key:

- `pred_notnull`: isNotNull

The following function is only for stating that you want a key to be
null.

- `pred_isnull` : isNull

The following two functions accept multiple individual predicates,
separating them by either "and" or "or":

- `pred_and`: and

- `pred_or`: or

The not predicate accepts one predicate; that is, this negates whatever
predicate is passed in, e.g., not the taxonKey of 12345:

- `pred_not`: not

The following function is special in that it accepts a single key but
many values; stating that you want to search for all the values:

- `pred_in`: in

The following function will apply commonly used **defaults**.

- `pred_default`

Using `pred_default()` is equivalent to running:

      pred_and(
       pred("HAS_GEOSPATIAL_ISSUE",FALSE),
       pred("HAS_COORDINATE",TRUE),
       pred("OCCURRENCE_STATUS","PRESENT"),
       pred_not(pred_in("BASIS_OF_RECORD",
        c("FOSSIL_SPECIMEN","LIVING_SPECIMEN")))
      )

## What happens internally

Internally, the input to `pred*` functions turns into JSON to be sent to
GBIF. For example ...

`pred_in("taxonKey", c("9WLSS", "Q2N2"))` gives:

    {
       "type": "in",
       "key": "TAXON_KEY",
       "values": ["9WLSS", "Q2N2"]
     }

`pred_gt("elevation", 5000)` gives:

    {
       "type": "greaterThan",
       "key": "ELEVATION",
       "value": "5000"
    }

`pred_or(pred("taxonKey", "Q2M4"), pred("taxonKey", "Q2KZ"))` gives:

    {
      "type": "or",
      "predicates": [
         {
           "type": "equals",
           "key": "TAXON_KEY",
           "value": "Q2M4"
         },
         {
           "type": "equals",
           "key": "TAXON_KEY",
           "value": "Q2KZ"
         }
      ]
    }

## Keys

Acceptable arguments to the `key` parameter are (with the version of the
key in parens that must be sent if you pass the query via the `body`
parameter; see below for examples). You can also use the 'ALL_CAPS'
version of a key if you prefer. Open an issue in the GitHub repository
for this package if you know of a key that should be supported that is
not yet.

- taxonKey (TAXON_KEY)

- acceptedTaxonKey (ACCEPTED_TAXON_KEY)

- kingdomKey (KINGDOM_KEY)

- phylumKey (PHYLUM_KEY)

- classKey (CLASS_KEY)

- orderKey (ORDER_KEY)

- familyKey (FAMILY_KEY)

- genusKey (GENUS_KEY)

- subgenusKey (SUBGENUS_KEY)

- speciesKey (SPECIES_KEY)

- scientificName (SCIENTIFIC_NAME)

- country (COUNTRY)

- publishingCountry (PUBLISHING_COUNTRY)

- hasCoordinate (HAS_COORDINATE)

- hasGeospatialIssue (HAS_GEOSPATIAL_ISSUE)

- typeStatus (TYPE_STATUS)

- recordNumber (RECORD_NUMBER)

- lastInterpreted (LAST_INTERPRETED)

- modified (MODIFIED)

- continent (CONTINENT)

- geometry (GEOMETRY)

- basisOfRecord (BASIS_OF_RECORD)

- datasetKey (DATASET_KEY)

- datasetID/datasetId (DATASET_ID)

- eventDate (EVENT_DATE)

- catalogNumber (CATALOG_NUMBER)

- otherCatalogNumbers (OTHER_CATALOG_NUMBERS)

- year (YEAR)

- month (MONTH)

- decimalLatitude (DECIMAL_LATITUDE)

- decimalLongitude (DECIMAL_LONGITUDE)

- elevation (ELEVATION)

- depth (DEPTH)

- institutionCode (INSTITUTION_CODE)

- collectionCode (COLLECTION_CODE)

- issue (ISSUE)

- mediatype (MEDIA_TYPE)

- recordedBy (RECORDED_BY)

- recordedById/recordedByID (RECORDED_BY_ID)

- establishmentMeans (ESTABLISHMENT_MEANS)

- coordinateUncertaintyInMeters (COORDINATE_UNCERTAINTY_IN_METERS)

- gadm (GADM_GID) (for the Database of Global Administrative Areas)

- level0Gid (GADM_LEVEL_0_GID)

- level1Gid (GADM_LEVEL_1_GID)

- level2Gid (GADM_LEVEL_2_GID)

- level3Gid (GADM_LEVEL_3_GID)

- stateProvince (STATE_PROVINCE)

- occurrenceStatus (OCCURRENCE_STATUS)

- publishingOrg (PUBLISHING_ORG)

- occurrenceId/occurrenceID (OCCURRENCE_ID)

- eventId/eventID (EVENT_ID)

- parentEventId/parentEventID (PARENT_EVENT_ID)

- identifiedBy (IDENTIFIED_BY)

- identifiedById/identifiedByID (IDENTIFIED_BY_ID)

- license (LICENSE) - Note: Use underscores, not spaces (e.g.,
  "CC_BY_4_0" not "CC BY 4.0")

- locality(LOCALITY)

- pathway (PATHWAY)

- preparations (PREPARATIONS)

- networkKey (NETWORK_KEY)

- organismId/organismID (ORGANISM_ID)

- organismQuantity (ORGANISM_QUANTITY)

- organismQuantityType (ORGANISM_QUANTITY_TYPE)

- protocol (PROTOCOL)

- relativeOrganismQuantity (RELATIVE_ORGANISM_QUANTITY)

- repatriated (REPATRIATED)

- sampleSizeUnit (SAMPLE_SIZE_UNIT)

- sampleSizeValue (SAMPLE_SIZE_VALUE)

- samplingProtocol (SAMPLING_PROTOCOL)

- verbatimScientificName (VERBATIM_SCIENTIFIC_NAME)

- taxonID/taxonId (TAXON_ID)

- taxonomicStatus (TAXONOMIC_STATUS)

- waterBody (WATER_BODY)

- iucnRedListCategory (IUCN_RED_LIST_CATEGORY)

- degreeOfEstablishment (DEGREE_OF_ESTABLISHMENT)

- isInCluster (IS_IN_CLUSTER)

- lifeStage (LIFE_STAGE)

- distanceFromCentroidInMeters (DISTANCE_FROM_CENTROID_IN_METERS)

- gbifId (GBIF_ID)

- institutionKey (INSTITUTION_KEY)

## References

Download predicates docs:
<https://www.gbif.org/developer/occurrence#predicates>

## See also

Other downloads:
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
[`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md),
[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md),
[`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md),
[`occ_download_list()`](https://docs.ropensci.org/rgbif/reference/occ_download_list.md),
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md),
[`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md),
[`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md),
[`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md),
[`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md),
[`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md),
[`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md),
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md),
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

## Examples

``` r
# Uses COL (Catalogue of Life) Extended Release alpha-numeric keys by default
pred("taxonKey", "Q2M4") # Calopteryx splendens
#> <<gbif download - predicate>>
#>   > type: equals, key: TAXON_KEY, value: Q2M4, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred_gt("elevation", 5000)
#> <<gbif download - predicate>>
#>   > type: greaterThan, key: ELEVATION, value: 5000
pred_gte("elevation", 5000)
#> <<gbif download - predicate>>
#>   > type: greaterThanOrEquals, key: ELEVATION, value: 5000
pred_lt("elevation", 1000)
#> <<gbif download - predicate>>
#>   > type: lessThan, key: ELEVATION, value: 1000
pred_lte("elevation", 1000)
#> <<gbif download - predicate>>
#>   > type: lessThanOrEquals, key: ELEVATION, value: 1000
pred_within("POLYGON((-14 42, 9 38, -7 26, -14 42))")
#> <<gbif download - predicate>>
#>   > type: within, key: geometry, value: POLYGON((-14 42, 9 38, -7 26, -14 42))
pred_and(pred_within("POLYGON((-14 42, 9 38, -7 26, -14 42))"),
  pred_gte("elevation", 5000))
#> <<gbif download - predicate list>>
#>   type: and
#>   > type: within, key: geometry, value: POLYGON((-14 42, 9 38, -7 26, -14 42))
#>   > type: greaterThanOrEquals, key: ELEVATION, value: 5000
pred_or(pred_lte("year", 1989), pred("year", 2000))
#> <<gbif download - predicate list>>
#>   type: or
#>   > type: lessThanOrEquals, key: YEAR, value: 1989
#>   > type: equals, key: YEAR, value: 2000
pred_and(pred_lte("year", 1989), pred("year", 2000))
#> <<gbif download - predicate list>>
#>   type: and
#>   > type: lessThanOrEquals, key: YEAR, value: 1989
#>   > type: equals, key: YEAR, value: 2000
pred_in("taxonKey", c("Q2M4", "9WLSS", "Q2N2")) # COL XR alpha-numeric keys
#> <<gbif download - predicate>>
#>   > type: in, key: TAXON_KEY, value: Q2M4,9WLSS,Q2N2, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred_in("basisOfRecord", c("MACHINE_OBSERVATION", "HUMAN_OBSERVATION"))
#> <<gbif download - predicate>>
#>   > type: in, key: BASIS_OF_RECORD, value: MACHINE_OBSERVATION,HUMAN_OBSERVATION
pred_not(pred("taxonKey", "Q2M4"))
#> <<gbif download - predicate list>>
#>   type: not
#>   > type: equals, key: TAXON_KEY, value: Q2M4, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred_like("catalogNumber", "PAPS5-560%")
#> <<gbif download - predicate>>
#>   > type: like, key: CATALOG_NUMBER, value: PAPS5-560%
pred_notnull("issue")
#> <<gbif download - predicate>>
#>   > type: isNotNull, parameter: ISSUE
pred("basisOfRecord", "LITERATURE")
#> <<gbif download - predicate>>
#>   > type: equals, key: BASIS_OF_RECORD, value: LITERATURE
pred("hasCoordinate", TRUE)
#> <<gbif download - predicate>>
#>   > type: equals, key: HAS_COORDINATE, value: true
pred("stateProvince", "California")
#> <<gbif download - predicate>>
#>   > type: equals, key: STATE_PROVINCE, value: California
pred("hasGeospatialIssue", FALSE)
#> <<gbif download - predicate>>
#>   > type: equals, key: HAS_GEOSPATIAL_ISSUE, value: false
pred_within("POLYGON((-14 42, 9 38, -7 26, -14 42))")
#> <<gbif download - predicate>>
#>   > type: within, key: geometry, value: POLYGON((-14 42, 9 38, -7 26, -14 42))
pred_or(pred("taxonKey", "Q2M4"), pred("taxonKey", "9WLSS"),
  pred("taxonKey", "Q2N2"))
#> <<gbif download - predicate list>>
#>   type: or
#>   > type: equals, key: TAXON_KEY, value: Q2M4, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
#>   > type: equals, key: TAXON_KEY, value: 9WLSS, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
#>   > type: equals, key: TAXON_KEY, value: Q2N2, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred_in("taxonKey", c("Q2M4", "9WLSS", "Q2N2", "Q2KZ"))
#> <<gbif download - predicate>>
#>   > type: in, key: TAXON_KEY, value: Q2M4,9WLSS,Q2N2,Q2KZ, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred("license", "CC_BY_4_0")
#> <<gbif download - predicate>>
#>   > type: equals, key: LICENSE, value: CC_BY_4_0
pred_in("license", c("CC_BY_4_0", "CC_BY_NC_4_0"))
#> <<gbif download - predicate>>
#>   > type: in, key: LICENSE, value: CC_BY_4_0,CC_BY_NC_4_0

# Using checklistKey with different taxonomic rank keys
pred("classKey", "B8V3Z")  # Uses COL XR by default
#> <<gbif download - predicate>>
#>   > type: equals, key: CLASS_KEY, value: B8V3Z, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
pred("orderKey", "C4PL")   # Uses COL XR by default
#> <<gbif download - predicate>>
#>   > type: equals, key: ORDER_KEY, value: C4PL, checklistKey: 7ddf754f-d193-4cc9-b351-99906754a03b
# Override to use GBIF Backbone
pred("classKey", "220", checklistKey = "d7dddbf4-2cf0-4f39-9b2a-bb099caae36c")
#> <<gbif download - predicate>>
#>   > type: equals, key: CLASS_KEY, value: 220, checklistKey: d7dddbf4-2cf0-4f39-9b2a-bb099caae36c
```
