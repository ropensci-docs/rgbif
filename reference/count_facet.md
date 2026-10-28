# Facetted count occurrence search.

Facetted count occurrence search.

## Usage

``` r
count_facet(keys = NULL, by = "country", countries = 10, removezeros = FALSE)
```

## Arguments

- keys:

  (numeric) GBIF keys, a vector. optional

- by:

  (character) One of georeferenced, basisOfRecord, country, or
  publishingCountry. default: country

- countries:

  (numeric) Number of countries to facet on, or a vector of country
  names. default: 10

- removezeros:

  (logical) remove zeros or not? default: `FALSE`

## Examples

``` r
if (FALSE) { # \dontrun{
# Select number of countries to facet on
count_facet(by='country', countries=3, removezeros = TRUE)
# Or, pass in country names
count_facet(by='country', countries='AR', removezeros = TRUE)

spplist <- c('Geothlypis trichas','Tiaris olivacea','Pterodroma axillaris',
             'Calidris ferruginea','Pterodroma macroptera',
             'Gallirallus australis',
             'Falco cenchroides','Telespiza cantans','Oreomystis bairdi',
             'Cistothorus palustris')
keys <- sapply(spplist,
  function(x) name_backbone(x, rank="species")$usageKey)
count_facet(keys, by='country', countries=3, removezeros = TRUE)
count_facet(keys, by='country', countries=3, removezeros = FALSE)
count_facet(by='country', countries=20, removezeros = TRUE)
count_facet(keys, by='basisOfRecord', countries=5, removezeros = TRUE)

# get occurrences by georeferenced state
## across all records
count_facet(by='georeferenced')

## by keys
count_facet(keys, by='georeferenced')

# by basisOfRecord
count_facet(by="basisOfRecord")
} # }
```
