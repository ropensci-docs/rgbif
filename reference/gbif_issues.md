# List all GBIF issues and their codes.

Returns a data.frame of all GBIF issues with the following columns:

- `code`: issue short code, e.g. `gass84`

- `code`: issue full name, e.g. `GEODETIC_DATUM_ASSUMED_WGS84`

- `description`: issue description

- `type`: issue type, either related to `occurrence` or `name`

## Usage

``` r
gbif_issues()
```

## Source

https://gbif.github.io/gbif-api/apidocs/org/gbif/api/vocabulary/OccurrenceIssue.html
https://gbif.github.io/gbif-api/apidocs/org/gbif/api/vocabulary/NameUsageIssue.html
