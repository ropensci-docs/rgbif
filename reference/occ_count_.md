# Get quick pre-computed occurrence counts of a limited number of dimensions.

Get quick pre-computed occurrence counts of a limited number of
dimensions.

## Usage

``` r
occ_count_country(publishingCountry = NULL)

occ_count_pub_country(country = NULL)

occ_count_year(year = NULL)

occ_count_basis_of_record(curlopts = list(http_version = 2))
```

## Arguments

- publishingCountry:

  The 2-letter country code (as per ISO-3166-1) the country from which
  the occurrence was published.

- country:

  (character) The 2-letter country code (ISO-3166-1) in which the
  occurrence was recorded.

- year:

  The 4 digit year. Supports range queries, 'smaller,larger' (e.g.,
  '1990,1991', whereas 1991, 1990' wouldn't work).

- curlopts:

  (list) curl options.

## Value

A `data.frame` of counts.

## Details

Get quick pre-computed counts of a limited number of dimensions.

`occ_count_country()` will return a data.frame with occurrence counts by
country. By using `occ_count_country(publishingCountry="DK")` will
return the occurrence contributions Denmark has made to each country.

`occ_count_pub_country()` will return a data.frame with occurrence
counts by publishing country. Using
`occ_count_pub_country(country="DK")`, will return the occurrence
contributions each country has made to that focal `country=DK`.

`occ_count_year()` will return a data.frame with the total occurrences
mediated by GBIF for each year. By using
`occ_counts_year(year="1800,1900")` will only return counts for that
range.

`occ_count_basis_of_record()` will return a data.frame with total
occurrences mediated by GBIF for each basis of record.

## See also

[`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# total occurrence counts for all countries and iso2 places
occ_count_country()  
# the occurrences Mexico has published in other countries 
occ_count_country("MX") 
# the occurrences Denmark has published in other countries 
occ_count_country("DK")

# the occurrences other countries have published in Denmark
occ_count_pub_country("DK")
# the occurrences other countries have published in Mexico
occ_count_pub_country("MX")

# total occurrence counts for each year that an occurrence was 
# recorded or collected.
occ_count_year()
# supports ranges
occ_count_year("1800,1900")

# table of occurrence counts by basis of record
occ_count_basis_of_record()

} # }
```
