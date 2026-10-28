# View photos from GBIF.

View photos from GBIF.

## Usage

``` r
gbif_photos(input, output = NULL, which = "table", browse = TRUE)
```

## Arguments

- input:

  Input output from occ_search

- output:

  Output folder path. If not given uses temporary folder.

- which:

  One of map or table (default).

- browse:

  (logical) Browse output (default: `TRUE`)

## Details

The max number of photos you can see when which="map" is ~160, so cycle
through if you have more than that.

## BEWARE

The maps in the table view may not show up correctly if you are using
RStudio

## Examples

``` r
if (FALSE) { # \dontrun{
res <- occ_search(mediaType = 'StillImage', limit = 100)
gbif_photos(res)
gbif_photos(res, which='map')

res <- occ_search(scientificName = "Aves", mediaType = 'StillImage',
  limit=150)
gbif_photos(res)
gbif_photos(res, output = '~/barfoo')
} # }
```
