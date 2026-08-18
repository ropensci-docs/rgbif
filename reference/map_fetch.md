# Fetch maps of GBIF occurrences

This function is a wrapper for the GBIF mapping api version 2.0. The
mapping API is a web map tile service making it straightforward to
visualize GBIF content on interactive maps, and overlay content from
other sources. It returns tile maps with number of GBIF records per area
unit that can be used in a variety of ways, for example in interactive
leaflet web maps. Map details are specified by a number of query
parameters, some of them optional. Full documentation of the GBIF
mapping api can be found at https://www.gbif.org/developer/maps

## Usage

``` r
map_fetch(
  source = "density",
  x = 0:1,
  y = 0,
  z = 0,
  format = "@1x.png",
  srs = "EPSG:4326",
  bin = NULL,
  hexPerTile = NULL,
  squareSize = NULL,
  style = NULL,
  taxonKey = NULL,
  checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b",
  datasetKey = NULL,
  country = NULL,
  publishingOrg = NULL,
  publishingCountry = NULL,
  year = NULL,
  basisOfRecord = NULL,
  return = "png",
  base_style = NULL,
  plot_terra = TRUE,
  curlopts = list(http_version = 2),
  ...
)
```

## Arguments

- source:

  (character) Either `density` for fast, precalculated tiles, or `adhoc`
  for any search. Default: `density`

- x:

  (integer sequence) the column. Default: 0:1

- y:

  (integer sequence) the row. Default: 0

- z:

  (integer) the zoom. Default: 0

- format:

  (character) The data format, one of:

  - `@Hx.png` for a 256px raster tile

  - `@1x.png` for a 512px raster tile (the default)

  - `@2x.png` for a 1024px raster tile

  - `@3x.png` for a 2048px raster tile

  - `@4x.png` for a 4096px raster tile

- srs:

  (character) Spatial reference system. One of:

  - `EPSG:3857` (Web Mercator)

  - `EPSG:4326` (WGS84 plate care?)

  - `EPSG:3575` (Arctic LAEA on 10 degrees E)

  - `EPSG:3031` (Antarctic stereographic)

- bin:

  (character) `square` or `hex` to aggregate occurrence counts into
  squares or hexagons. Points by default.

- hexPerTile:

  (integer) sets the size of the hexagons (the number horizontally
  across a tile).

- squareSize:

  (integer) sets the size of the squares. Choose a factor of 4096 so
  they tessalate correctly: probably from 8, 16, 32, 64, 128, 256, 512.

- style:

  (character) for raster tiles, choose from the available styles.
  Defaults to classic.point for source="density" and "scaled.circle" for
  source="adhoc".

- taxonKey:

  (integer/numeric/character) search by taxon key, can only supply 1.

- checklistKey:

  (character) The key of a checklist to use for taxonomy. Defaults to
  COL (Catalogue of Life) Extended Release
  (`"7ddf754f-d193-4cc9-b351-99906754a03b"`). Set to `NULL` to use the
  GBIF Backbone Taxonomy.

- datasetKey:

  (character) search by taxon key, can only supply 1.

- country:

  (character) search by taxon key, can only supply 1.

- publishingOrg:

  (character) search by taxon key, can only supply 1.

- publishingCountry:

  (character) search by taxon key, can only supply 1.

- year:

  (integer) integer that limits the search to a certain year or, if
  passing a vector of integers, multiple years, for example `1984` or
  `c(2016, 2017, 2018)` or `2010:2015` (years 2010 to 2015). optional

- basisOfRecord:

  (character) one or more basis of record states to include records with
  that basis of record. The full list is:
  `c("OBSERVATION", "HUMAN_OBSERVATION", "MACHINE_OBSERVATION", "MATERIAL_SAMPLE", "PRESERVED_SPECIMEN", "FOSSIL_SPECIMEN", "LIVING_SPECIMEN", "LITERATURE", "UNKNOWN")`.

- return:

  (character) Either "png" or "terra".

- base_style:

  (character) The style of the base map.

- plot_terra:

  (logical) Set whether the terra map be default plotted.

- curlopts:

  options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html)

- ...:

  additional arguments passed to the adhoc interface.

## Value

a `magick-image` or
[`terra::SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)` `
object.

## Details

The default settings, `return='png'`, will return a `magick-image` png.
This image will be a composite image of the the occurrence tiles fetched
and a base map. This map is primarily useful as a high quality image of
occurrence records.

The args `x` and `y` can both be integer sequences. For example, `x=0:3`
or `y=0:1`. Note that the tile index starts at 0. Higher values of `z`,
will will produce more tiles that can be fetched and stitched together.
Selecting a too high value for `x` or `y` will produce a blank image.

Setting `return='terra'` will return a
[`terra::SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)` `
object. This is primarily useful if you were interested in the
underlying aggregated occurrence density data.

See the article

## References

https://www.gbif.org/developer/maps

https://api.gbif.org/v2/map/demo.html

https://api.gbif.org/v2/map/demo13.html

## See also

[`mvt_fetch()`](https://docs.ropensci.org/rgbif/reference/mvt_fetch.md)

## Author

John Waller and Laurens Geffert <laurensgeffert@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{

# all occurrences
map_fetch()
# get artic map
map_fetch(srs='EPSG:3031') 
# only preserved specimens
map_fetch(basisOfRecord="PRESERVED_SPECIMEN")

# Map of occ in Great Britain
map_fetch(z=3,y=1,x=7:8,country="GB")
# Penguins with artic projection using COL XR key
map_fetch(srs='EPSG:3031',taxonKey="623RM",style='glacier.point', 
base_style="gbif-dark")

# occ from a long time ago
map_fetch(year=1600) 
# polygon style 
map_fetch(style="iNaturalist.poly",bin="hex")
# iNaturalist dataset plotted 
map_fetch(datasetKey="50c9509d-22c7-4a22-a47d-8c48425ef4a7",
  style="iNaturalist.poly")
 
# use source="adhoc" for more filters
map_fetch(z=1,
  source="adhoc",
  iucn_red_list_category="CR",
  style="scaled.circles",
  base_style='gbif-light')

# cropped map of Hawaii
map_fetch(z=5,x=3:4,y=12,source="adhoc",gadmGid="USA.12_1")


} # }
```
