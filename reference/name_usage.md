# Lookup details for specific names in all taxonomies in GBIF.

Lookup details for specific names in all taxonomies in GBIF.

## Usage

``` r
name_usage(
  key = NULL,
  name = NULL,
  data = "all",
  language = NULL,
  datasetKey = NULL,
  uuid = NULL,
  rank = NULL,
  shortname = NULL,
  start = 0,
  limit = 100,
  return = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- key:

  (numeric or character) A GBIF key for a taxon

- name:

  (character) Filters by a case insensitive, canonical namestring, e.g.
  'Puma concolor'

- data:

  (character) Specify an option to select what data is returned. See
  Description below.

- language:

  (character) Language, default is english

- datasetKey:

  (character) Filters by the dataset's key (a uuid). Must be length=1

- uuid:

  (character) A dataset key

- rank:

  (character) Taxonomic rank. Filters by taxonomic rank as one of:
  CLASS, CULTIVAR, CULTIVAR_GROUP, DOMAIN, FAMILY, FORM, GENUS,
  INFORMAL, INFRAGENERIC_NAME, INFRAORDER, INFRASPECIFIC_NAME,
  INFRASUBSPECIFIC_NAME, KINGDOM, ORDER, PHYLUM, SECTION, SERIES,
  SPECIES, STRAIN, SUBCLASS, SUBFAMILY, SUBFORM, SUBGENUS, SUBKINGDOM,
  SUBORDER, SUBPHYLUM, SUBSECTION, SUBSERIES, SUBSPECIES, SUBTRIBE,
  SUBVARIETY, SUPERCLASS, SUPERFAMILY, SUPERORDER, SUPERPHYLUM,
  SUPRAGENERIC_NAME, TRIBE, UNRANKED, VARIETY

- shortname:

  (character) A short name for a dataset - it may not do anything

- start:

  Record number to start at. Default: 0.

- limit:

  Number of records to return. Default: 100.

- return:

  Defunct. All components are returned; index to the one(s) you want

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

An object of class gbif, which is a S3 class list, with slots for
metadata (`meta`) and the data itself (`data`). In addition, the object
has attributes listing the user supplied arguments and type of search,
which is, differently from occurrence data, always equals to 'single'
even if multiple values for some parameters are given. `meta` is a list
of length four with offset, limit, endOfRecords and count fields. `data`
is a tibble (aka data.frame) containing all information about the found
taxa.

## Details

This service uses fuzzy lookup so that you can put in partial names and
you should get back those things that match. See examples below.

This function is different from
[`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
in that that function searches for names. This function encompasses a
bunch of API endpoints, most of which require that you already have a
taxon key, but there is one endpoint that allows name searches (see
examples below).

**Important:** When `key` is provided, the `datasetKey` parameter is
ignored by the GBIF API. The API returns data based solely on the key,
regardless of what `datasetKey` is set to. A warning will be issued if
both parameters are provided.

Note that `data="verbatim"` hasn't been working.

Options for the data parameter are: 'all', 'verbatim', 'name',
'parents', 'children', 'related', 'synonyms',
'descriptions','distributions', 'media', 'references',
'speciesProfiles', 'vernacularNames', 'typeSpecimens', 'root',
'iucnRedListCategory'

This function used to be vectorized with respect to the `data`
parameter, where you could pass in multiple values and the function
internally loops over each option making separate requests. This has
been removed. You can still loop over many options for the `data`
parameter, just use an `lapply` family function, or a for loop, etc.

See
[`name_issues()`](https://docs.ropensci.org/rgbif/reference/name_issues.md)
for more information about issues in `issues` column.

## Deprecation Notice

**This function is deprecated.** It only works with the GBIF Backbone
Taxonomy and does not support COL (Catalogue of Life) Extended Release.
Use `rcol::col_usage()` from the rcol package instead for COL XR
support.

## Repeat parameter inputs

These parameters used to accept many inputs, but no longer do:

- **rank**

- **name**

- **langugae**

- **datasetKey**

## References

<https://www.gbif.org/developer/species#nameUsages>

## Examples

``` r
if (FALSE) { # \dontrun{
# A single name usage
name_usage(key=1)

# Name usage for a taxonomic name
name_usage(name='Puma', rank="GENUS")

# Name usage for all taxa in a dataset
# (set sufficient high limit, but less than 100000)
# name_usage(datasetKey = "9ff7d317-609b-4c08-bd86-3bc404b77c42", 
#  limit = 10000)
# All name usages
name_usage()

# References for a name usage
name_usage(key=2435099, data='references')

# Species profiles, descriptions
name_usage(key=5231190, data='speciesProfiles')
name_usage(key=5231190, data='descriptions')
name_usage(key=2435099, data='children')

# Vernacular names for a name usage
name_usage(key=5231190, data='vernacularNames')

# Limit number of results returned
name_usage(key=5231190, data='vernacularNames', limit=3)

# Search for names by dataset with datasetKey parameter
name_usage(datasetKey="d7dddbf4-2cf0-4f39-9b2a-bb099caae36c")

# Search for a particular language
name_usage(key=5231190, language="FRENCH", data='vernacularNames')

# get root usage with a uuid
name_usage(data = "root", uuid = "73605f3a-af85-4ade-bbc5-522bfb90d847")

# search by language
name_usage(language = "spanish")

# Pass on curl options
name_usage(name='Puma concolor', limit=300, curlopts = list(verbose=TRUE))

# look up iucn red list category 
name_usage(key = 7707728, data = 'iucnRedListCategory') 
} # }
```
