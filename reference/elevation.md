# Get elevation for lat/long points from a data.frame or list of points.

Uses the GeoNames web service

## Usage

``` r
elevation(
  input = NULL,
  latitude = NULL,
  longitude = NULL,
  latlong = NULL,
  elevation_model = "srtm3",
  username = Sys.getenv("GEONAMES_USER"),
  key,
  curlopts = list(http_version = 2),
  ...
)
```

## Arguments

- input:

  A data.frame of lat/long data. There must be columns decimalLatitude
  and decimalLongitude.

- latitude:

  A vector of latitude's. Must be the same length as the longitude
  vector.

- longitude:

  A vector of longitude's. Must be the same length as the latitude
  vector.

- latlong:

  A vector of lat/long pairs. See examples.

- elevation_model:

  (character) one of srtm3 (default), srtm1, astergdem, or gtopo30. See
  "Elevation models" below for more

- username:

  (character) Required. An GeoNames user name. See Details.

- key, curlopts:

  defunct. see docs

- ...:

  curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)
  see
  [`curl::curl_options()`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A new column named `elevation_geonames` in the supplied data.frame or a
vector with elevation of each location in meters. Note that data from
GBIF can already have a column named `elevation`, thus the column we add
is named differently.

## Deprecation Notice

This function is deprecated as of rgbif 3.9.0 and will be removed in a
future version. It relies on a non-GBIF web service (GeoNames) and is
not core to the package's purpose of interacting with GBIF data.

## GeoNames user name

To get a GeoNames user name, register for an account at
http://www.geonames.org/login - then you can enable your account for the
GeoNames webservice on your account page
(http://www.geonames.org/manageaccount). Once you are enabled to use the
webservice, you can pass in your username to the `username` parameter.
Better yet, store your username in your `.Renviron` file, or similar
(e.g., .zshrc or .bash_profile files) and read it in via
[`Sys.getenv()`](https://rdrr.io/r/base/Sys.getenv.html) as in the
examples below. By default we do `Sys.getenv("GEONAMES_USER")` for the
`username` parameter.

## Elevation models

- srtm3:

  - sample area: ca 90m x 90m

  - result: a single number giving the elevation in meters according to
    srtm3, ocean areas have been masked as "no data" and have been
    assigned a value of -32768

- srtm1:

  - sample area: ca 30m x 30m

  - result: a single number giving the elevation in meters according to
    srtm1, ocean areas have been masked as "no data" and have been
    assigned a value of -32768

- astergdem (Aster Global Digital Elevation Model V2 2011):

  - sample area: ca 30m x 30m, between 83N and 65S latitude

  - result: a single number giving the elevation in meters according to
    aster gdem, ocean areas have been masked as "no data" and have been
    assigned a value of -32768

- gtopo30:

  - sample area: ca 1km x 1km

  - result: a single number giving the elevation in meters according to
    gtopo30, ocean areas have been masked as "no data" and have been
    assigned a value of -9999

## References

GeoNames http://www.geonames.org/export/web-services.html

## Examples

``` r
if (FALSE) { # \dontrun{
user <- Sys.getenv("GEONAMES_USER")

occ_key <- name_suggest('Puma concolor')$key[1]
dat <- occ_search(taxonKey = occ_key, limit = 300, hasCoordinate = TRUE)
head( elevation(dat$data, username = user) )

# Pass in a vector of lat's and a vector of long's
elevation(latitude = dat$data$decimalLatitude[1:10],
  longitude = dat$data$decimalLongitude[1:10],
  username = user, verbose = TRUE)

# Pass in lat/long pairs in a single vector
pairs <- list(c(31.8496,-110.576060), c(29.15503,-103.59828))
elevation(latlong=pairs, username = user)

# Pass on curl options
pairs <- list(c(31.8496,-110.576060), c(29.15503,-103.59828))
elevation(latlong=pairs, username = user, verbose = TRUE)

# different elevation models
lats <- dat$data$decimalLatitude[1:5]
lons <- dat$data$decimalLongitude[1:5]
elevation(latitude = lats, longitude = lons, elevation_model = "srtm3")
elevation(latitude = lats, longitude = lons, elevation_model = "srtm1")
elevation(latitude = lats, longitude = lons, elevation_model = "astergdem")
elevation(latitude = lats, longitude = lons, elevation_model = "gtopo30")
} # }
```
