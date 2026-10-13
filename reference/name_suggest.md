# Suggest up to 20 name usages.

Suggest up to 20 name usages.

## Usage

``` r
name_suggest(
  q = NULL,
  datasetKey = NULL,
  rank = NULL,
  fields = NULL,
  start = NULL,
  limit = 100,
  curlopts = list(http_version = 2)
)
```

## Arguments

- q:

  (character, required) Simple search parameter. The value for this
  parameter can be a simple word or a phrase. Wildcards can be added to
  the simple word parameters only, e.g. q=*puma*

- datasetKey:

  (character) Filters by the checklist dataset key (a uuid, see
  examples)

- rank:

  (character) A taxonomic rank. One of class, cultivar, cultivar_group,
  domain, family, form, genus, informal, infrageneric_name, infraorder,
  infraspecific_name, infrasubspecific_name, kingdom, order, phylum,
  section, series, species, strain, subclass, subfamily, subform,
  subgenus, subkingdom, suborder, subphylum, subsection, subseries,
  subspecies, subtribe, subvariety, superclass, superfamily, superorder,
  superphylum, suprageneric_name, tribe, unranked, or variety.

- fields:

  (character) Fields to return in output data.frame (simply prunes
  columns off)

- start:

  Record number to start at. Default: 0. Use in combination with `limit`
  to page through results.

- limit:

  Number of records to return. Default: 100. Maximum: 1000.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

A list, with two elements `data` (tibble) and `hierarchy` (list of
data.frame's). If 'higherClassificationMap' is one of the `fields`
requested, then `hierarchy` is a list of data.frame's; if not included,
`hierarchy` is an empty list.

## Deprecation Notice

**This function is deprecated.** It only works with the GBIF Backbone
Taxonomy and does not support COL (Catalogue of Life) Extended Release.
Use `rcol::col_suggest()` from the rcol package instead for COL XR
support.

A quick and simple autocomplete service that returns up to 20 name
usages by doing prefix matching against the scientific name. Results are
ordered by relevance.

## Repeat parmeter inputs

Some parameters can take many inputs, and treated as 'OR' (e.g., a or b
or c). The following take many inputs:

- **rank**

- **datasetKey**

## References

<https://www.gbif.org/developer/species#searching>

## Examples

``` r
if (FALSE) { # \dontrun{
name_suggest(q='Puma concolor')
name_suggest(q='Puma')
name_suggest(q='Puma', rank="genus")
name_suggest(q='Puma', rank="subspecies")
name_suggest(q='Puma', rank="species")
name_suggest(q='Puma', rank="infraspecific_name")

name_suggest(q='Puma', limit=2)
name_suggest(q='Puma', fields=c('key','canonicalName'))
name_suggest(q='Puma', fields=c('key','canonicalName',
  'higherClassificationMap'))

# Some parameters accept many inputs, treated as OR
name_suggest(rank = c("family", "genus"))
name_suggest(datasetKey = c("73605f3a-af85-4ade-bbc5-522bfb90d847",
  "d7c60346-44b6-400d-ba27-8d3fbeffc8a5"))

# If 'higherClassificationMap' in fields, a list is returned
name_suggest(q='Puma', fields=c('key','higherClassificationMap'))

# Pass on curl options
name_suggest(q='Puma', limit=200, curlopts = list(verbose=TRUE))
} # }
```
