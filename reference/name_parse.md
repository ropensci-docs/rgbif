# Parse taxon names using the GBIF name parser.

Parse taxon names using the GBIF name parser.

## Usage

``` r
name_parse(scientificname, curlopts = list(http_version = 2))
```

## Arguments

- scientificname:

  A character vector of scientific names.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A `data.frame` containing fields extracted from parsed taxon names.
Fields returned are the union of fields extracted from all species names
in `scientificname`.

## References

<https://www.gbif.org/developer/species#parser>

## Author

John Baumgartner (johnbb@student.unimelb.edu.au)

## Examples

``` r
if (FALSE) { # \dontrun{
name_parse(scientificname='x Agropogon littoralis')
name_parse(c('Arrhenatherum elatius var. elatius',
             'Secale cereale subsp. cereale', 'Secale cereale ssp. cereale',
             'Vanessa atalanta (Linnaeus, 1758)'))
name_parse("Ajuga pyramidata")
name_parse("Ajuga pyramidata x reptans")

# Pass on curl options
# res <- name_parse(c('Arrhenatherum elatius var. elatius',
#          'Secale cereale subsp. cereale', 'Secale cereale ssp. cereale',
#          'Vanessa atalanta (Linnaeus, 1758)'), curlopts=list(verbose=TRUE))
} # }
```
