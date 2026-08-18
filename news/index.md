# Changelog

## rgbif 3.9.0

#### BREAKING CHANGES

**Default taxonomy changed from GBIF Backbone to COL (Catalogue of Life)
Extended Release**
([\#895](https://github.com/ropensci/rgbif/issues/895))

[Migration
Guide](https://docs.ropensci.org/rgbif/articles/col_migration_guide.html)

The following functions now use COL Extended Release
(`checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b"`) as the default
taxonomy:

- [`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md) -
  Returns COL XR alpha-numeric taxon keys (e.g., “Q2M4”) instead of
  numeric GBIF Backbone keys
- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md) -
  Matches names against COL XR by default  
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md) -
  Searches using COL XR taxonomy
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md) -
  Creates downloads with COL XR taxonomy
- [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md) -
  Prepares downloads with COL XR taxonomy
- [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md) -
  Fetches maps using COL XR taxonomy
- [`mvt_fetch()`](https://docs.ropensci.org/rgbif/reference/mvt_fetch.md) -
  Fetches map vector tiles using COL XR taxonomy

#### DEPRECATED

The following functions are deprecated because they use the GBIF
Backbone taxonomy, and will not work with COL XR keys.

- [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md) -
  use `rcol::col_search()` instead
- [`name_suggest()`](https://docs.ropensci.org/rgbif/reference/name_suggest.md) -
  use `rcol::col_suggest()` instead
- [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md) -
  use `rcol::col_usage()` instead
- [`name_issues()`](https://docs.ropensci.org/rgbif/reference/name_issues.md) -
  use `rcol::col_usage()` to parse and examine name issues

Additionally:

- [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md) -
  deprecated because it relies on a non-GBIF web service (GeoNames) and
  will be removed in a future version
  ([\#473](https://github.com/ropensci/rgbif/issues/473))

#### NEW FEATURE

[`gbif_to_col()`](https://docs.ropensci.org/rgbif/reference/gbif_to_col.md) -
Convert GBIF Backbone numeric taxon keys to COL Extended Release
alpha-numeric keys. Returns the full API response including usage
details, classification hierarchy, and match diagnostics.

#### MINOR IMPROVEMENTS

- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now returns `classifications` as a named list of tibbles, with one
  tibble per checklistKey (taxonomy source). Each tibble contains one
  row per occurrence with taxonomic ranks pivoted into camelCase columns
  (checklistKey, kingdomName, kingdomKey, phylumName, phylumKey,
  className, classKey, etc.). This structure makes it easy to work with
  occurrences from different taxonomies separately while keeping the
  checklistKey information with the data. Known checklists (COL,
  backbone) are shown with friendly names, while unknown checklists use
  their UUID.  
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now detects numeric taxonomic keys (taxonKey, speciesKey, kingdomKey,
  etc.) and automatically switches to the GBIF Backbone taxonomy
  checklistKey with a warning message. These numeric keys are legacy
  identifiers from the GBIF Backbone taxonomy. Users are advised to
  migrate to COL XR identifiers using
  [`gbif_to_col()`](https://docs.ropensci.org/rgbif/reference/gbif_to_col.md).
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  and
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  now detect numeric taxonomic keys in predicates and automatically
  inject the GBIF Backbone checklistKey at the predicate level with a
  warning message. This ensures existing code using numeric keys
  continues to work correctly.
- [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  now warns when `datasetKey` parameter is ignored. When a `key` is
  provided, the GBIF API ignores the `datasetKey` parameter and returns
  data based solely on the key. A warning is now issued to alert users
  of this behavior
  ([\#899](https://github.com/ropensci/rgbif/issues/899)).

## rgbif 3.8.5

CRAN release: 2026-03-20

#### NEW FEATURES

New functions for accessing GBIF occurrence download statistics
([\#837](https://github.com/ropensci/rgbif/issues/837))
([\#823](https://github.com/ropensci/rgbif/issues/823)):

- [`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md)
  to retrieve summarized download statistics
- [`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md)
  to export download summaries
- [`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md)
  to get downloads by user country
- [`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md)
  to get downloaded records by dataset
- [`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md)
  to get downloads by dataset
- [`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md)
  to get downloads by source

[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
now supports downloading multiple taxonomy downloads.
([\#830](https://github.com/ropensci/rgbif/issues/830))
([\#832](https://github.com/ropensci/rgbif/issues/832))
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
now supports downloading verbatim extension data.
([\#829](https://github.com/ropensci/rgbif/issues/829))
([\#831](https://github.com/ropensci/rgbif/issues/831))

#### BUG FIXES

Fixed bug in
[`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md).
([\#820](https://github.com/ropensci/rgbif/issues/820))
([\#822](https://github.com/ropensci/rgbif/issues/822)) Fixed
[`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
to include `acceptedUsageKey` and `acceptedScientificName` in output.
([\#824](https://github.com/ropensci/rgbif/issues/824))
([\#826](https://github.com/ropensci/rgbif/issues/826))

#### MINOR IMPROVEMENTS

Removed `wk` package dependency and implemented internal WKT validation.
([\#827](https://github.com/ropensci/rgbif/issues/827))
([\#828](https://github.com/ropensci/rgbif/issues/828))

#### DOCUMENTATION

Clarified license format in download predicates documentation.
([\#836](https://github.com/ropensci/rgbif/issues/836))

## rgbif 3.8.4

CRAN release: 2025-11-13

#### NEW FEATURES

[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
now supports searching for occurrence by `checklistKey`.
([\#801](https://github.com/ropensci/rgbif/issues/801))
[`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
and
[`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
now use GBIF API v2 for matching.
([\#797](https://github.com/ropensci/rgbif/issues/797))

#### BUG FIXES

Fixed bug in
[`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
where large numbers of async requests were not being handled properly.
([\#815](https://github.com/ropensci/rgbif/issues/815)) Fixed bug with
`dnaSequenceID` in
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
results. ([\#810](https://github.com/ropensci/rgbif/issues/810))

## rgbif 3.8.3

CRAN release: 2025-09-04

#### NEW FEATURES

[`installation_search()`](https://docs.ropensci.org/rgbif/reference/installation_search.md)
and
[`collection_search()`](https://docs.ropensci.org/rgbif/reference/collection_search.md)
allow you to search for GRSciColl institutions and collections.
([\#554](https://github.com/ropensci/rgbif/issues/554))

#### BUG FIXES

Fixed “Error in the HTTP2 framing layer” bug by setting
`curlopts = list(http_version=2)` as the default for most functions.
([\#805](https://github.com/ropensci/rgbif/issues/805))

#### MINOR IMPROVEMENTS

The GBIF occurrence search API now actively discourages the use of bulk
downloads via paging through occurrence records using
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
or related functions. When a user has exceeded a certain threshold of
requests, they will be temporarily paused for 5 seconds. A message will
be printed to the console when this happens. Users are strongly
encouraged to use
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
for bulk downloads.
([\#804](https://github.com/ropensci/rgbif/issues/804))

## rgbif 3.8.2

CRAN release: 2025-06-12

#### NEW FEATURES

[`occ_download_doi()`](https://docs.ropensci.org/rgbif/reference/occ_download_doi.md)
accepts a GBIF download DOI and returns the download key.
([\#743](https://github.com/ropensci/rgbif/issues/743))
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
now supports download via `institutionKey`.
([\#785](https://github.com/ropensci/rgbif/issues/785))

### BUG FIXES

Fixed double import bug in
[`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md).
([\#765](https://github.com/ropensci/rgbif/issues/765)) Fixed URL
encoding bug in
[`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md).
([\#784](https://github.com/ropensci/rgbif/issues/784))

#### DOCUMENTATION

Several small improvements to the docs.
([\#777](https://github.com/ropensci/rgbif/issues/777))
([\#776](https://github.com/ropensci/rgbif/issues/776))
([\#773](https://github.com/ropensci/rgbif/issues/773))
([\#763](https://github.com/ropensci/rgbif/issues/763))
([\#758](https://github.com/ropensci/rgbif/issues/758))

## rgbif 3.8.1

CRAN release: 2024-09-27

#### NEW FEATURES

- New function
  [`occ_download_sql()`](https://docs.ropensci.org/rgbif/reference/occ_download_sql.md)
  for downloading occurrence data using SQL queries.
  ([\#752](https://github.com/ropensci/rgbif/issues/752))

### BUG FIXES

- [`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md)
  bug fixed. ([\#748](https://github.com/ropensci/rgbif/issues/748))

#### DOCUMENTATION

- New article [GBIF SQL
  Downloads](https://docs.ropensci.org/rgbif/articles/gbif_sql_downloads.html)

## rgbif 3.8.0

CRAN release: 2024-05-23

#### NEW FEATURES

- Added many missing
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  terms. ([\#698](https://github.com/ropensci/rgbif/issues/698))
- New function
  [`occ_download_describe()`](https://docs.ropensci.org/rgbif/reference/occ_download_describe.md)
  for getting information about download formats.
  ([\#721](https://github.com/ropensci/rgbif/issues/721))

#### MINOR IMPROVEMENTS

- Added `constituentKey` to
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md).
  ([\#729](https://github.com/ropensci/rgbif/issues/729))
- Added support for `gbifId` downloads
  ([\#711](https://github.com/ropensci/rgbif/issues/711))

### BUG FIXES

- `check_inputs()`bug fixed.
  ([\#706](https://github.com/ropensci/rgbif/issues/706))

#### DOCUMENTATION

- New article [Effectively using
  occ_search](https://docs.ropensci.org/rgbif/articles/effectively_using_occ_search.html)
- Guidance for reversing WKT winding order.
  ([\#724](https://github.com/ropensci/rgbif/issues/724))

#### DEPRECATED

- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  datasetKey methods no longer supported
  ([\#716](https://github.com/ropensci/rgbif/issues/716))
- “axe” feature in
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  is no longer supported.
  ([\#718](https://github.com/ropensci/rgbif/issues/718))
- [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  is soft deprecated and supported for legacy reasons only, and will no
  longer add new features.

## rgbif 3.7.9

CRAN release: 2024-01-11

#### NEW FEATURES

There have been many additions for accessing dataset metadata.

- [`dataset_export()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  downloads all of the results of a
  [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md).

- New functions for getting dataset metadata from a datasetkey (uuid) :
  [`dataset_get()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_process()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_networks()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_constituents()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_comment()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_contact()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_endpoint()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_identifier()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_machinetag()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_tag()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md),
  [`dataset_metrics()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md).

- New function for getting more obscure dataset metadata, such as
  machineTags:
  [`dataset()`](https://docs.ropensci.org/rgbif/reference/dataset.md).

- New functions for listing dataset metadata :
  [`dataset_noendpoint()`](https://docs.ropensci.org/rgbif/reference/dataset_list_funs.md),
  [`dataset_duplicate()`](https://docs.ropensci.org/rgbif/reference/dataset_list_funs.md).

- [`dataset_doi()`](https://docs.ropensci.org/rgbif/reference/dataset_doi.md)
  gets dataset metadata from the dataset’s doi.

#### MINOR IMPROVEMENTS

- Error message improvements for
  [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md).
  ([\#686](https://github.com/ropensci/rgbif/issues/686))

#### Documentation

- New article [Getting Dataset Metadata From
  GBIF](https://docs.ropensci.org/rgbif/articles/getting_dataset_info.html)

#### DEPRECATED

- There are no longer static data files in rgbif. This data is better
  fetched fresh from the appropriate endpoints.
  ([\#690](https://github.com/ropensci/rgbif/issues/690))
  ([\#688](https://github.com/ropensci/rgbif/issues/688))

- [`datasets()`](https://docs.ropensci.org/rgbif/reference/datasets.md)
  is soft deprecated, since the interface was overloaded and confusing.
  See functional replacements above.

## rgbif 3.7.8

CRAN release: 2023-09-11

- **rgbif** has a new logo.
  ([\#679](https://github.com/ropensci/rgbif/issues/679))

#### NEW FEATURES

- [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  now returns a base map as a `magick::magick-image`. This allows for
  the creation of high quality images from the GBIF maps API.
  ([\#675](https://github.com/ropensci/rgbif/issues/675))
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  terms added to key lookup.
  ([\#661](https://github.com/ropensci/rgbif/issues/661))
  ([\#589](https://github.com/ropensci/rgbif/issues/589))
- [`pred_default()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  is an
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  pred function that allows users to easily filter out commonly unwanted
  occurrence records.
  ([\#611](https://github.com/ropensci/rgbif/issues/611))

#### MINOR IMPROVEMENTS

- Stream error fixed (“HTTP/2 stream 15 was not closed cleanly before
  end of the underlying stream”). Now
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md),
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md),
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md),
  and
  [`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md)
  have `curlopts = list(http_version=2)`, which fixes the error. This
  might need to be the default setting for the whole package.
  ([\#656](https://github.com/ropensci/rgbif/issues/656))

- [`name_suggest()`](https://docs.ropensci.org/rgbif/reference/name_suggest.md)
  now gives a warning at prevents setting the `limit` \> 100, since this
  is the GBIF API max.
  ([\#657](https://github.com/ropensci/rgbif/issues/657))

#### Documentation

New article [Creating maps from
occurrences](https://docs.ropensci.org/rgbif/articles/creating_maps_from_occurrences.html),
which explains how to use
[`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md).

#### DEPRECATED

- [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  is now deprecated, since it is difficult to maintain, and not widely
  used. ([\#651](https://github.com/ropensci/rgbif/issues/651))

## rgbif 3.7.7

CRAN release: 2023-04-03

#### MINOR IMPROVEMENTS

- Fixes test that was causing errors on CRAN.

## rgbif 3.7.6

CRAN release: 2023-03-23

#### BREAKING CHANGE

- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  parameter `type` is now deprecated and will no longer work correctly.
  Please see
  [`occ_count_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
  [`occ_count_pub_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
  [`occ_count_year()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md),
  [`occ_count_basis_of_record()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)
  for replacements.
  ([\#622](https://github.com/ropensci/rgbif/issues/622))

#### DEPRECATED

- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  parameters `georeferenced`, `type`, `date`, `to`, `from` are no longer
  supported and not guaranteed to work correctly.
  ([\#622](https://github.com/ropensci/rgbif/issues/622))
- [`occ_facet()`](https://docs.ropensci.org/rgbif/reference/occ_facet.md)
  and
  [`count_facet()`](https://docs.ropensci.org/rgbif/reference/count_facet.md)
  are now deprecated use `occ_count(facet="x")` instead.

#### NEW FEATURES

- [`lit_search()`](https://docs.ropensci.org/rgbif/reference/lit_search.md)
  now supports searching the GBIF literature API.
  ([\#591](https://github.com/ropensci/rgbif/issues/591))
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  now supports almost all
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  queries. ([\#622](https://github.com/ropensci/rgbif/issues/622))
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  now supports the facets interface through `occ_count(facet="x")`.
  ([\#622](https://github.com/ropensci/rgbif/issues/622))  
- [`organizations()`](https://docs.ropensci.org/rgbif/reference/organizations.md)
  (aka publishers) now supports the use of getting lists of publishers
  by `country`. ([\#606](https://github.com/ropensci/rgbif/issues/606))
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now support downloading and getting occurrences a certain distance
  from known country/area centroids via the parameter
  `distanceFromCentroidInMeters`.
  ([\#594](https://github.com/ropensci/rgbif/issues/594))

#### MINOR IMPROVEMENTS

- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now supports more multi-valued parameters.
  ([\#617](https://github.com/ropensci/rgbif/issues/617))
- Removed dependencies on `randgeo` and `conditionz`.
  ([\#624](https://github.com/ropensci/rgbif/issues/624))
  ([\#625](https://github.com/ropensci/rgbif/issues/625))

#### Documentation

New article explaining
[`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
changes and new features [Getting Occurrence Counts From
GBIF](https://docs.ropensci.org/rgbif/articles/occ_counts.html).

## rgbif 3.7.5

CRAN release: 2023-01-05

#### NEW FEATURES

- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  now accepts `strict=TRUE`, meaning that only non-fuzzy matches are
  returned. ([\#565](https://github.com/ropensci/rgbif/issues/565))
- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  now accepts default values for high taxonomy, such as kingdom, phylum,
  family, ect. ([\#515](https://github.com/ropensci/rgbif/issues/515))
- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  now returns a column `is_alternative` when `verbose=TRUE`, which lets
  the user know if a name was originally considered to be an alternative
  choice by the name matcher.
  ([\#515](https://github.com/ropensci/rgbif/issues/515))

#### DOCUMENTATION

- Updated README to be more inviting to new users
  ([\#574](https://github.com/ropensci/rgbif/issues/574))
- Added data quality section to article [Getting Occurrence Data From
  GBIF](https://docs.ropensci.org/rgbif/articles/getting_occurrence_data.html).
  ([\#575](https://github.com/ropensci/rgbif/issues/575))

#### MINOR IMPROVEMENTS

- removed `sp` and `rgeos` dependencies.
  ([\#578](https://github.com/ropensci/rgbif/issues/578))

## rgbif 3.7.4

CRAN release: 2022-12-06

#### NEW FEATURES

- `name_usage` now has the ability to fetch iucn red list categories
  using `data=iucnRedListCategory`.
  ([\#547](https://github.com/ropensci/rgbif/issues/547))

#### DOCUMENTATION

- `name_backbone_checklist` updated definition of `verbose` argument.
  ([\#564](https://github.com/ropensci/rgbif/issues/564))
- “Too many choices” warning added to article [Working With Taxonomic
  Names](https://docs.ropensci.org/rgbif/articles/taxonomic_names.html).
  ([\#536](https://github.com/ropensci/rgbif/issues/536))

#### BUG FIXES

- `dataset_gridded` bug fixed when inputting only one non-gridded
  dataset. ([\#546](https://github.com/ropensci/rgbif/issues/546))

#### MINOR IMPROVEMENTS

- New CRAN checks badge URL.
  ([\#555](https://github.com/ropensci/rgbif/issues/555))
- Update min vcr requirement to (\>= 1.2.0).
  ([\#559](https://github.com/ropensci/rgbif/issues/559))
- Updated r-lib actions to v2
  ([\#566](https://github.com/ropensci/rgbif/issues/566))

## rgbif 3.7.3

CRAN release: 2022-09-03

#### NEW FEATURES

- Added missing search parameters for
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  ([\#530](https://github.com/ropensci/rgbif/issues/530))
- Added missing
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  terms to key lookup
  ([\#541](https://github.com/ropensci/rgbif/issues/541))
- Support for identifying “gridded datasets” with experimental API using
  [`dataset_gridded()`](https://docs.ropensci.org/rgbif/reference/dataset_gridded.md)
  ([\#516](https://github.com/ropensci/rgbif/issues/516))
- Look up the datasets in a GBIF network with
  [`network_constituents()`](https://docs.ropensci.org/rgbif/reference/network.md)
  ([\#527](https://github.com/ropensci/rgbif/issues/527))
- Added support for using GBIF experimental reverse geocoding API
  [`gbif_geocode()`](https://docs.ropensci.org/rgbif/reference/gbif_geocode.md)
  ([\#521](https://github.com/ropensci/rgbif/issues/521))

#### DEPRECATED

- [`networks()`](https://docs.ropensci.org/rgbif/reference/networks.md)
  is deprecated and called
  [`network()`](https://docs.ropensci.org/rgbif/reference/network.md)
  instead. ([\#527](https://github.com/ropensci/rgbif/issues/527))
- [`parsenames()`](https://docs.ropensci.org/rgbif/reference/parsenames.md)
  is deprecated and called
  [`name_parse()`](https://docs.ropensci.org/rgbif/reference/name_parse.md)
  for better alignment with other `name_*` functions.
  ([\#504](https://github.com/ropensci/rgbif/issues/504))

#### BUG FIXES

- `occ_search` fixed bug related to networkKey in the column names
  ([\#524](https://github.com/ropensci/rgbif/issues/524))

## rgbif 3.7.2

CRAN release: 2022-04-11

#### MINOR IMPROVEMENTS

- Removing `wellknown` dependency and switching to `wk`
  ([\#512](https://github.com/ropensci/rgbif/issues/512))

#### BUG FIXES

- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  : bug fix related two square brackets in url
  ([\#509](https://github.com/ropensci/rgbif/issues/509))

## rgbif 3.7.1

CRAN release: 2022-03-16

#### BUG FIXES

- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  : bug fixes ([\#501](https://github.com/ropensci/rgbif/issues/501))
  ([\#505](https://github.com/ropensci/rgbif/issues/505))

## rgbif 3.7.0

CRAN release: 2022-02-08

There is a new rgbif maintainer: John Waller.

#### NEW FEATURES

- [`derived_dataset()`](https://docs.ropensci.org/rgbif/reference/derived_dataset.md)
  : New function to register a cleaned or modified dataset on GBIF for
  citation. ([\#467](https://github.com/ropensci/rgbif/issues/467))
- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  : New function that takes a list, vector, or data.frame of scientific
  names and asynchronously matches them to the backbone.
  ([\#475](https://github.com/ropensci/rgbif/issues/475))
- [`pred_isnull()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  : New predicate function that includes NULL values from a column in
  the download. ([\#489](https://github.com/ropensci/rgbif/issues/489))
- `occ_download.print()` : Now prints out much more information
  including a DOI and citation.
  ([\#494](https://github.com/ropensci/rgbif/issues/494))

#### DEPRECATED

- `gbif_citation.gbif()` : it is no longer considered best practice to
  generate a citation from
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  or
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md).
  We recommend
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  or
  [`derived_dataset()`](https://docs.ropensci.org/rgbif/reference/derived_dataset.md)
  instead. ([\#494](https://github.com/ropensci/rgbif/issues/494))

#### MINOR IMPROVEMENTS

- [`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md)
  and
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  : now accept a class character download key directly. The keys does do
  not need to be class “occ_download”.
  ([\#487](https://github.com/ropensci/rgbif/issues/487))
- [`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
  : now returns new columns “verbatim_name”, “verbatim_genus” ect. that
  the user has supplied. This makes it easier for the user to track what
  has been matched. The verbose argument also has been un-retired. If
  `verbose=TRUE`, more results will be returned in a single data.frame.
  ([\#475](https://github.com/ropensci/rgbif/issues/475))
- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  : will now accept a download key directly.
- [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md)
  : Does not throw an error if the data is already present and
  `overwrite=FALSE`, it will just give a warning and return the already
  present dataset. This allows users to run
  `occ_download_get(key) %>% occ_download_import()` multiple times
  without re-downloading the same file with `overwrite=TRUE`.
- [`download_predicate_dsl()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  : “publishingOrg” now added as a download key.
  ([\#496](https://github.com/ropensci/rgbif/issues/496)) `key_lkup` now
  includes GBIF-style uppercase keys as well. So `pred("TAXON_KEY",212)`
  and `pred("taxonKey",212)` will both work.

#### DOCUMENTATION

Wrote new articles highlighting new features and encouraging the use of
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
over
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md).

New articles:

- [Citing GBIF Mediated
  Data](https://docs.ropensci.org/rgbif/articles/gbif_citations.html)
- [Set Up Your GBIF Username and
  Password](https://docs.ropensci.org/rgbif/articles/gbif_credentials.html)
- [Getting Occurrence Data From
  GBIF](https://docs.ropensci.org/rgbif/articles/getting_occurrence_data.html)
- [Downloading A Long Species
  List](https://docs.ropensci.org/rgbif/articles/downloading_a_long_species_list.html)
- [Working With Taxonomic
  Names](https://docs.ropensci.org/rgbif/articles/taxonomic_names.html)

#### BUG FIXES

- [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  : fixed bug related to select argument.
  ([\#479](https://github.com/ropensci/rgbif/issues/479))
- [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  : fixed bug related to `sp::CRS`
  ([\#497](https://github.com/ropensci/rgbif/issues/497))

## rgbif 3.6.0

CRAN release: 2021-06-02

#### Downloads

- typo in download predicate functions fixed - `mulitpoint` -\>
  `multipoint` ([\#460](https://github.com/ropensci/rgbif/issues/460))
  thanks [@damianooldoni](https://github.com/damianooldoni) for catching
  that
- added three new predicate keys: `stateProvince`
  ([\#458](https://github.com/ropensci/rgbif/issues/458)), `gadm`
  ([\#462](https://github.com/ropensci/rgbif/issues/462)), and
  `occurrenceStatus`
  ([\#465](https://github.com/ropensci/rgbif/issues/465))

#### MINOR IMPROVEMENTS

- add two new occurrence issues: `FOOTPRINT_SRS_INVALID` and
  `FOOTPRINT_WKT_INVALID`
  ([\#454](https://github.com/ropensci/rgbif/issues/454))
- [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  docs: more information on
  [`data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html)
  parameters and particular ones that would be useful to sort out data
  read issues ([\#461](https://github.com/ropensci/rgbif/issues/461))

#### BUG FIXES

- fix
  [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md):
  downloaded files used to have a certain content type in response
  header we checked for, but its changed at least once even in
  successful responses, so that step has been removed
  ([\#464](https://github.com/ropensci/rgbif/issues/464))
- fix
  [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md):
  country code for Namibia is `NA` - this was turning into the R missing
  value `NA` - now fixed
  ([\#463](https://github.com/ropensci/rgbif/issues/463))

## rgbif 3.5.2

CRAN release: 2021-01-27

#### Download predicates

- in occurrence download predicate builder checks, to better help users,
  give the name of the key that fails upon failure instead of just the
  string ‘key’ ([\#450](https://github.com/ropensci/rgbif/issues/450))
- occurrence download predicates: new key
  `coordinateUncertaintyInMeters` added, e.g. usage:
  `pred_lt("coordinateUncertaintyInMeters",10000)`
  ([\#449](https://github.com/ropensci/rgbif/issues/449))
- [`pred_and()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  and
  [`pred_or()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  slight change: now required that more than one predicate is passed to
  each of these functions because it doesn’t make sense to do an `and`
  or `or` predicate with only one predicate
  ([\#452](https://github.com/ropensci/rgbif/issues/452))
- fix for use of `pred_not(pred_notnull())`
  ([\#452](https://github.com/ropensci/rgbif/issues/452))

#### MINOR IMPROVEMENTS

- add a new occurrence issue (`TAXON_MATCH_AGGREGATE`) and a new name
  issue (`BACKBONE_MATCH_AGGREGATE`)
  ([\#453](https://github.com/ropensci/rgbif/issues/453))

#### BUG FIXES

- remove geoaxe references in man-roxygen template doc files - not using
  pkg anymore here and that pkg is cran archived too
  ([\#448](https://github.com/ropensci/rgbif/issues/448))

## rgbif 3.5.0

CRAN release: 2021-01-13

#### MINOR IMPROVEMENTS

- remove package wicket - use package wellknown instead - no user facing
  changes related to this
  ([\#447](https://github.com/ropensci/rgbif/issues/447))
- remove package geoaxe (to be archived on CRAN soon) - use package sf
  instead ([\#447](https://github.com/ropensci/rgbif/issues/447))

#### BUG FIXES

- fix to download predicate function
  [`pred_not()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md):
  it was not constructing the query correctly, fixed now. user facing
  change as well: it now expects a predicate to be passed, and only a
  single predicate as GBIF not predicate only accepts one predicate
  ([\#446](https://github.com/ropensci/rgbif/issues/446))

## rgbif 3.4.2

CRAN release: 2021-01-06

#### MINOR IMPROVEMENTS

- Add new occurrence issue `DIFFERENT_OWNER_INSTITUTION`
  ([\#444](https://github.com/ropensci/rgbif/issues/444))
- re-record all test fixtures

#### BUG FIXES

- fix bug in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  ([\#443](https://github.com/ropensci/rgbif/issues/443))

## rgbif 3.4

#### MINOR IMPROVEMENTS

- Documentation: clarify for
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  and
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  what parameters accept many values and which do not; in addition, we
  clarify which parameters accept multiple values in the same HTTP
  request, and those that accept multiple values but apply each in
  separate HTTP requests. See also `?many-values` manual file
  ([\#369](https://github.com/ropensci/rgbif/issues/369))
- [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md)
  gains 9 new occurrence issues
  ([\#435](https://github.com/ropensci/rgbif/issues/435))
- for
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  and
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md),
  `basisOfRecord` parameter now supports multiple values, both in one
  request and in different requests, depending on input format (see
  “Multiple values passed to a parameter” section in
  [`?occ_search`](https://docs.ropensci.org/rgbif/reference/occ_search.md))
  ([\#437](https://github.com/ropensci/rgbif/issues/437))
- remove vignettes from cran to avoid cran checks - still available on
  our docs site ([\#438](https://github.com/ropensci/rgbif/issues/438))
- [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md):
  GBIF slightly altered download behavior - we now explicitly follow any
  redirects to get a download
  ([\#439](https://github.com/ropensci/rgbif/issues/439))
- `print.occ_download_meta` (used when you run
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md))
  was printing `NA` for number of results found if no results were ready
  yet - now prints `0` instead of `NA`
  ([\#440](https://github.com/ropensci/rgbif/issues/440))

#### BUG FIXES

- [`count_facet()`](https://docs.ropensci.org/rgbif/reference/count_facet.md)
  fixes: fixed internal fxn for `count_facet` for parsing results, was
  dropping values for facets; added assertions to check parameter types
  input by user for the fxn; changed so that keys and basisofrecord can
  be passed together
  ([\#436](https://github.com/ropensci/rgbif/issues/436))

## rgbif 3.3

#### MINOR IMPROVEMENTS

- added two new occurrence issues to
  [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md):
  `GEOREFERENCED_DATE_INVALID` and `GEOREFERENCED_DATE_UNLIKELY`
  ([\#430](https://github.com/ropensci/rgbif/issues/430))

#### BUG FIXES

- fixed an error in
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  caused by GBIF adding a new field of data to the output of
  `/occurrence/search/`: gadm. cleaned up internals of
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  to drop gadm, and other fields that are complex and take time to parse
  (use
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  if you want all the data fields)
  ([\#427](https://github.com/ropensci/rgbif/issues/427))
- [`gbif_names()`](https://docs.ropensci.org/rgbif/reference/gbif_names.md)
  fix: was ending up with invalid URLs to GBIF species pages because we
  had taxon keys with leading spaces somehow. now all leading and
  trailing spaces in taxon keys removed before making URLs
  ([\#429](https://github.com/ropensci/rgbif/issues/429))

## rgbif 3.2

#### MINOR IMPROVEMENTS

- [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md)
  changes: three new occurrence issues added; one name issue removed
  that’s deprecated
  ([\#423](https://github.com/ropensci/rgbif/issues/423))
- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  rights field was empty unless pulling from a downloaded file; now fill
  in with `license` key; also a fix for when occurrence key passed to
  the function ([\#424](https://github.com/ropensci/rgbif/issues/424))
- `establishmentMeans` now supported in `occ_download`/`pred`
  ([\#420](https://github.com/ropensci/rgbif/issues/420))

#### BUG FIXES

- fix for
  [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md):
  response content-type header changed recently, fixed
  ([\#422](https://github.com/ropensci/rgbif/issues/422))

## rgbif 3.1

#### MINOR IMPROVEMENTS

- finally delete code originally extracted from
  [`plyr::rbind.fill`](https://rdrr.io/pkg/plyr/man/rbind.fill.html) -
  use
  [`data.table::rbindlist`](https://rdrr.io/pkg/data.table/man/rbindlist.html)
  in all cases ([\#417](https://github.com/ropensci/rgbif/issues/417))
- fix failing test on cran for
  [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  ([\#418](https://github.com/ropensci/rgbif/issues/418))
- fix xd refs note on cran (non-file package anchored links) for curl
  pkg function ([\#419](https://github.com/ropensci/rgbif/issues/419))

#### BUG FIXES

- [`occ_download_cancel_staged()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md)
  fix: was broken cause we were indexing to a column in a table with
  `[,"key"]` ([\#416](https://github.com/ropensci/rgbif/issues/416))

## rgbif 3.0

#### BREAKING CHANGE

- Many functions (`occ_search`, `occ_get`, `name_usage`, `name_lookup`,
  `name_suggest`, `name_backbone`, and `dataset_search`) have a `return`
  parameter to toggle what is returned from the function call. To
  simplify rgbif maintenance, we’ve deprecated the `return` parameter.
  We’ve left it in each of the functions, but it no longer does
  anything, other than raising a warning if used. This means that
  function calls to these functions now always return the same data
  structure, making it easier to reason about for the user, as well as
  for us developers trying to make sure the package works as expected
  under a variety of conditions. If you have been using the `return`
  parameter, do the same function call as before, but now index to the
  output you need. This is a breaking change, thus the major version
  bump ([\#413](https://github.com/ropensci/rgbif/issues/413))

#### NEW FEATURES

- new function
  [`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
  which takes the same input as
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
  but instead of starting a query, it checks if you’ve recently made the
  same request (with configureable settings for what “recent” means).
  This can save time when you’re doing occurrence download requests that
  you may have done in the recent past
  ([\#308](https://github.com/ropensci/rgbif/issues/308))

#### MINOR IMPROVEMENTS

- configured package to be able to use two different base urls,
  `api.gbif-uat.org` and `api.gbif.org`. We have only used the latter
  previously, but now can configure rgbif to use the former, mostly for
  testing purposes
  ([\#398](https://github.com/ropensci/rgbif/issues/398))
- [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  gains `encoding` parameter that is passed down to
  [`data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html)
  to make it very clear that encoding can be configured (even though you
  could have before via `...`)
  ([\#414](https://github.com/ropensci/rgbif/issues/414))

#### BUG FIXES

- fix tibble construction
  ([\#412](https://github.com/ropensci/rgbif/issues/412))

## rgbif 2.3

CRAN release: 2020-05-28

#### MINOR IMPROVEMENTS

- max records you can return for `/occurrence/search` route is now
  100,000 (used in
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)).
  updated docs throughout accordingly
  ([\#405](https://github.com/ropensci/rgbif/issues/405))
- improved docs in
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  for how we determine when a job is done. see new section “When is a
  job done?” ([\#409](https://github.com/ropensci/rgbif/issues/409))
- print methods `print.occ_download_prep` and `print.occ_download`
  improved. previously well-known text strings were printed in their
  entirety. now they are handled to only print so many characters; also
  applies to any download predicate string that’s long
  ([\#407](https://github.com/ropensci/rgbif/issues/407))
- [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md)
  now supports using a progress bar by passing in
  [`httr::progress()`](https://httr.r-lib.org/reference/progress.html)
  ([\#402](https://github.com/ropensci/rgbif/issues/402))
- [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  gain two new parameters: `recordedByID` and `identifiedByID`
  ([\#403](https://github.com/ropensci/rgbif/issues/403))

#### BUG FIXES

- fix in `occ_download_queue`: an empty
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  lead to problems; now removing any `NULL`’s from a list of
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  outputs before further work
  ([\#408](https://github.com/ropensci/rgbif/issues/408))
- fix in `occ_download_queue`: we were not accounting for job status
  “cancelled” ([\#409](https://github.com/ropensci/rgbif/issues/409))
- [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  fix: `fill` parameter was set to `TRUE` by default, changed to
  `FALSE`. improved docs for this fxn on passing down parameters to
  [`data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html)
  ([\#404](https://github.com/ropensci/rgbif/issues/404))

## rgbif 2.2

#### MINOR IMPROVEMENTS

- add a section *Download status* to the
  [`?downloads`](https://docs.ropensci.org/rgbif/reference/downloads.md)
  manual file listing all the different download status states a
  download can have and what they mean
  ([\#390](https://github.com/ropensci/rgbif/issues/390))
- fix `gbif_issues`/`gbif_issues_lookup`: added four missing occurrence
  issues to the package (COORDINATE_PRECISION_INVALID,
  COORDINATE_UNCERTAINTY_METERS_INVALID, INDIVIDUAL_COUNT_INVALID, and
  INTERPRETATION_ERROR)
  ([\#400](https://github.com/ropensci/rgbif/issues/400))
- doing real tests now for
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  via vcr ([\#396](https://github.com/ropensci/rgbif/issues/396))

#### BUG FIXES

- fix
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md):
  we were attempting to rearrange columns when no results found, leading
  to an error ([\#399](https://github.com/ropensci/rgbif/issues/399))

## rgbif 2.1

#### DEFUNCT

- the `spellCheck` parameter has been removed from the occurrence
  routes; thus, the
  [`occ_spellcheck()`](https://docs.ropensci.org/rgbif/reference/occ_spellcheck-defunct.md)
  function is now defunct - and the parameter `spellCheck` has been
  removed from
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  ([\#397](https://github.com/ropensci/rgbif/issues/397))

#### MINOR IMPROVEMENTS

- docs fix for
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md):
  remove `...` parameter definition as it wasn’t used in the function
  ([\#394](https://github.com/ropensci/rgbif/issues/394))

#### BUG FIXES

- download predicate fxns fix: “within” wasnt being handled properly
  ([\#393](https://github.com/ropensci/rgbif/issues/393)) thanks
  [@damianooldoni](https://github.com/damianooldoni)

## rgbif 2.0

#### NEW FEATURES

- The download query user interface for
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  has changed in a breaking fashion (thus the major version bump). After
  installation, see
  [`?download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md).
  Much more complex queries are now possible with
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md).
  TL;DR: you now construct queries with functions like
  `pred("taxonKey", 3119195)` rather than passing in strings like
  `taxonKey = 3119195`, and `pred_gt("elevation", 5000)` instead of
  `"elevation > 5000"`
  ([\#362](https://github.com/ropensci/rgbif/issues/362))
- gains new function
  [`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md)
  to re-run
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  until the download is ready - kinda like
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  but for a single download
  ([\#389](https://github.com/ropensci/rgbif/issues/389))
- [`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md)
  gains pagination parameters `limit` and `start` to paginate through
  results ([\#382](https://github.com/ropensci/rgbif/issues/382))
- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  now works with the output of
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  in addition to the other existing inputs it accepts
  ([\#392](https://github.com/ropensci/rgbif/issues/392))

#### MINOR IMPROVEMENTS

- typo fix in the *geometry* section of the
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  manual file ([\#387](https://github.com/ropensci/rgbif/issues/387))
- vignettes fixes
  ([\#391](https://github.com/ropensci/rgbif/issues/391))

#### BUG FIXES

- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  tests needed preserve body bytes for vcr
  ([\#384](https://github.com/ropensci/rgbif/issues/384))
- fix to
  [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  and
  [`count_facet()`](https://docs.ropensci.org/rgbif/reference/count_facet.md):
  isGeoreferenced/georeferenced variable needed booleans converted to
  lowercase before being sent to GBIF
  ([\#385](https://github.com/ropensci/rgbif/issues/385))
  ([\#386](https://github.com/ropensci/rgbif/issues/386))

## rgbif 1.4.0

CRAN release: 2019-10-30

#### NEW FEATURES

- gains new function
  [`mvt_fetch()`](https://docs.ropensci.org/rgbif/reference/mvt_fetch.md)
  for fetching Map Vector Tiles (MVT). mvt used to be an option in
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md),
  but we only returned raw bytes for that option. With
  [`mvt_fetch()`](https://docs.ropensci.org/rgbif/reference/mvt_fetch.md)
  we now leverage the `protolite` package, which parses MVT files, to
  give back an sf object
  ([\#373](https://github.com/ropensci/rgbif/issues/373)) thanks to
  [@jeroen](https://github.com/jeroen) for the protolite work to make
  this work
- associated with above,
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  loses the `format = ".mvt"` option; and thus now only returns a
  `RasterLayer`
- [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  and
  [`name_issues()`](https://docs.ropensci.org/rgbif/reference/name_issues.md)
  reworked. Both now use the same underlying internal logic, with
  occ_issues pulling metadata specfic to occurrence issues and
  name_issues pulling metadata specific to name issues. name_issues used
  to only be a data.frame of name issues, but can now be used similarly
  to occ_issues; you can pass the output of
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  to name_issues to filter/parse name results by their associated name
  issues. Associated with this, new function `gbif_issues_lookup` can be
  used to lookup either occurrence or name issues by their full name or
  code ([\#363](https://github.com/ropensci/rgbif/issues/363))
  ([\#364](https://github.com/ropensci/rgbif/issues/364))

#### MINOR IMPROVEMENTS

- fix examples and tests that had WKT in the wrong winding order
  ([\#361](https://github.com/ropensci/rgbif/issues/361))
- parsing GBIF issues in the output of
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  wasn’t working ([\#328](https://github.com/ropensci/rgbif/issues/328))
  ([\#363](https://github.com/ropensci/rgbif/issues/363))
  ([\#364](https://github.com/ropensci/rgbif/issues/364))
- [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  gains an additional parameters `issue` for filtering name results by
  name issues ([\#335](https://github.com/ropensci/rgbif/issues/335))
  ([\#363](https://github.com/ropensci/rgbif/issues/363))
  ([\#364](https://github.com/ropensci/rgbif/issues/364))
- fixed definitions of `x`, `y`, `z` parameters in
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  manual file ([\#375](https://github.com/ropensci/rgbif/issues/375))
- added examples to
  [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  manual file for accessing many citations
  ([\#379](https://github.com/ropensci/rgbif/issues/379))
- fixed a test for
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  ([\#365](https://github.com/ropensci/rgbif/issues/365))
- `name_*` function outpus have changed, so be aware if you’re using
  those functions

#### BUG FIXES

- fixed issue with
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md):
  when srs was `EPSG:3857`, the extent we set was incorrectly set as
  `raster::extent(-180, 180, -85.1, 85.1)`. Now the extent is
  `raster::extent(-20037508, 20037508, -20037508, 20037508`
  ([\#366](https://github.com/ropensci/rgbif/issues/366))
  ([\#367](https://github.com/ropensci/rgbif/issues/367)) thanks
  [@dmcglinn](https://github.com/dmcglinn) for reporting and
  [@mdsumner](https://github.com/mdsumner) for fixing!
- fix for Windows platforms for
  [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  for `occ_download_get` objects. we weren’t correctly creating the path
  to a file on windows
  ([\#359](https://github.com/ropensci/rgbif/issues/359))
- fix to `print.gbif_data`
  ([\#370](https://github.com/ropensci/rgbif/issues/370))
  ([\#371](https://github.com/ropensci/rgbif/issues/371))
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  was erroring with a useless error when users try to use the fxn with
  the same parameter input types as `occ_search`/`occ_data`; when this
  happens now there is a useful error message
  ([\#381](https://github.com/ropensci/rgbif/issues/381))
- fix to
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md):
  when `type = "in"` was used, we weren’t creating the JSON correctly,
  fixed now ([\#362](https://github.com/ropensci/rgbif/issues/362))

## rgbif 1.3.0

CRAN release: 2019-05-08

#### NEW FEATURES

- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  and
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  gain a new parameter `format` for specifying the type of download.
  options are DWCA (default), SIMPLE_CSV, or SPECIES_LIST. SIMPLE_CSV
  and SPECIES_LIST are csv formats, while DWCA is the darwin core format
  ([\#352](https://github.com/ropensci/rgbif/issues/352))
- now throughout the package you can pass `NA` in addition to `NULL` for
  a missing parameter - both are removed before being sent to GBIF
  ([\#351](https://github.com/ropensci/rgbif/issues/351))

#### MINOR IMPROVEMENTS

- replace
  [`tibble::as_data_frame`](https://tibble.tidyverse.org/reference/deprecated.html)/[`tibble::data_frame`](https://tibble.tidyverse.org/reference/deprecated.html)
  with
  [`tibble::as_tibble`](https://tibble.tidyverse.org/reference/as_tibble.html)
  ([\#350](https://github.com/ropensci/rgbif/issues/350))
- `key` and `gbifID` in the output of `occ_data`/`occ_search`/`occ_get`
  have been changed so that both are character class (strings) to match
  how GBIF encodes them
  ([\#349](https://github.com/ropensci/rgbif/issues/349))
- fix some test fixtures to use preserve exact bytes so that cran checks
  on debian clang devel don’t fail
  ([\#355](https://github.com/ropensci/rgbif/issues/355))

#### BUG FIXES

- fix to `occ_download`: fail with useful message when user does not
  pass in queries as character class
  ([\#347](https://github.com/ropensci/rgbif/issues/347))
- fix to `occ_download`: fail with useful message now when
  user/pwd/email not found or given
  ([\#348](https://github.com/ropensci/rgbif/issues/348))

## rgbif 1.2.0

CRAN release: 2019-02-26

#### NEW FEATURES

- pkgdown documentation site
  ([\#336](https://github.com/ropensci/rgbif/issues/336))
  ([\#337](https://github.com/ropensci/rgbif/issues/337)) all work done
  by [@peterdesmet](https://github.com/peterdesmet)
- package gains hex logo
  ([\#331](https://github.com/ropensci/rgbif/issues/331))
  ([\#332](https://github.com/ropensci/rgbif/issues/332)) thanks
  [@peterdesmet](https://github.com/peterdesmet)
- big change to
  [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  function: the Google Maps API requires a form of payment up front, and
  so we’ve decided to move away from the service.
  [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  now uses the Geonames service <https://www.geonames.org/>; it does
  require you to register to get a username, but its a free service.
  Geonames has a few different data models for elevation and can be
  chosen in the `elevation_model` parameter
  ([\#344](https://github.com/ropensci/rgbif/issues/344))
  ([\#345](https://github.com/ropensci/rgbif/issues/345))
- biggish change to
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)/[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  output: the data.frame in the `data` slot now always has the first
  column as the occurrence key (`key`), and the second column is now the
  scientific name (`scientificName`). the previously used `name` column
  still exists in the data.frame, so as not to break any user code, but
  is simply a duplicate of the `scientificName` column. in a future
  version of this package the `name` column will be dropped
  ([\#329](https://github.com/ropensci/rgbif/issues/329))

#### MINOR IMPROVEMENTS

- README gains full list of code contributors and any folks involved in
  github issues ([\#339](https://github.com/ropensci/rgbif/issues/339))
  ([\#343](https://github.com/ropensci/rgbif/issues/343)) thanks
  [@peterdesmet](https://github.com/peterdesmet)
- update pkg citation, include all authors
  ([\#338](https://github.com/ropensci/rgbif/issues/338))
- added more to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)/[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)/[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  documentation on WKT (well-known text) with respect to winding order.
  GBIF requires counter-clockwise winding order; if you submit clockwise
  winding order WKT to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  or
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  you should get data back but the WKT is treated as an exclusion, so
  returns data outside of that shape instead of within it; if you submit
  clockwise winding order WKT to
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  you will get no data back
  ([\#340](https://github.com/ropensci/rgbif/issues/340))

#### BUG FIXES

- fix bug in
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
  was failing in certain cases because of some bad code in an internal
  function `catch_err()`
  ([\#333](https://github.com/ropensci/rgbif/issues/333))
- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  was not returning user name and email in it’s print method
  ([\#334](https://github.com/ropensci/rgbif/issues/334))
- [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  was failing with
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  or
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  input when `type="many"` (i.e., when \> 1 thing was passed in)
  ([\#341](https://github.com/ropensci/rgbif/issues/341))

## rgbif 1.1.0

CRAN release: 2018-10-19

#### NEW FEATURES

- tests that make HTTP requests are now cached via the `vcr` package so
  do not require an internet connection
  ([\#306](https://github.com/ropensci/rgbif/issues/306))
  ([\#327](https://github.com/ropensci/rgbif/issues/327))
- added name usage issues (similar to occurrence issues) data. in part
  fixes
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  problem, more work coming to allow users to use the name issues data
  like we allow for occurrence issues through
  [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  ([\#324](https://github.com/ropensci/rgbif/issues/324))

#### MINOR IMPROVEMENTS

- [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  changes following changes in GBIF maps API: new parameters `taxonKey`,
  `datasetkey`, `country`, `publishingOrg`, `publishingCountry` and
  removed parameters `search` and `id`; note that this changes how
  queries work with this function
  ([\#319](https://github.com/ropensci/rgbif/issues/319))
- added note to
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  docs that `style` parameter does not necessarily use the style you
  give it. not sure why
  ([\#302](https://github.com/ropensci/rgbif/issues/302))
- fixed messaging in
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  to report an accurate number of jobs being processed; before we were
  just saying “kicking off first 3 requests” even if there were only 1
  or 2 ([\#312](https://github.com/ropensci/rgbif/issues/312))

#### BUG FIXES

- fix to
  [`occ_get()`](https://docs.ropensci.org/rgbif/reference/occ_get.md)
  when `verbatim=TRUE`
  ([\#318](https://github.com/ropensci/rgbif/issues/318))
- [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  function now fails better. when the API key was invalid the function
  did not give an informative message; now it does
  ([\#322](https://github.com/ropensci/rgbif/issues/322))

## rgbif 1.0.2

CRAN release: 2018-07-06

#### MINOR IMPROVEMENTS

- significant change to
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md):
  sleep time between successive calls to check on the status of download
  requests is now 10 seconds or greater. This shouldn’t slow down your
  use of
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  much because most requests should take more than the 10 seconds to be
  prepared ([\#313](https://github.com/ropensci/rgbif/issues/313))
- add tests for download queue method
  ([\#315](https://github.com/ropensci/rgbif/issues/315))
- explicitly `@importFrom` fxns used from `lazyeval` package to avoid
  check note ([\#316](https://github.com/ropensci/rgbif/issues/316))
- remove `reshape2` and `maps` packages from Suggests
  ([\#317](https://github.com/ropensci/rgbif/issues/317))

#### BUG FIXES

- fix bug in
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md):
  we were screwing up parsing of issues column when single taxon keys
  passed in ([\#314](https://github.com/ropensci/rgbif/issues/314))

## rgbif 1.0.0

CRAN release: 2018-07-03

#### NEW FEATURES

- [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  now works with download data and arbitrary data.frame’s
  ([\#193](https://github.com/ropensci/rgbif/issues/193))
- New downloads queueing tools: gains functions
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  for preparing a download request without executing it, and
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  for kicking off many download jobs while respecting GBIF’s downloads
  rate limits. See also internal R6 classes for dealing with queuing:
  `DownReq`, `GifQueue`. See
  [`?occ_download_queue`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  to get started ([\#266](https://github.com/ropensci/rgbif/issues/266))
  ([\#305](https://github.com/ropensci/rgbif/issues/305))
  ([\#311](https://github.com/ropensci/rgbif/issues/311))
- New function
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  working with the GBIF maps API <https://www.gbif.org/developer/maps>.
  See
  [`?map_fetch`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  to get started ([\#238](https://github.com/ropensci/rgbif/issues/238))
  ([\#269](https://github.com/ropensci/rgbif/issues/269))
  ([\#284](https://github.com/ropensci/rgbif/issues/284)) thanks to
  [@JanLauGe](https://github.com/JanLauGe) for the work on this
- [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  gains `origin` parameter
  ([\#288](https://github.com/ropensci/rgbif/issues/288))
  ([\#293](https://github.com/ropensci/rgbif/issues/293)) thanks
  [@peterdesmet](https://github.com/peterdesmet) and
  [@damianooldoni](https://github.com/damianooldoni)
- [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  and
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  gain internal paging - just as
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)/[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  have ([\#291](https://github.com/ropensci/rgbif/issues/291)) (see also
  [\#281](https://github.com/ropensci/rgbif/issues/281)) thanks
  [@damianooldoni](https://github.com/damianooldoni)
- new import `lazyeval`, and new suggests `png` and `raster`
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)/[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  gain parameter `skip_validate` (boolean) to skip or not stkip WKT
  validation by the `wicket` package

#### MINOR IMPROVEMENTS

- removed warnings about parameters that were removed in previous
  versions of the package
  ([\#189](https://github.com/ropensci/rgbif/issues/189))
- add citation file
  ([\#189](https://github.com/ropensci/rgbif/issues/189))
- updated
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  to check params that now only allow 1 value: name, language,
  datasetKey, rank
  ([\#287](https://github.com/ropensci/rgbif/issues/287))
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  loses `nubKey`, `catalogNumber`, and `hostCountry` as those parameters
  are no longer accepted by GBIF

#### BUG FIXES

- fixed bug in
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md),
  was screwing something up internally
  ([\#286](https://github.com/ropensci/rgbif/issues/286))
- fixed bug in
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md):
  curl options weren’t being passed through
  ([\#297](https://github.com/ropensci/rgbif/issues/297))
- fixed geometry usage in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)/[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md) -
  skipping the wicket validation and constructing WKT by hand from
  bounding box (if bounding box given) - the validation that wicket does
  isn’t what GBIF wants
  ([\#303](https://github.com/ropensci/rgbif/issues/303))
- add `fill` parameter to
  [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  to pass on to `fill` in
  [`data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html),
  and set `fill=TRUE` as default.
  ([\#292](https://github.com/ropensci/rgbif/issues/292))
- better failure for
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  ([\#300](https://github.com/ropensci/rgbif/issues/300))
- fix bug in
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  in which a single `taxonKey` passed in was failing
  ([\#283](https://github.com/ropensci/rgbif/issues/283))
- [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  was ignoring `datasetKey` and `uuid` parameters
  ([\#290](https://github.com/ropensci/rgbif/issues/290))

#### DEFUNCT AND DEPRECATED

- [`gbifmap()`](https://docs.ropensci.org/rgbif/reference/gbifmap-defunct.md)
  has been removed, see the package `mapr` for similar functionality and
  [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  in this package to use the GBIF map API
  ([\#298](https://github.com/ropensci/rgbif/issues/298))

## rgbif 0.9.9

CRAN release: 2017-11-12

#### NEW FEATURES

- Gains new functions `occ_download_datasets` and
  `occ_download_dataset_activity` to list datasets for a download, and
  list the downloads activity of a dataset
  ([\#275](https://github.com/ropensci/rgbif/issues/275))
  ([\#276](https://github.com/ropensci/rgbif/issues/276))
- Gains a new vignette covering working with GBIF downloads in `rgbif`
  ([\#262](https://github.com/ropensci/rgbif/issues/262))

#### MINOR IMPROVEMENTS

- Guidance added to docs for downloads functions on length of the
  request body ([\#263](https://github.com/ropensci/rgbif/issues/263))
- Changed authentication details (user name, password, email) for
  downloads to allow any of the options: pass in as arguments, store as
  R options, store as environment variables
  ([\#187](https://github.com/ropensci/rgbif/issues/187))
- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  function gains an S3 method for passing the output of
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  to it. In addition, for downloads
  [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  now returns a citation for the entire download (including) its DOI, in
  addition to citations for each dataset
  ([\#274](https://github.com/ropensci/rgbif/issues/274)) thanks
  [@dnoesgaard](https://github.com/dnoesgaard)

#### BUG FIXES

- Fix documentation bug in
  [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md):
  `georeferenced` had a misleading description of what the value `FALSE`
  did ([\#265](https://github.com/ropensci/rgbif/issues/265))
- Fixed bug in
  [`gbifmap()`](https://docs.ropensci.org/rgbif/reference/gbifmap-defunct.md) -
  was failing in some cases - better error handlingn now
  ([\#271](https://github.com/ropensci/rgbif/issues/271)) thanks
  [@TomaszSuchan](https://github.com/TomaszSuchan)
- Fixed
  [`occ_download_cancel_staged()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md):
  it wasn’t passing on authentication parameters correctly
  ([\#280](https://github.com/ropensci/rgbif/issues/280))

## rgbif 0.9.8

CRAN release: 2017-04-18

#### NEW FEATURES

- The GBIF API supports passing in many instances of the same parameter
  for some parameters on some routes. Previously we didn’t support this
  feature, but now we do. See the `?many-values` manual file for
  details. added docs to individual functions that support this, and
  added additional tests
  ([\#200](https://github.com/ropensci/rgbif/issues/200))
  ([\#260](https://github.com/ropensci/rgbif/issues/260))
  ([\#261](https://github.com/ropensci/rgbif/issues/261))
- We’ve removed `V8` dependency and replaced with C++ based WKT parser
  package `wicket`. We still use `rgeos` for some WKT parsing. rgbif
  functions that use wicket: `gbif_bbox2wkt`, `gbif_wkt2bbox`,
  `check_wkt` ([\#243](https://github.com/ropensci/rgbif/issues/243))
- `httr` replaced with `crul` for HTTP reqeusts. As part of this change,
  the `...` parameter was replaced in most functions by `curlopts` which
  expects a list. Some functions require a `...` parameter for facet
  inputs, so `...` is retained with the addition of `curltops`
  parameter. A result of this change is that whereas in the past
  parameters that were not defined in a function that also had a `...`
  parameter would essentially silently ignore that undefined parameter,
  but with functions where `...` was removed a misspelled or undefined
  parameter will cause an error with message
  ([\#256](https://github.com/ropensci/rgbif/issues/256))

#### MINOR IMPROVEMENTS

- moved to markdown docs
  ([\#258](https://github.com/ropensci/rgbif/issues/258))
- namespacing calls to base R pkgs instead of importing them

#### BUG FIXES

- Fixed problem in
  [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  to allow import of csv type download in addition to darwin core
  archive. additional change to `occ_download_get` to add `format`
  attribute stating which format
  ([\#246](https://github.com/ropensci/rgbif/issues/246))
- fix to `occ_download_import` adding `fill=TRUE` to the
  [`data.table::fread`](https://rdrr.io/pkg/data.table/man/fread.html)
  call ([\#257](https://github.com/ropensci/rgbif/issues/257))

## rgbif 0.9.7

CRAN release: 2017-01-21

#### NEW FEATURES

- `occ_dowload` gains new parameter `body` to allow users to pass in
  JSON or a list for the query instead of passing in statements to
  `...`. See examples in `?occ_dowload`.

#### MINOR IMPROVEMENTS

- Now using `tibble` for compact data.frame output for
  `occ_download_import` instead of bespoke internal solution
  ([\#240](https://github.com/ropensci/rgbif/issues/240))
- Moved all GBIF API requests to use `https` instead of `http`
  ([\#244](https://github.com/ropensci/rgbif/issues/244))
- Improved print method for `occ_download_meta`

#### BUG FIXES

- Fix to `occ_download` to structure query correctly when `type=within`
  and `geometry` used because the structure is slightly different than
  when not using `geometry`
  ([\#242](https://github.com/ropensci/rgbif/issues/242))
- Fixed `occ_download` to allow `OR` queries for many values of a
  parameter, e.g., `taxonKey=2475470,2480946` will be queried correctly
  now as essentially `taxonKey=2475470` or `taxonKey=2480946`
  ([\#245](https://github.com/ropensci/rgbif/issues/245))

## rgbif 0.9.6

CRAN release: 2016-12-06

#### BUG FIXES

- Fixed a bug in
  [`parsenames()`](https://docs.ropensci.org/rgbif/reference/parsenames.md)
  caused by some slots in the list being `NULL`
  ([\#237](https://github.com/ropensci/rgbif/issues/237))
- Fixed some failing tests:
  [`occ_facet()`](https://docs.ropensci.org/rgbif/reference/occ_facet.md)
  tests were failing due to changes in GBIF API
  ([\#239](https://github.com/ropensci/rgbif/issues/239))
- Fixes to
  [`gbif_oai_get_records()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  for slight changes in `oai` dependency pkg
  ([\#236](https://github.com/ropensci/rgbif/issues/236))

## rgbif 0.9.5

CRAN release: 2016-10-06

#### NEW FEATURES

- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now has faceted search. This feature is not in
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  as that function focuses on getting occurrence data quickly, so will
  not do get facet data. This means that a new slot is available in the
  output object from
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md),
  namely `facets`. Note that `rgbif` has had faceted search for the
  species search route
  ([`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md))
  and the registry search route
  ([`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md))
  for quite a while.
  ([\#215](https://github.com/ropensci/rgbif/issues/215))
- new function
  ([`occ_facet()`](https://docs.ropensci.org/rgbif/reference/occ_facet.md))
  to facilitate retrieving only facet data, so no occurrence data is
  retrieved. ([\#215](https://github.com/ropensci/rgbif/issues/215))
  ([\#229](https://github.com/ropensci/rgbif/issues/229))
- A suite of new parameters added to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  and
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  following addition the GBIF search API: `subgenusKey`, `repatriated`,
  `phylumKey`, `kingdomKey`, `classKey`, `orderKey`, `familyKey`,
  `genusKey`, `establishmentMeans`, `protocol`, `license`, `organismId`,
  `publishingOrg`, `stateProvince`, `waterBody`, `locality`
  ([\#216](https://github.com/ropensci/rgbif/issues/216))
  ([\#224](https://github.com/ropensci/rgbif/issues/224))
- New parameter `spellCheck` added to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  and
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  that if `TRUE` spell checks anything passed to the `search` parameter
  (same as `q` parameter on GBIF API; which is a full text search)
  ([\#227](https://github.com/ropensci/rgbif/issues/227))
- New function `occ_spellcheck` to spell check search terms, returns
  `TRUE` if no spelling problems, or a list with info on suggestions if
  not.
- Both
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  and
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  now have ability to support queries where `limit=0`, which for one
  should be possible and not fail as we did previously, and second, this
  makes it so that you can do faceted searches (See above) and not have
  to wait for occurrence records to be returned.
  ([\#222](https://github.com/ropensci/rgbif/issues/222))
- `MULTIPOLYGON` well known text features now supported in the GBIF API.
  Previously, you could not query `geometry` with more than one polygon
  (`POLYGON`), but now you can.
  ([\#222](https://github.com/ropensci/rgbif/issues/222))

#### MINOR IMPROVEMENTS

- Improved docs for
  [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md),
  especially for the set of allowed parameter options that the GBIF
  count API supports
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  gains new parameter `typeStatus` to indicate the specimen type status.
- When no results found, the `data` slot now returns `NULL` instead of a
  character string

#### BUG FIXES

- Fixes to
  [`gbif_photos()`](https://docs.ropensci.org/rgbif/reference/gbif_photos.md): 1)
  Mapbox URLs to their JS and CSS assets were out of date, and API key
  needed. 2) In RStudio, the `table` view was outputting errors due to
  serving files on `localhost:<port>` instead of simply opening the
  file; fixed now by checking platform and using simple open file
  command appropriate for the OS.
  ([\#228](https://github.com/ropensci/rgbif/issues/228))
  ([\#235](https://github.com/ropensci/rgbif/issues/235))

## rgbif 0.9.4

CRAN release: 2016-06-29

#### NEW FEATURES

- Now using `tibble` in most of the package when the output is a
  data.frame ([\#204](https://github.com/ropensci/rgbif/issues/204))
- New vignette *Taxonomic Names* for discussing some common names
  problems users may run into, and some strategies for dealing with
  taxonomic names when using GBIF
  ([\#208](https://github.com/ropensci/rgbif/issues/208))
  ([\#209](https://github.com/ropensci/rgbif/issues/209))

#### MINOR IMPROVEMENTS

- Replaced [`is()`](https://rdrr.io/r/methods/is.html) with
  [`inherits()`](https://rdrr.io/r/base/class.html), no longer importing
  [`methods()`](https://rdrr.io/r/utils/methods.html)
  ([\#219](https://github.com/ropensci/rgbif/issues/219))
- Improved docs for registry functions. Not all options were listed for
  the `data` parameter, now they are
  ([\#210](https://github.com/ropensci/rgbif/issues/210))
- Fixed documentation error in
  [`gbifmap()`](https://docs.ropensci.org/rgbif/reference/gbifmap-defunct.md)
  man file ([\#212](https://github.com/ropensci/rgbif/issues/212))
  thanks to [@rossmounce](https://github.com/rossmounce)

#### BUG FIXES

- Fixed bug in internal parser within
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
  in which strings to parse were not being parsed correctly if spaces
  weren’t in the right place, should be more robust now, and added tests
  ([\#217](https://github.com/ropensci/rgbif/issues/217)). Came from
  <https://discuss.ropensci.org/t/rgbif-using-geometry-in-occ-download/395>
- The parameter `type` was being silently ignored in a number of
  registry functions. fixed that.
  ([\#211](https://github.com/ropensci/rgbif/issues/211))

## rgbif 0.9.3

CRAN release: 2016-03-29

#### NEW FEATURES

- [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  and
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  gain ability to more flexibly deal with inputs to the `geometry`
  parameter. Previously, long WKT strings passed to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  or
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  would fail because URIs can only be so long. Another option is to use
  the download API (see
  [`?downloads`](https://docs.ropensci.org/rgbif/reference/downloads.md)).
  This version adds the ability to choose what to do with long WKT
  strings via the `geom_big` parameter: `asis` (same as previous
  version), `bbox` which detects if a WKT sting is likely too long, and
  creates a bounding box from the WKT string then once data is
  retrieved, clips the result to the original WKT string; `axe` uses the
  `geoaxe` package to chop up the input WKT polygon into many, with
  toggles in the new parameters `geom_size` and `geom_n`.
  ([\#197](https://github.com/ropensci/rgbif/issues/197))
  ([\#199](https://github.com/ropensci/rgbif/issues/199))
- As part of this change, when \>1 geometry value passed, or if
  `geom_big="axe"`, then named elements of the output get names `geom1`,
  `geom2`, `geom3`, etc. instead of the input WKT strings - this is
  because WKT strings can be very long, and make for very awkward named
  access to elements. The original WKT strings can still be accessed via
  `attr(result, "args")$geometry`

#### MINOR IMPROVEMENTS

- code tidying throughout the package

#### BUG FIXES

- Fix parsing bug in
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  function, see commit
  [e88cf01cc11cb238d44222346eaeff001c0c637e](https://github.com/ropensci/rgbif/commit/e88cf01cc11cb238d44222346eaeff001c0c637e)
- Fix to tests to use new `testthat` fxn names, e.g., `expect_gt()`
  instead of `expect_more_than()`
- Fix to
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  to parse error correctly when empty body passed from GBIF
  ([\#202](https://github.com/ropensci/rgbif/issues/202))

## rgbif 0.9.2

CRAN release: 2016-02-02

#### NEW FEATURES

- New function
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md) -
  its primary purpose to perform faster data requests. Whereas
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  gives you lots of data, including taxonomic hierarchies and media
  records,
  [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  only gives occurrence data.
  ([\#190](https://github.com/ropensci/rgbif/issues/190))

#### MINOR IMPROVEMENTS

- Replaced `XML` with `xml2`
  ([\#192](https://github.com/ropensci/rgbif/issues/192))
- Speed ups to the following functions due to use of
  [`data.table::rbindlist()`](https://rdrr.io/pkg/data.table/man/rbindlist.html)
  for fast list to data.frame coercion:
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md),
  [`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md),
  [`name_suggest()`](https://docs.ropensci.org/rgbif/reference/name_suggest.md),
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md),
  and
  [`parsenames()`](https://docs.ropensci.org/rgbif/reference/parsenames.md)
  ([\#191](https://github.com/ropensci/rgbif/issues/191))
- Changes to `httr` usage to comply with changes in `httr >= v1.1.0`:
  now setting encoding explicitly to `UTF-8` and parsing all data
  manually, using the internal function
  `function(x) content(x, "text", encoding = "UTF-8")`
  ([\#195](https://github.com/ropensci/rgbif/issues/195))

#### BUG FIXES

- Fix to internal function `move_col()` to not fail on fields that don’t
  exist. Was failing sometimes when no latitude or longitude columns
  were returned. ([\#196](https://github.com/ropensci/rgbif/issues/196))

## rgbif 0.9.0

CRAN release: 2015-11-25

#### NEW FEATURES

- New set of functions (`gbif_oai_*()`) for working with GBIF registry
  OAI-PMH service. Now importing `oai` package to make working with
  GBIF’s OAI-PMH service easier
  ([\#183](https://github.com/ropensci/rgbif/issues/183))
- Added code of conduct
  ([\#180](https://github.com/ropensci/rgbif/issues/180))
- Now sending user-agent header with all requests from this package to
  GBIF’s servers indicating what version of rgbif and that it’s an
  ropensci package. Looks like
  `r-curl/0.9.4 httr/1.0.0 rOpenSci(rgbif/0.9.0)`, with whatever
  versions of each package you’re using. We also pass a user-agent
  string with the header `X-USER-AGENT` in case the `useragent` header
  gets stripped somewhere along the line
  ([\#185](https://github.com/ropensci/rgbif/issues/185))
- New function
  [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  helps get citations for datasets eith using the occurrence search API
  via
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  or the downloads API via `occ_downlad()`
  ([\#178](https://github.com/ropensci/rgbif/issues/178))
  ([\#179](https://github.com/ropensci/rgbif/issues/179))

#### MINOR IMPROVEMENTS

- Using `importFrom` instead of `import` in all cases now.
- Parameter `collectorName` changed to `recordedBy`
  ([\#184](https://github.com/ropensci/rgbif/issues/184))

#### BUG FIXES

- Fix to
  [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  print method to handle 1 or more predicate results
  ([\#186](https://github.com/ropensci/rgbif/issues/186))
- Fix to
  [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  to work with `return=data` and `return=all`
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  output ([\#188](https://github.com/ropensci/rgbif/issues/188))

## rgbif 0.8.9

CRAN release: 2015-10-07

#### MINOR IMPROVEMENTS

- Updated `terraformer.js` javascript code included in the package along
  with an update in that codebase
  ([\#156](https://github.com/ropensci/rgbif/issues/156))
- The `email` parameter now `NULL` by default in the function
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md),
  so that if not provided or not set in options, then function fails.
  ([\#173](https://github.com/ropensci/rgbif/issues/173))
- Additional explanation added to the
  [`?downloads`](https://docs.ropensci.org/rgbif/reference/downloads.md)
  help file.
- Added internal checks to
  [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  to check for coordinates that are impossible (e.g., latitude \> 90),
  not complete (e.g., lat given, long not given), or points at `0,0`
  (just warns, doesn’t stop).
  ([\#176](https://github.com/ropensci/rgbif/issues/176)) thanks
  [@luisDVA](https://github.com/luisDVA)
- General code tidying across package

#### BUG FIXES

- A route changed for getting images for a taxon within the `/species`
  route, fix to function
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  ([\#174](https://github.com/ropensci/rgbif/issues/174))
- Fix to
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  to remove a block of code to do synonym checking. This block of code
  was used if the parameter `scientificName` was passed, and checked if
  the name given was a synonym; if yes, we used the accepted name
  according to the GBIF backbone taxonomy; if no, we proceeded with the
  name given by the user. We removed the block of code because the GBIF
  API now essentially does this behind the scenes server side. See
  <https://github.com/gbif/gbif-api> for examples.
  ([\#175](https://github.com/ropensci/rgbif/issues/175))

## rgbif 0.8.8

CRAN release: 2015-07-24

#### MINOR IMPROVEMENTS

- Additional tests added for
  [`gbif_photos()`](https://docs.ropensci.org/rgbif/reference/gbif_photos.md)
  and
  [`gbif_names()`](https://docs.ropensci.org/rgbif/reference/gbif_names.md)
  ([\#170](https://github.com/ropensci/rgbif/issues/170))

#### BUG FIXES

- Fixed a few tests that were not passing on CRAN.

## rgbif 0.8.6

CRAN release: 2015-07-03

#### NEW FEATURES

- New set of functions with names `occ_download*()` for working with the
  GBIF download API. This is the same service as using the GBIF website,
  but via an API. See
  [`?downloads`](https://docs.ropensci.org/rgbif/reference/downloads.md).
  ([\#154](https://github.com/ropensci/rgbif/issues/154))
  ([\#167](https://github.com/ropensci/rgbif/issues/167))

#### MINOR IMPROVEMENTS

- Explicitly import non-base R pkg functions, so importing from `utils`,
  `methods`, and `stats`
  ([\#166](https://github.com/ropensci/rgbif/issues/166))

#### BUG FIXES

- Fixed problem with `httr` `v1` where empty list not allowed to pass to
  the `query` parameter in `GET`
  ([\#163](https://github.com/ropensci/rgbif/issues/163))

## rgbif 0.8.4

CRAN release: 2015-06-08

#### NEW FEATURES

- New functions for the `/enumerations` GBIF API route:
  [`enumeration()`](https://docs.ropensci.org/rgbif/reference/enumeration.md)
  and
  [`enumeration_country()`](https://docs.ropensci.org/rgbif/reference/enumeration.md).
  Many parts of the GBIF API make use of enumerations, i.e. controlled
  vocabularies for specific topics - and are available via these
  functions. ([\#152](https://github.com/ropensci/rgbif/issues/152))

#### IMPROVEMENTS

- [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  now requires an API key
  ([\#148](https://github.com/ropensci/rgbif/issues/148))
- The `V8` package an Import now, used to do WKT read/create with use of
  the Javascript library Terraformer (<http://terraformer.io/>).
  Replaces packages `sp` and `rgeos`, which are no longer imported
  ([\#155](https://github.com/ropensci/rgbif/issues/155))
- Changed
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  parameter `spatialIssues` to `hasGeospatialIssues`
  ([\#151](https://github.com/ropensci/rgbif/issues/151))
- Added note to docs about difference between `/search` and `/count`
  services, and how they work.
  ([\#150](https://github.com/ropensci/rgbif/issues/150))
- Added tests for habitat parameter in
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  ([\#149](https://github.com/ropensci/rgbif/issues/149))
- Dropped `plyr` from Imports
  ([\#159](https://github.com/ropensci/rgbif/issues/159))
- Dropped `stringr` from Imports
  ([\#160](https://github.com/ropensci/rgbif/issues/160))
- Dropped `maps` and `grid` packages from Imports
  ([\#161](https://github.com/ropensci/rgbif/issues/161))

#### BUG FIXES

- Looping over records with `limit` and `start` parameters was in some
  cases resulting in duplicate records returned. Problem fixed.
  ([\#157](https://github.com/ropensci/rgbif/issues/157))

## rgbif 0.8.0

CRAN release: 2015-03-09

#### IMPROVEMENTS

- All example moved to `\dontrun`
  ([\#139](https://github.com/ropensci/rgbif/issues/139))
- README fixes for html
  ([\#141](https://github.com/ropensci/rgbif/issues/141))
- Fixed documentation in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  to give correct values for default and max limit and start parameters
  ([\#145](https://github.com/ropensci/rgbif/issues/145))
- Changed internal `GET` helper function to properly pass on error
  message ([\#144](https://github.com/ropensci/rgbif/issues/144))
- Replaced `assertthat::assert_that()` with
  [`stopifnot()`](https://rdrr.io/r/base/stopifnot.html) to have one
  less dependency
  ([\#134](https://github.com/ropensci/rgbif/issues/134))
- Fixed
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  to allow ability to query by only publishingCountry, that is, with no
  other parameters if desired
  ([\#137](https://github.com/ropensci/rgbif/issues/137))

#### BUG FIXES

- Fixed bug in internal `GET()` helper function to just pass `NULL` to
  the `query` parameter when the list of length 0 passed, since it
  caused requests to fail in some cases.
- Fix to
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  to force a logical entry for certain parameters - before this fix if
  the correct logical param was not passed, the GBIF API went with its
  default parameter
  ([\#135](https://github.com/ropensci/rgbif/issues/135))
- Fixed bug in
  [`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
  due to change in `namelkupparser()` helper function - fixes parsing
  for verbose output
  ([\#136](https://github.com/ropensci/rgbif/issues/136))
- Fixed some broken URLs in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  documentation ([\#140](https://github.com/ropensci/rgbif/issues/140))

## rgbif 0.7.7

CRAN release: 2014-11-07

#### NEW FEATURES

- New function
  [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  to subset data from
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  based on GBIF issues. (#)
  ([\#122](https://github.com/ropensci/rgbif/issues/122))
- Related to the last bullet, GBIF issues now are returned by default in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  results, and are intentionally moved to the beginning of the column
  order of the data to be more obvious.
  ([\#102](https://github.com/ropensci/rgbif/issues/102))
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now returns all data fields by default. The default setting for the
  `fields` parameter is `all` - but can be changed. See
  [`?occ_search`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
- New function
  [`gbif_names()`](https://docs.ropensci.org/rgbif/reference/gbif_names.md)
  to view highlighted terms in name results from a call to
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md).
  ([\#114](https://github.com/ropensci/rgbif/issues/114))
- New functions: `occ_issues_lookup()` to lookup GBIF issues based on
  code name or full issue name, and
  [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md)
  to print the entire issues table.

#### IMPROVEMENTS

- Completely replaced `RCurl` with `httr`
- Completely replaced `RJSONIO` with `jsonlite`. Should see slight
  performance in JSON parsing with `jsonlite`.
- Default number of records in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now 500; was 25.
  ([\#113](https://github.com/ropensci/rgbif/issues/113))
- Vignette for old version of GBIF API removed.
- New vignette for cleaning data via GBIF issues added.
  ([\#132](https://github.com/ropensci/rgbif/issues/132))
- Functions for working with old GBIF API removed, now defunct.
  ([\#116](https://github.com/ropensci/rgbif/issues/116))
- Now better parsing for some functions
  ([`organizations()`](https://docs.ropensci.org/rgbif/reference/organizations.md),
  [`datasets()`](https://docs.ropensci.org/rgbif/reference/datasets.md),
  [`networks()`](https://docs.ropensci.org/rgbif/reference/networks.md),
  [`nodes()`](https://docs.ropensci.org/rgbif/reference/nodes.md),
  [`installations()`](https://docs.ropensci.org/rgbif/reference/installations.md))
  to data.frames when possible.
  ([\#117](https://github.com/ropensci/rgbif/issues/117))
- Added further help to warn users when searching on ranges in latitude
  or longitude in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  ([\#123](https://github.com/ropensci/rgbif/issues/123))
- `callopts` parameter changed to `...` throughout all functions. Now
  pass on options to `httr` as named lists or functions.
  ([\#130](https://github.com/ropensci/rgbif/issues/130))
- Beware that GBIF data is becoming Darwin Core compliant - so many
  parameters throughout this package have changed from sentence_case to
  camelCase.
- [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  and
  [`dataset_suggest()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  gain new parameter `publishingOrg`
- Default for `limit` parameter changed to 100 for dataset functions:
  [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md),
  [`dataset_suggest()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md),
  and
  [`datasets()`](https://docs.ropensci.org/rgbif/reference/datasets.md).
- Default for `limit` parameter changed to 100 for registry functions:
  [`installations()`](https://docs.ropensci.org/rgbif/reference/installations.md),
  [`networks()`](https://docs.ropensci.org/rgbif/reference/networks.md),
  `organizations`, and
  [`nodes()`](https://docs.ropensci.org/rgbif/reference/nodes.md).
- Parameter changes in
  [`networks()`](https://docs.ropensci.org/rgbif/reference/networks.md):
  `name`, `code`, `modifiedsince`, `startindex`, and `maxresults` gone;
  new parameters `query`, `identifier`, `identifierType`, `limit`, and
  `start`
- Parameter changes in
  [`nodes()`](https://docs.ropensci.org/rgbif/reference/nodes.md): new
  parameters `identifier`, `identifierType`, `limit`, and `start`

#### BUG FIXES

- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  failed sometimes on species that were not found. Fixed.
  ([\#112](https://github.com/ropensci/rgbif/issues/112))
- Added better handling of some server errors to pass on to user.
  ([\#115](https://github.com/ropensci/rgbif/issues/115))
  ([\#118](https://github.com/ropensci/rgbif/issues/118))
- Fixed incorrect parsing for some cases in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  ([\#119](https://github.com/ropensci/rgbif/issues/119))
- Fixed bad parsing on output from
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  ([\#120](https://github.com/ropensci/rgbif/issues/120))
- Fixed single map option in
  [`gbif_photos()`](https://docs.ropensci.org/rgbif/reference/gbif_photos.md)
  that caused map with no data.
  ([\#121](https://github.com/ropensci/rgbif/issues/121))
- Fixed some parameter names in `name_()` functions according to changes
  in the GBIF API spec, and fixed documentation to align with GBIF API
  changes, and added note about maximum limit.
  ([\#124](https://github.com/ropensci/rgbif/issues/124))
  ([\#127](https://github.com/ropensci/rgbif/issues/127))
  ([\#129](https://github.com/ropensci/rgbif/issues/129)) Thanks to
  [@willgearty](https://github.com/willgearty) !
- Fixed internals of
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  so that user can pass in multiple values to the `issue` parameter.
  ([\#107](https://github.com/ropensci/rgbif/issues/107))
- Fixed URL to tutorial on ropensci website
  ([\#105](https://github.com/ropensci/rgbif/issues/105)) Thanks
  [@fxi](https://github.com/fxi) !

## rgbif 0.7.0

CRAN release: 2014-07-31

#### NEW FEATURES

- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now has a `dplyr` like summary output when `return='all'`. See
  [`?occ_search`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  for examples. You can still easily access all data, by indexing to
  `meta`, `hierarchy`, `data`, or `media` via e.g., `$data`, `['data']`,
  or `[['data']]`. ([\#95](https://github.com/ropensci/rgbif/issues/95))
- Media now returned from the GBIF API. Thus, in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md),
  we now return a media slot in the output list by default.
- New function
  [`gbif_photos()`](https://docs.ropensci.org/rgbif/reference/gbif_photos.md)
  to view media files (photos in the wild or of museum specimens). Two
  options are available, `which='map'` creates a single map which
  presents the image when the user clicks on the point, and
  `which='table'` in which a table has one row for each image,
  presenting the image and an interactive map with the single point.
  ([\#88](https://github.com/ropensci/rgbif/issues/88))
- Two new packages are imported: `sp` and `whisker`

#### IMPROVEMENTS

- GBIF updated their API, now at v1. URL endpoints in `rgbif` changed
  accordingly. ([\#92](https://github.com/ropensci/rgbif/issues/92))
- GBIF switched to using 2-letter country codes. Take note.
  ([\#90](https://github.com/ropensci/rgbif/issues/90))
- GBIF switched all parameters to `camelCase` from `under_score` style -
  changed accordingly in `rgbif`.
- Using package custom version of
  [`plyr::compact()`](https://rdrr.io/pkg/plyr/man/compact.html) instead
  of importing from `plyr`.
- In
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  removed `facet_only` parameter as it doesn’t do anything - use
  `limit=0` instead. Further, added two new slots of output: `hierarchy`
  and `names` (for common/vernacular names)
  ([\#96](https://github.com/ropensci/rgbif/issues/96)). The output can
  be determined by user via the `return` parameter.
- In
  [`name_suggest()`](https://docs.ropensci.org/rgbif/reference/name_suggest.md),
  if the field `higherClassificationMap` is selected to be returned via
  the `fields` parameter, a list is returned with a data frame, and a
  list of the hierarchies separately. If `higherClassificationMap` is
  not selected, only a data frame is returned.
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  gains new parameters `mediatype` and `issue`
  ([\#93](https://github.com/ropensci/rgbif/issues/93)), with detailed
  list of possible options for the `issue` parameter. Gains new examples
  for searching for images, examples of calls that will throw errors.
- Updated the vignette.

#### BUG FIXES

- Added better error message to
  [`check_wkt()`](https://docs.ropensci.org/rgbif/reference/check_wkt.md).
- `facet_only` parameter removed from
  [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  function as it doesn’t do anything - use `limit=0` instead.
- Fixed some examples that didn’t work correctly.

## rgbif 0.6.3

#### IMPROVEMENTS

- Added functions
  [`gbif_bbox2wkt()`](https://docs.ropensci.org/rgbif/reference/gbif_bbox2wkt.md)
  and
  [`gbif_wkt2bbox()`](https://docs.ropensci.org/rgbif/reference/gbif_bbox2wkt.md)
  to convert a bounding box to wkt and a wkt object to a bounding box,
  respectively. Copied from the `spocc` package. Prefixes to fxn names
  will avoid conflicts.
- Now spitting out more informative error messages when WKT strings
  passed in are not properly formed, either from `rgeos::readWKT` or
  from the returned response from GBIF.

## rgbif 0.6.2

CRAN release: 2014-04-24

#### BUG FIXES

- [`gbifmap()`](https://docs.ropensci.org/rgbif/reference/gbifmap-defunct.md)
  was throwing an error because it was looking for two variables
  `latitude` and `longitude`, which had been changed to
  `decimalLatitude` and `decimalLongitude`, respectively, in other
  functions in this package. Fixed.
  ([\#81](https://github.com/ropensci/rgbif/issues/81))
- [`occ_get()`](https://docs.ropensci.org/rgbif/reference/occ_get.md)
  was updated to include changes in the GBIF API for this endpoint. The
  fix included fixing the parser for verbatim results, see
  `rgbif::gbifparser_verbatim`.
  ([\#83](https://github.com/ropensci/rgbif/issues/83))
- Fixed bugs in
  [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md) -
  it was expecting column names to be latitude and longitude, whereas
  inputs from other `rgbif` functions have changed to decimalLatitude
  and decimalLongitude.
- Fixed bug in
  [`count_facet()`](https://docs.ropensci.org/rgbif/reference/count_facet.md)
  introduced b/c GBIF no longer accepts hostCountry or nubKey
  parameters.

#### IMPROVEMENTS

- [`gist()`](https://docs.ropensci.org/rgbif/reference/gist.md),
  [`stylegeojson()`](https://docs.ropensci.org/rgbif/reference/stylegeojson.md),
  and
  [`togeojson()`](https://docs.ropensci.org/rgbif/reference/togeojson.md)
  functions now listed as deprecated. Their functionality moved to the
  `spocc` package
  ([http://cran.r-project.org/web/packages/spocc/index.html](http://cran.r-project.org/web/packages/spocc/index.md)).
  These functions will be removed from this package in a future version.
  ([\#82](https://github.com/ropensci/rgbif/issues/82))
- Added a quick sanity test for
  [`gbifmap()`](https://docs.ropensci.org/rgbif/reference/gbifmap-defunct.md).
- Added tests for
  [`occ_get()`](https://docs.ropensci.org/rgbif/reference/occ_get.md)
  for when `verbatim=TRUE`, which gives back different data than when
  `verbatim=FALSE`.

## rgbif 0.6.0

CRAN release: 2014-04-17

#### BUG FIXES

- A number of variables changed names to better follow the Darwin Core
  standard. `latitude` is now `decimalLatitude`. `longitude` is now
  `decimalLongitude`. `clazz` is now `class`. Code in this package
  changed to accomodate these changes. `date` is now `eventDate`.
  `georeferenced` is now `hasCoordinate`. Beware of these changes in
  your own code using `rgbif` - find and replace for these should be
  easy.
- Changed `altitude` parameter in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  to `elevation` - should have been `elevation` the whole time.
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  function with parameter changes: `nubKey` parameter in changed to
  `taxonKey`. New parameter `protocol`. Parameter `catalogNumber` gone.
  Parameter `hostCountry` gone. These parameters are still in the
  function definition, but if called they throw a useful warning telling
  you the correct parameter names.
  ([\#76](https://github.com/ropensci/rgbif/issues/76))
- Fixed bug in
  [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  function that was labeling facet outputs incorrectly.
  ([\#77](https://github.com/ropensci/rgbif/issues/77))

#### IMPROVEMENTS

- Better checking and parsing of response data from GBIF: Across all
  functions, we now check that the response content type is
  `application/json`, then parse JSON ourselves using
  `RJSONIO::fromJSON` (instead of httr doing it).
- Across all functions, we now return all potential character class
  columns as character class (instead of factor), by passing
  `stringsAsFactors = FALSE` to all
  [`data.frame()`](https://rdrr.io/r/base/data.frame.html) calls.
- Now using assertthat package in various places to give better error
  messages when the wrong input is passed to a function.
- Four parameters have name changes in the
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  function. These parameters are still in the function definition, but
  if called they throw a useful warning telling you the correct
  parameter names. ([\#75](https://github.com/ropensci/rgbif/issues/75))
- Updated docs in `name_usage`, `name_backbone`, `name_lookup`, and
  `name_suggest` functions.
- `sourceId` parameter in
  [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  function doesn’t work so error message is thrown when used.

#### NEW FEATURES

- New function
  [`check_wkt()`](https://docs.ropensci.org/rgbif/reference/check_wkt.md)
  to check that well known text string is the right format.
  ([\#68](https://github.com/ropensci/rgbif/issues/68))
- New dataset typestatus to look up possible specimen typeStatus values.
  See [\#74](https://github.com/ropensci/rgbif/issues/74) for more
  information.
- GBIF added some new parameters for use in the
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  function. `scientificName`: search for a species by name (instead of
  `taxonKey`). `continent`: search by continent. `lastInterpreted`:
  search by last time GBIF modified the record. `recordNumber`: search
  by the data collector’s specimen record number - this is different
  from the GBIF record number. `typeStatus`: search by specimen type
  status. ([\#74](https://github.com/ropensci/rgbif/issues/74))
- Note that given the new parameters many more options are available for
  implicit faceted search in which you can pass many values in a vector
  to do multiple searches like `parameterName = c(x, y, z)`. These
  parameters are: `taxonKey`, `scientificName`, `datasetKey`,
  `catalogNumber`, `collectorName`, `geometry`, `country`,
  `recordNumber`, `search`, `institutionCode`, `collectionCode`,
  `decimalLatitude`, `decimalLongitude`, `depth`, `year`, `typeStatus`,
  `lastInterpreted`, and `continent`. This isn’t faceted search server
  side - this is just looping your different values of the parameter
  against the GBIF API.
- Range queries are a new feature in the GBIF API. Some parameters in
  [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  now support range queries:
  `decimalLatitude`,`decimalLongitude`,`depth`,`elevation`,`eventDate`,`lastInterpreted`,`month`,
  and `year`. Do a range query for example by `depth=50,100` to ask for
  occurrences where depth was recorded between 50 and 100 meters. Note
  that this syntax `depth=c(50,100)` will perform two separate searches,
  one for `depth=50` and one for `depth=100`.
  ([\#71](https://github.com/ropensci/rgbif/issues/71))

## rgbif 0.5.0

CRAN release: 2014-02-16

#### IMPROVEMENTS

- Changed name of country_codes() function to gbif_country_codes() to
  avoid conflicts with other packages.
- Replaced sapply() with vapply() throughout the package as it is more
  robust and can be faster.
- Added a startup message to the package.
- gbifmap() now plots a map with ggplot2::coord_fixed(ratio=1) so that
  you don’t get wonky maps.
- occ_count() now accepts a call to query publishingCountry with a
  single parameter (country), to list occurrence counts by publishing
  country.
- occ_get() and occ_search() lose parameter minimal, and in its place
  gains parameter fields, in which you can request fields=‘minimal’ to
  get just name, taxon key, lat and long. Or set to ‘all’ to get all
  fields, or selection the fields you want by passing in a vector of
  field names.

#### BUG FIXES

- Updated base url for the GIBF parser function parsenames()
- isocodes dataset now with documentation.

#### NEW FEATURES

- New function count_facet() to do facetted count search, as GBIF
  doesn’t allow faceted searches against the count API.
- New function elevation() to get elevation data for a data.frame of
  lat/long points, or a list of lat/long points. This function uses the
  Google Elevation API
  (<https://developers.google.com/maps/documentation/elevation/>).
- New function installations() to get metadata on installations.

## rgbif 0.4.1

#### BUG FIXES

- Improved handling of limit parameter in occ_search() so that the
  correct number of occurrences are returned.
- Fixed various tests that were broken.

#### IMPROVEMENTS

- Added missing limit argument in datasets() function man file, also
  function gains start and callopts parameters.

## rgbif 0.4.0

CRAN release: 2013-11-20

#### IMPROVEMENTS

- Data object isocodes gains new column gbif_names, the GBIF specific
  names for countries.
- Added in deprecation messages throughout package for functions and
  arguments that are deprecated.
- tests moved to tests/testthat from inst/tests.
- Vignettes now in vignettes/ directory.

#### NEW FEATURES

- New function dataset_suggest(), a quick autocomplete service that
  returns up to 20 datasets.
- New function name_backbone() looks up names against the GBIF backbone
  taxonomy.
- New function name_suggest(), a quick autocomplete service that returns
  up to 20 name usages.
- New function occ_metadata() to search dataset metadata.
- New function parsenames() that parses taxonomic names and returns
  their components.

## rgbif 0.3.9

#### IMPROVEMENTS

- Added back in functions, and .Rd files, from old version or rgbif that
  interacts with the old GBIF API.
- Updated vignette to work with new GBIF API and fxns.

#### NEW FEATURES

- Added functions to interact with the new GBIF API, notably:
  country_codes(), dataset_metrics(), dataset_search(), datasets(),
  name_lookup(), gbifmap(), gist(), name_lookup(), name_usage(),
  networks(), nodes(), occ_count(), occ_get(), occ_search(),
  organizations(), stylegeojson(), togeojson(). See the README for a
  crosswalk from old functions to new ones.

#### BUG FIXES

- test files moved from inst/tests/ to tests/testthat/

## rgbif 0.3.2

#### BUG FIXES

- Removed georeferencedonly parameter - is deprecated in the GBIF API

## rgbif 0.3.0

CRAN release: 2013-07-19

#### IMPROVEMENTS

- Added S3 objects: Output from calls to occurrencelist() and occurrence
  list_many() now of class gbiflist, and output from calls to
  densitylist() now of class gbifdens.
- Slight changes to gbifmaps() function.
- url parameter in all functions moved into the function itself as the
  base GBIF API url doesn’t need to be specified by user.
- Vignette added.

#### NEW FEATURES

- Added function country_codes() to look up 2 character ISO country
  codes for use in searches.
- Added function occurrencelist_many() to handle searches of many
  species.
- Added functions togeojson() and stylegeosjon() to convert a data.frame
  with lat/long columns to geojson file format, and to add styling to
  data.frames before using togeojson() .
- occurrencelist() and occurrencelist_many() gain argument fixnames,
  which lets user change species names in output data.frame according to
  a variety of scenarios.
- taxonsearch() gains argument accepted_status to accept only those
  names that have a status of accepted. In addition, this function has
  significant changes, and examples, to improve performance.

## rgbif 0.2.0

CRAN release: 2013-03-01

#### IMPROVEMENTS

- Improved code style, and simplified code in some functions.

#### NEW FEATURES

- occurrencelist() now handles scientific notation when maxresults are
  given in that form.
- occurencelist() now can retrieve any number of records; was previously
  a max of 1000 records.

#### BUG FIXES

- Demo “List” was returning incorrect taxon names - corrected now.
- Removed unused parameter ‘latlongdf’ in occurencelist().

## rgbif 0.1.5

CRAN release: 2012-12-04

#### IMPROVEMENTS

- Changed all functions to use RCurl instead of httr as httr was
  presenting some problems.
- Two function, capwords and gbifxmlToDataFrame, added with
  documentation as internal functions.

#### NEW FEATURES

- Added function density_spplist to get a species list or data.frame of
  species and their counts for any degree cell.
- Added function densitylist to access to records showing the density of
  occurrence records from the GBIF Network by one-degree cell.
- Added function gbifmap to make a simple map to visualize GBIF data.
- Added function occurrencecount to count taxon concept records matching
  a range of filters.

DEPRECATED

- gbifdatause removed, was just a function to return the data sharing
  agreement from GBIF.

## rgbif 0.1.0

#### NEW FEATURES

- released to CRAN
