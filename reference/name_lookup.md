# Lookup names in all taxonomies in GBIF.

This service uses fuzzy lookup so that you can put in partial names and
you should get back those things that match. See examples below.

Faceting: If `facet=FALSE` or left to the default (NULL), no faceting is
done. And therefore, all parameters with facet in their name are ignored
(facetOnly, facetMincount, facetMultiselect).

## Usage

``` r
name_lookup(
  query = NULL,
  rank = NULL,
  higherTaxonKey = NULL,
  status = NULL,
  isExtinct = NULL,
  habitat = NULL,
  nameType = NULL,
  datasetKey = NULL,
  origin = NULL,
  nomenclaturalStatus = NULL,
  limit = 100,
  start = 0,
  facet = NULL,
  facetMincount = NULL,
  facetMultiselect = NULL,
  type = NULL,
  hl = NULL,
  issue = NULL,
  constituentKey = NULL,
  verbose = FALSE,
  return = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- query:

  Query term(s) for full text search.

- rank:

  CLASS, CULTIVAR, CULTIVAR_GROUP, DOMAIN, FAMILY, FORM, GENUS,
  INFORMAL, INFRAGENERIC_NAME, INFRAORDER, INFRASPECIFIC_NAME,
  INFRASUBSPECIFIC_NAME, KINGDOM, ORDER, PHYLUM, SECTION, SERIES,
  SPECIES, STRAIN, SUBCLASS, SUBFAMILY, SUBFORM, SUBGENUS, SUBKINGDOM,
  SUBORDER, SUBPHYLUM, SUBSECTION, SUBSERIES, SUBSPECIES, SUBTRIBE,
  SUBVARIETY, SUPERCLASS, SUPERFAMILY, SUPERORDER, SUPERPHYLUM,
  SUPRAGENERIC_NAME, TRIBE, UNRANKED, VARIETY

- higherTaxonKey:

  Filters by any of the higher Linnean rank keys. Note this is within
  the respective checklist and not searching nub keys across all
  checklists. This parameter accepts many inputs in a vector ( passed in
  the same request).

- status:

  Filters by the taxonomic status as one of:

  - ACCEPTED

  - DETERMINATION_SYNONYM Used for unknown child taxa referred to via
    spec, ssp, ...

  - DOUBTFUL Treated as accepted, but doubtful whether this is correct.

  - HETEROTYPIC_SYNONYM More specific subclass of SYNONYM.

  - HOMOTYPIC_SYNONYM More specific subclass of SYNONYM.

  - INTERMEDIATE_RANK_SYNONYM Used in nub only.

  - MISAPPLIED More specific subclass of SYNONYM.

  - PROPARTE_SYNONYM More specific subclass of SYNONYM.

  - SYNONYM A general synonym, the exact type is unknown.

- isExtinct:

  (logical) Filters by extinction status (e.g. `isExtinct=TRUE`)

- habitat:

  (character) Filters by habitat. One of: marine, freshwater, or
  terrestrial

- nameType:

  Filters by the name type as one of:

  - BLACKLISTED surely not a scientific name.

  - CANDIDATUS Candidatus is a component of the taxonomic name for a
    bacterium that cannot be maintained in a Bacteriology Culture
    Collection.

  - CULTIVAR a cultivated plant name.

  - DOUBTFUL doubtful whether this is a scientific name at all.

  - HYBRID a hybrid formula (not a hybrid name).

  - INFORMAL a scientific name with some informal addition like "cf." or
    indetermined like Abies spec.

  - SCINAME a scientific name which is not well formed.

  - VIRUS a virus name.

  - WELLFORMED a well formed scientific name according to present
    nomenclatural rules.

- datasetKey:

  Filters by the dataset's key (a uuid)

- origin:

  (character) Filters by origin. One of:

  - SOURCE

  - DENORMED_CLASSIFICATION

  - VERBATIM_ACCEPTED

  - EX_AUTHOR_SYNONYM

  - AUTONYM

  - BASIONYM_PLACEHOLDER

  - MISSING_ACCEPTED

  - IMPLICIT_NAME

  - PROPARTE

  - VERBATIM_BASIONYM

- nomenclaturalStatus:

  Not yet implemented, but will eventually allow for filtering by a
  nomenclatural status enum.

- limit:

  Number of records to return. Hard maximum limit set by GBIF API:
  99999.

- start:

  Record number to start at. Default: 0.

- facet:

  A vector/list of facet names used to retrieve the 100 most frequent
  values for a field. Allowed facets are: datasetKey, higherTaxonKey,
  rank, status, isExtinct, habitat, and nameType. Additionally threat
  and nomenclaturalStatus are legal values but not yet implemented, so
  data will not yet be returned for them.

- facetMincount:

  Used in combination with the facet parameter. Set facetMincount to
  exclude facets with a count less than x, e.g. http://bit.ly/2osAUQB
  only shows the type values 'CHECKLIST' and 'OCCURRENCE' because the
  other types have counts less than 10000

- facetMultiselect:

  (logical) Used in combination with the facet parameter. Set
  `facetMultiselect=TRUE` to still return counts for values that are not
  currently filtered, e.g. http://bit.ly/2JAymaC still shows all type
  values even though type is being filtered by `type=CHECKLIST`.

- type:

  Type of name. One of occurrence, checklist, or metadata.

- hl:

  (logical) Set `hl=TRUE` to highlight terms matching the query when in
  fulltext search fields. The highlight will be an emphasis tag of class
  `gbifH1` e.g. `query='plant', hl=TRUE`. Fulltext search fields
  include: title, keyword, country, publishing country, publishing
  organization title, hosting organization title, and description. One
  additional full text field is searched which includes information from
  metadata documents, but the text of this field is not returned in the
  response.

- issue:

  Filters by issue. Issue has to be related to names. Type
  [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md)
  to get complete list of issues.

- constituentKey:

  Filters by the dataset's constituent key (a uuid).

- verbose:

  (logical) If `TRUE`, all data is returned as a list for each element.
  If `FALSE` (default) a subset of the data that is thought to be most
  essential is organized into a data.frame.

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
metadata (`meta`), the data itself (`data`), the taxonomic hierarchy
data (`hierarchies`), and vernacular names (`names`). In addition, the
object has attributes listing the user supplied arguments and type of
search, which is, differently from occurrence data, always equals to
'single' even if multiple values for some parameters are given. `meta`
is a list of length four with offset, limit, endOfRecords and count
fields. `data` is a tibble (aka data.frame) containing all information
about the found taxa. `hierarchies` is a list of data.frame's, one per
GBIF key (taxon), containing its taxonomic classification. Each
data.frame contains two columns: `rankkey` and `name`. `names` returns a
list of data.frame's, one per GBIF key (taxon), containing all
vernacular names. Each data.frame contains two columns: `vernacularName`
and `language`.

A list of length five:

- **metadata**

- **data**: either a data.frame (`verbose=FALSE`, default) or a list
  (`verbose=TRUE`).

- **facets**

- **hierarchies**

- **names**

## Deprecation Notice

**This function is deprecated.** It only works with the GBIF Backbone
Taxonomy and does not support COL (Catalogue of Life) Extended Release.
Use `rcol::col_search()` from the rcol package instead for COL XR
support.

## Repeat parameter inputs

Some parameters can take many inputs, and treated as 'OR' (e.g., a or b
or c). The following take many inputs:

- **rank**

- **higherTaxonKey**

- **status**

- **habitat**

- **nameType**

- **datasetKey**

- **origin**

## References

<https://www.gbif.org/developer/species#searching>

## Examples

``` r
if (FALSE) { # \dontrun{
# Look up names like mammalia
name_lookup(query='mammalia', limit = 20)

# Start with an offset
name_lookup(query='mammalia', limit=1)
name_lookup(query='mammalia', limit=1, start=2)

# large requests (paging is internally implemented).
# hard maximum limit set by GBIF API: 99999
# name_lookup(query = "Carnivora", limit = 10000)

# Get all data and parse it, removing descriptions which can be quite long
out <- name_lookup('Helianthus annuus', rank="species", verbose=TRUE)
lapply(out$data, function(x) {
  x[!names(x) %in% c("descriptions","descriptionsSerialized")]
})

# Search for a genus
name_lookup(query="Cnaemidophorus", rank="genus")
# Limit records to certain number
name_lookup('Helianthus annuus', rank="species", limit=2)

# Query by habitat
name_lookup(habitat = "terrestrial", limit=2)
name_lookup(habitat = "marine", limit=2)
name_lookup(habitat = "freshwater", limit=2)

# Using faceting
name_lookup(facet='status', limit=0, facetMincount='70000')
name_lookup(facet=c('status','higherTaxonKey'), limit=0,
  facetMincount='700000')

name_lookup(facet='nameType', limit=0)
name_lookup(facet='habitat', limit=0)
name_lookup(facet='datasetKey', limit=0)
name_lookup(facet='rank', limit=0)
name_lookup(facet='isExtinct', limit=0)

name_lookup(isExtinct=TRUE, limit=0)

# text highlighting
## turn on highlighting
res <- name_lookup(query='canada', hl=TRUE, limit=5)
res$data
name_lookup(query='canada', hl=TRUE, limit=45)
## and you can pass the output to gbif_names() function
res <- name_lookup(query='canada', hl=TRUE, limit=5)
gbif_names(res)

# Lookup by datasetKey (set up sufficient high limit, API maximum: 99999)
# name_lookup(datasetKey='3f8a1297-3259-4700-91fc-acc4170b27ce',
#   limit = 50000)

# Some parameters accept many inputs, treated as OR
name_lookup(rank = c("family", "genus"))
name_lookup(higherTaxonKey = c("119", "120", "121", "204"))
name_lookup(status = c("misapplied", "synonym"))$data
name_lookup(habitat = c("marine", "terrestrial"))
name_lookup(nameType = c("cultivar", "doubtful"))
name_lookup(datasetKey = c("73605f3a-af85-4ade-bbc5-522bfb90d847",
  "d7c60346-44b6-400d-ba27-8d3fbeffc8a5"))
name_lookup(datasetKey = "289244ee-e1c1-49aa-b2d7-d379391ce265",
  origin = c("SOURCE", "DENORMED_CLASSIFICATION"))

# Pass on curl options
name_lookup(query='Cnaemidophorus', rank="genus",
  curlopts = list(verbose = TRUE))
} # }
```
