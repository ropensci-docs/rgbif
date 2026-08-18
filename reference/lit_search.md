# Search for literature that cites GBIF mediated data

Search for literature that cites GBIF mediated data

## Usage

``` r
lit_search(
  q = NULL,
  countriesOfResearcher = NULL,
  countriesOfCoverage = NULL,
  literatureType = NULL,
  relevance = NULL,
  year = NULL,
  topics = NULL,
  datasetKey = NULL,
  publishingOrg = NULL,
  peerReview = NULL,
  openAccess = NULL,
  downloadKey = NULL,
  doi = NULL,
  journalSource = NULL,
  journalPublisher = NULL,
  flatten = TRUE,
  abstract = FALSE,
  limit = NULL,
  curlopts = list(http_version = 2)
)

lit_count(...)

lit_export(
  q = NULL,
  countriesOfResearcher = NULL,
  countriesOfCoverage = NULL,
  literatureType = NULL,
  relevance = NULL,
  year = NULL,
  topics = NULL,
  datasetKey = NULL,
  publishingOrg = NULL,
  peerReview = NULL,
  openAccess = NULL,
  downloadKey = NULL,
  doi = NULL,
  journalSource = NULL,
  journalPublisher = NULL,
  flatten = NULL,
  abstract = FALSE,
  limit = NULL,
  curlopts = list()
)
```

## Arguments

- q:

  (character) Simple full text search parameter. The value for this
  parameter can be a simple word or a phrase. Wildcards are not
  supported.

- countriesOfResearcher:

  (character) Country of institution with which author is affiliated,
  e.g. DK (for Denmark). Country codes are listed in
  enumeration_country().

- countriesOfCoverage:

  (character) Country of focus of study, e.g. BR (for Brazil). Country
  codes are listed in enumeration_country().

- literatureType:

  (character) Type of literature ("JOURNAL", "BOOK_SECTION",
  "WORKING_PAPER", "REPORT", "GENERIC", "THESIS",
  "CONFERENCE_PROCEEDINGS", "WEB_PAGE").

- relevance:

  (character) How is the publication relate to GBIF. See details
  ("GBIF_USED", "GBIF_MENTIONED", "GBIF_PUBLISHED", "GBIF_CITED",
  "GBIF_CITED", "GBIF_PUBLISHED", "GBIF_ACKNOWLEDGED", "GBIF_AUTHOR").

- year:

  (integer) Year of publication.

- topics:

  (character) Topic of publication.

- datasetKey:

  (character) GBIF dataset uuid referenced in publication.

- publishingOrg:

  (character) Publisher uuid whose dataset is referenced in publication.

- peerReview:

  (logical) Has publication undergone peer-review?

- openAccess:

  (logical) Is publication Open Access?

- downloadKey:

  (character) Download referenced in publication.

- doi:

  (character) Digital Object Identifier (DOI).

- journalSource:

  (character) Journal of publication.

- journalPublisher:

  (character) Publisher of journal.

- flatten:

  (logical) should any lists in the resulting data be flattened into
  comma-seperated strings? Ignored in lit_export.

- abstract:

  (logical) should the abstract be included in the results. Ignored for
  lit_search.

- limit:

  how many records to return. limit=NULL will fetch up to 10,000.

- curlopts:

  list of named curl options passed on to HttpClient. see
  curl::curl_options for curl options.

- ...:

  additional parameters passed to lit_search

## Value

A named list with two values: `$data` and `$meta`. `$data` is a
`data.frame` of literature references.

## Details

This function enables you to search for literature indexed by GBIF,
including peer-reviewed papers, citing GBIF datasets and downloads. The
literature API powers the [literature
search](https://www.gbif.org/resource/search?contentType=literature) on
GBIF.

The GBIF Secretariat maintains an ongoing [literature tracking
programme](https://www.gbif.org/literature-tracking), which identifies
research uses and citations of biodiversity information accessed through
GBIF’s global infrastructure.

In the literature database, **relevance** refers to how publications
relate to GBIF following these definitions:

- GBIF_USED : makes substantive use of data in a quantitative analysis
  (e.g. ecological niche modelling)

- GBIF_CITED : cites a qualitative fact derived in data (e.g. a given
  species is found in a given country)

- GBIF_DISCUSSED : discusses GBIF as an infrastructure or the use of
  data

- GBIF_PRIMARY : GBIF is the primary source of data (no longer applied)

- GBIF_ACKNOWLEDGED : acknowledges GBIF (but doesn't use or cite data)

- GBIF_PUBLISHED : describes or talks about data published to GBIF

- GBIF_AUTHOR : authored by GBIF staff

- GBIF_MENTIONED : unspecifically mentions GBIF or the GBIF portal

- GBIF_FUNDED : funded by GBIF or a GBIF-managed funding programme

The following arguments can take multiple values:

- relevance

- countriesOfResearcher

- countriesOfCoverage

- literatureType

- topics

- datasetKey

- publishingOrg

- downloadKey

- doi

- journalSource

- journalPublisher

If `flatten=TRUE`, then **data** will be returned as flat data.frame
with no complex column types (i.e. no lists or data.frames).

`limit=NULL` will return up to 10,000 records. The maximum value for
`limit` is 10,000. If no filters are used, only the first 1,000 records
will be returned, limit must be explicitly set to `limit=10000`, to get
the first 10,000 records in this case.

`lit_count()` is a convenience wrapper, which will return the number of
literature references for a certain `lit_search()` query. This is the
same as running `lit_search()$meta$count`.

## Examples

``` r
if (FALSE) { # \dontrun{
lit_search(q="bats")$data 
lit_search(datasetKey="50c9509d-22c7-4a22-a47d-8c48425ef4a7")
lit_search(year=2020)
lit_search(year="2011,2020") # year ranges
lit_search(relevance=c("GBIF_CITED","GBIF_USED")) # multiple values
lit_search(relevance=c("GBIF_USED","GBIF_CITED"), 
topics=c("EVOLUTION","PHYLOGENETICS"))
lit_count() # total number of literature referencing GBIF
lit_count(peerReview=TRUE)
# number of citations of iNaturalist 
lit_count(datasetKey="50c9509d-22c7-4a22-a47d-8c48425ef4a7")
# number of peer-reviewed articles used GBIF mediated data
lit_count(peerReview=TRUE,literatureType="JOURNAL",relevance="GBIF_USED")
 
# Typically what is meant by "literature that uses GBIF" 
lit_search(peerReview=TRUE,literatureType="JOURNAL",relevance="GBIF_USED")
lit_count(peerReview=TRUE,literatureType="JOURNAL",relevance="GBIF_USED")
} # }
```
