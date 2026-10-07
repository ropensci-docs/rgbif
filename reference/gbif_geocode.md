# Geocode lat-lon point(s) with GBIF's set of geo-polygons (experimental)

Geocode lat-lon point(s) with GBIF's set of geo-polygons (experimental)

## Usage

``` r
gbif_geocode(
  latitude = NULL,
  longitude = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- latitude:

  a vector of numeric latitude values between -90 and 90.

- longitude:

  a vector of numeric longitude values between -180 and 180.

- curlopts:

  A list of curl options to pass to the request.

## Value

A data.frame of results from the GBIF gecoding service.

- **latitude** : The input latitude

- **longitude** : The input longitude

- **index** : The original input rownumber

- **id** : The polygon id from which the geocode comes from

- **type** : One of the following : "Political" (county codes), "IHO"
  (marine regions), "SeaVox" (marine regions), "WGSRPD" (tdwg regions),
  "EEZ", (in national waters) or
  "GADM0","GADM1","GADM2","GADM2"(http://gadm.org/)

- **title** : The name of the source polygon

- **distance** : distance to the polygon boarder

This function uses the GBIF geocoder API which is not guaranteed to be
stable and is undocumented. As such, this may return different data over
time, may be rate-limited or may stop working if GBIF change the
service. Use this function with caution.

## References

http://gadm.org/ http://marineregions.org/
http://www.tdwg.org/standards/
<http://api.gbif.org/v1/geocode/reverse?lat=0&lng=0>

## Examples

``` r
if (FALSE) { # \dontrun{
# one pair 
gbif_geocode(0,0)
# or multiple pairs of points
gbif_geocode(c(0,50),c(0,20))

} # }
```
