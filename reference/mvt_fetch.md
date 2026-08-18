# Fetch Map Vector Tiles (MVT)

This function is a wrapper for the GBIF mapping api version 2.0. The
mapping API is a web map tile service making it straightforward to
visualize GBIF content on interactive maps, and overlay content from
other sources. It returns maps vector tiles with number of GBIF records
per area unit that can be used in a variety of ways, for example in
interactive leaflet web maps. Map details are specified by a number of
query parameters, some of them optional. Full documentation of the GBIF
mapping api can be found at https://www.gbif.org/developer/maps

## Usage

``` r
mvt_fetch(
  source = "density",
  x = 0,
  y = 0,
  z = 0,
  srs = "EPSG:4326",
  bin = NULL,
  hexPerTile = NULL,
  squareSize = NULL,
  style = "classic.point",
  taxonKey = NULL,
  checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b",
  datasetKey = NULL,
  country = NULL,
  publishingOrg = NULL,
  publishingCountry = NULL,
  year = NULL,
  basisOfRecord = NULL,
  ...
)
```

## Arguments

- source:

  (character) Either `density` for fast, precalculated tiles, or `adhoc`
  for any search. Default: `density`

- x:

  (integer) the column. Default: 0

- y:

  (integer) the row. Default: 0

- z:

  (integer) the zoom. Default: 0

- srs:

  (character) Spatial reference system for the output (input srs for mvt
  from GBIF is always `EPSG:3857`). One of:

  - `EPSG:3857` (Web Mercator)

  - `EPSG:4326` (WGS84 plate care?)

  - `EPSG:3575` (Arctic LAEA on 10 degrees E)

  - `EPSG:3031` (Antarctic stereographic)

- bin:

  (character) `square` or `hex` to aggregate occurrence counts into
  squares or hexagons. Points by default. optional

- hexPerTile:

  (integer) sets the size of the hexagons (the number horizontally
  across a tile). optional

- squareSize:

  (integer) sets the size of the squares. Choose a factor of 4096 so
  they tessalate correctly: probably from 8, 16, 32, 64, 128, 256, 512.
  optional

- style:

  (character) for raster tiles, choose from the available styles.
  Defaults to classic.point. optional. THESE DON'T WORK YET.

- taxonKey:

  (integer/numeric/character) search by taxon key, can only supply 1.
  optional

- checklistKey:

  (character) The key of a checklist to use for taxonomy. Defaults to
  COL (Catalogue of Life) Extended Release
  (`"7ddf754f-d193-4cc9-b351-99906754a03b"`). Set to `NULL` to use the
  GBIF Backbone Taxonomy. optional

- datasetKey:

  (character) search by taxon key, can only supply 1. optional

- country:

  (character) search by taxon key, can only supply 1. optional

- publishingOrg:

  (character) search by taxon key, can only supply 1. optional

- publishingCountry:

  (character) search by taxon key, can only supply 1. optional

- year:

  (integer) integer that limits the search to a certain year or, if
  passing a vector of integers, multiple years, for example `1984` or
  `c(2016, 2017, 2018)` or `2010:2015` (years 2010 to 2015). optional

- basisOfRecord:

  (character) one or more basis of record states to include records with
  that basis of record. The full list is:
  `c("OBSERVATION", "HUMAN_OBSERVATION", "MACHINE_OBSERVATION", "MATERIAL_SAMPLE", "PRESERVED_SPECIMEN", "FOSSIL_SPECIMEN", "LIVING_SPECIMEN", "LITERATURE", "UNKNOWN")`.
  optional

- ...:

  curl options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html)

## Value

an sf object

## Details

This function uses the arguments passed on to generate a query to the
GBIF web map API. The API returns a web tile object as png that is read
and converted into an R raster object. The break values or nbreaks
generate a custom colour palette for the web tile, with each bin
corresponding to one grey value. After retrieval, the raster is
reclassified to the actual break values. This is a somewhat hacky but
nonetheless functional solution in the absence of a GBIF raster API
implementation.

We add extent and set the projection for the output. You can reproject
after retrieving the output.

## References

https://www.gbif.org/developer/maps

## See also

[`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)

## Examples

``` r
if (FALSE) { # \dontrun{
if (
 requireNamespace("sf", quietly = TRUE) &&
 requireNamespace("protolite", quietly = TRUE)
) {
  # Using COL XR taxon key (default)
  x <- mvt_fetch(taxonKey = "V2", year = 2007:2011)
  x
  
  # gives an sf object
  class(x)
  
  # different srs
  ## 3857
  y <- mvt_fetch(taxonKey = "V2", year = 2010, srs = "EPSG:3857")
  y
  ## 3031
  z <- mvt_fetch(taxonKey = "V2", year = 2010, srs = "EPSG:3031", verbose = TRUE)
  z
  # 3575
  z <- mvt_fetch(taxonKey = "V2", year = 2010, srs = "EPSG:3575")
  z

  # bin
  x <- mvt_fetch(taxonKey = "V2", year = 1998, bin = "hex",
     hexPerTile = 30, style = "classic-noborder.poly")
  x

  # query with basisOfRecord
  mvt_fetch(taxonKey = "V2", year = 2010,
    basisOfRecord = "HUMAN_OBSERVATION")
  mvt_fetch(taxonKey = "V2", year = 2010,
    basisOfRecord = c("HUMAN_OBSERVATION", "LIVING_SPECIMEN"))
 }
} # }
```
