# View highlighted terms in name results from GBIF.

View highlighted terms in name results from GBIF.

## Usage

``` r
gbif_names(input, output = NULL, browse = TRUE)
```

## Arguments

- input:

  Input output from occ_search

- output:

  Output folder path. If not given uses temporary folder.

- browse:

  (logical) Browse output (default: `TRUE`)

## Examples

``` r
if (FALSE) { # \dontrun{
# browse=FALSE returns path to file
gbif_names(name_lookup(query='snake', hl=TRUE), browse=FALSE)

(out <- name_lookup(query='canada', hl=TRUE, limit=5))
gbif_names(out)
gbif_names(name_lookup(query='snake', hl=TRUE))
gbif_names(name_lookup(query='bird', hl=TRUE))

# or not highlight
gbif_names(name_lookup(query='bird', limit=200))
} # }
```
