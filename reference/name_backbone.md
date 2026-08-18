# Match names to GBIF backbone and other checklists.

Match names to GBIF backbone and other checklists.

## Usage

``` r
name_backbone(
  name = NULL,
  rank = NULL,
  kingdom = NULL,
  phylum = NULL,
  class = NULL,
  order = NULL,
  superfamily = NULL,
  family = NULL,
  subfamily = NULL,
  tribe = NULL,
  subtribe = NULL,
  genus = NULL,
  subgenus = NULL,
  species = NULL,
  usageKey = NULL,
  taxonID = NULL,
  taxonConceptID = NULL,
  scientificNameID = NULL,
  scientificNameAuthorship = NULL,
  genericName = NULL,
  specificEpithet = NULL,
  infraspecificEpithet = NULL,
  verbatimTaxonRank = NULL,
  exclude = NULL,
  strict = NULL,
  verbose = FALSE,
  checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b",
  start = NULL,
  limit = NULL,
  curlopts = list(http_version = 2)
)

name_backbone_verbose(
  name = NULL,
  rank = NULL,
  kingdom = NULL,
  phylum = NULL,
  class = NULL,
  order = NULL,
  superfamily = NULL,
  family = NULL,
  subfamily = NULL,
  tribe = NULL,
  subtribe = NULL,
  genus = NULL,
  subgenus = NULL,
  species = NULL,
  usageKey = NULL,
  taxonID = NULL,
  taxonConceptID = NULL,
  scientificNameID = NULL,
  scientificNameAuthorship = NULL,
  genericName = NULL,
  specificEpithet = NULL,
  infraspecificEpithet = NULL,
  verbatimTaxonRank = NULL,
  exclude = NULL,
  strict = NULL,
  checklistKey = NULL,
  start = NULL,
  limit = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- name:

  (character) Full scientific name potentially with authorship
  (required)

- rank:

  (character) Filter by taxonomic rank. See API reference for available
  values.

- kingdom:

  (character) Kingdom to match.

- phylum:

  (character) Phylum to match.

- class:

  (character) Class to match.

- order:

  (character) Order to match.

- superfamily:

  (character) Superfamily to match.

- family:

  (character) Family to match.

- subfamily:

  (character) Subfamily to match.

- tribe:

  (character) Tribe to match.

- subtribe:

  (character) Subtribe to match.

- genus:

  (character) Genus to match.

- subgenus:

  (character) Subgenus to match.

- species:

  (character) Species to match.

- usageKey:

  (character) The usage key to look up. When provided, all other fields
  are ignored.

- taxonID:

  (character) The taxon ID to look up. Matches to a taxonID will take
  precedence over scientificName values supplied. A comparison of the
  matched scientific and taxonID is performed tocheck for
  inconsistencies.

- taxonConceptID:

  (character) The taxonConceptID to match. Matches to a taxonConceptID
  will take precedence over scientificName values supplied. A comparison
  of the matched scientific and taxonConceptID is performed to check for
  inconsistencies.

- scientificNameID:

  (character) Matches to a scientificNameID will take precedence over
  scientificName values supplied. A comparison of the matched scientific
  and scientificNameID is performed to check for inconsistencies.

- scientificNameAuthorship:

  (character) The scientific name authorship to match against.

- genericName:

  (character) Generic part of the name to match when given as atomised
  parts instead of the full name parameter.

- specificEpithet:

  (character) Specific epithet to match.

- infraspecificEpithet:

  (character) Infraspecific epithet to match.

- verbatimTaxonRank:

  (character) Filters by free text taxon rank.

- exclude:

  (character) An array of usage keys to exclude from the match.

- strict:

  (logical) If set to true, fuzzy matches only the given name, but never
  a taxon in the upper classification.

- verbose:

  (logical) If set to true, it shows alternative matches which were
  considered but then rejected.

- checklistKey:

  (character) The key of a checklist to use. The default is the GBIF
  Backbone taxanomy.

- start:

  (integer) Currently ignored.

- limit:

  (integer) Currently ignored.

- curlopts:

  A list of curl options passed on to
  [`httr::GET()`](https://httr.r-lib.org/reference/GET.html).

## Value

A single row `tibble` of the best matched name. If `verbose=TRUE`, a
longer `tibble` with all potential alternatives is returned.

## Details

If you don't get a match, GBIF gives back a data.frame with columns
`synonym`, `confidence`, and `matchType='NONE'`.

`name_backbone_verbose()` is a legacy wrapper function that returns
returns alternatives in a separate `tibble`.

## References

<https://techdocs.gbif.org/en/openapi/v1/species#/Searching%20names/matchNames>

## Examples

``` r
if (FALSE) { # \dontrun{
# Returns COL (Catalogue of Life) Extended Release alpha-numeric keys
name_backbone("Calopteryx splendens") # Returns usageKey "Q2M4"
name_backbone("Calopteryx splendens", kingdom = "Animalia")
name_backbone("Calopteryx splendens", kingdom = "Animalia", verbose = TRUE)
name_backbone_verbose("Calopteryx splendens", kingdom = "Animalia")
name_backbone("Calopteryx splendens", kingdom = "Plantae")

# Use GBIF Backbone Taxonomy by explicitly setting checklistKey
name_backbone("Calopteryx splendens", 
  checklistKey = "d7dddbf4-2cf0-4f39-9b2a-bb099caae36c")

} # }
```
