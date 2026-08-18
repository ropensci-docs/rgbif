# Convert a bounding box to a Well Known Text polygon, and a WKT to a bounding box

Convert a bounding box to a Well Known Text polygon, and a WKT to a
bounding box

## Usage

``` r
gbif_bbox2wkt(minx = NA, miny = NA, maxx = NA, maxy = NA, bbox = NULL)

gbif_wkt2bbox(wkt = NULL)
```

## Arguments

- minx:

  (numeric) Minimum x value, or the most western longitude

- miny:

  (numeric) Minimum y value, or the most southern latitude

- maxx:

  (numeric) Maximum x value, or the most eastern longitude

- maxy:

  (numeric) Maximum y value, or the most northern latitude

- bbox:

  (numeric) A vector of length 4, with the elements: minx, miny, maxx,
  maxy

- wkt:

  (character) A Well Known Text object.

## Value

gbif_bbox2wkt returns an object of class charactere, a Well Known Text
string of the form 'POLYGON((minx miny, maxx miny, maxx maxy, minx maxy,
minx miny))'.

gbif_wkt2bbox returns a numeric vector of length 4, like c(minx, miny,
maxx, maxy)

## Examples

``` r
if (FALSE) { # \dontrun{
# Convert a bounding box to a WKT
## Pass in a vector of length 4 with all values
gbif_bbox2wkt(bbox=c(-125.0,38.4,-121.8,40.9))

## Or pass in each value separately
gbif_bbox2wkt(minx=-125.0, miny=38.4, maxx=-121.8, maxy=40.9)

# Convert a WKT object to a bounding box
wkt <- "POLYGON((-125 38.4,-125 40.9,-121.8 40.9,-121.8 38.4,-125 38.4))"
gbif_wkt2bbox(wkt)
} # }
```
