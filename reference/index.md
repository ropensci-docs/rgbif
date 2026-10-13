# Package index

## rgbif

High level overview of package

- [`rgbif-package`](https://docs.ropensci.org/rgbif/reference/rgbif-package.md)
  [`rgbif`](https://docs.ropensci.org/rgbif/reference/rgbif-package.md)
  : Interface to the Global Biodiversity Information Facility API.

## Occurrence downloads

Work with the GBIF occurrence downloads APIs
<https://www.gbif.org/developer/occurrence#download>

- [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  [`occ_download_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  : Spin up a download request for GBIF occurrence data.
- [`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md)
  : Check for downloads already in your GBIF account
- [`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md)
  [`occ_download_cancel_staged()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md)
  : Cancel a download creation process.
- [`occ_download_countries()`](https://docs.ropensci.org/rgbif/reference/occ_download_countries.md)
  : List countries for a download
- [`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md)
  : Lists the downloads activity of a dataset
- [`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md)
  : List datasets for a download
- [`occ_download_describe()`](https://docs.ropensci.org/rgbif/reference/occ_download_describe.md)
  : Describes the fields available in GBIF downloads
- [`occ_download_doi()`](https://docs.ropensci.org/rgbif/reference/occ_download_doi.md)
  : Get download meta data from a doi
- [`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md)
  : Get a download from GBIF.
- [`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  [`as.download()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md)
  : Import a downloaded file from GBIF.
- [`occ_download_list()`](https://docs.ropensci.org/rgbif/reference/occ_download_list.md)
  : Lists the downloads created by a user.
- [`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)
  : Retrieves the occurrence download metadata by its unique key.
- [`occ_download_organizations()`](https://docs.ropensci.org/rgbif/reference/occ_download_organizations.md)
  : List organizations for a download
- [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)
  : Download requests in a queue
- [`occ_download_sql()`](https://docs.ropensci.org/rgbif/reference/occ_download_sql.md)
  [`occ_download_sql_validate()`](https://docs.ropensci.org/rgbif/reference/occ_download_sql.md)
  [`occ_download_sql_prep()`](https://docs.ropensci.org/rgbif/reference/occ_download_sql.md)
  : Download occurrence data using a SQL query
- [`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md)
  : Occurrence download statistics
- [`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md)
  : Downloads by dataset
- [`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md)
  : Downloaded records by dataset
- [`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md)
  : Export summary of occurrence downloads
- [`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md)
  : Downloads by source
- [`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md)
  : Downloads by user country
- [`occ_download_user_count()`](https://docs.ropensci.org/rgbif/reference/occ_download_user_count.md)
  : Count downloads for a user.
- [`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md)
  : Wait for an occurrence download to be done
- [`downloads`](https://docs.ropensci.org/rgbif/reference/downloads.md)
  : Downloads interface
- [`pred()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_gt()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_gte()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_lt()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_lte()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_not()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_like()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_within()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_isnull()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_notnull()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_or()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_and()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_in()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  [`pred_default()`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)
  : Download predicate DSL (domain specific language)

## Occurrence search

Work with the GBIF occurrence search APIs
<https://www.gbif.org/developer/occurrence>

- [`occ_get()`](https://docs.ropensci.org/rgbif/reference/occ_get.md)
  [`occ_get_verbatim()`](https://docs.ropensci.org/rgbif/reference/occ_get.md)
  : Get data for GBIF occurrences by occurrence key
- [`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
  : Legacy alternative to occ_search
- [`occ_metadata()`](https://docs.ropensci.org/rgbif/reference/occ_metadata.md)
  : Search for catalog numbers, collection codes, collector names, and
  institution codes.
- [`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
  : Search for GBIF occurrences
- [`occ_count()`](https://docs.ropensci.org/rgbif/reference/occ_count.md)
  : Get number of occurrence records.
- [`occ_count_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)
  [`occ_count_pub_country()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)
  [`occ_count_year()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)
  [`occ_count_basis_of_record()`](https://docs.ropensci.org/rgbif/reference/occ_count_.md)
  : Get quick pre-computed occurrence counts of a limited number of
  dimensions.
- [`occ_term()`](https://docs.ropensci.org/rgbif/reference/occ_term.md)
  : Get occurrence terms.

## Taxonomic names

Work with the GBIF taxonomic names API
<https://www.gbif.org/developer/species>

- [`name_backbone()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
  [`name_backbone_verbose()`](https://docs.ropensci.org/rgbif/reference/name_backbone.md)
  : Match names to GBIF backbone and other checklists.
- [`name_backbone_checklist()`](https://docs.ropensci.org/rgbif/reference/name_backbone_checklist.md)
  : Match names in the GBIF backbone taxonomy in a checklist.
- [`name_parse()`](https://docs.ropensci.org/rgbif/reference/name_parse.md)
  : Parse taxon names using the GBIF name parser.
- [`gbif_to_col()`](https://docs.ropensci.org/rgbif/reference/gbif_to_col.md)
  : Convert GBIF Backbone taxon keys to COL Extended Release keys

## Citation

<https://docs.ropensci.org/rgbif/articles/gbif_citations.html>

- [`gbif_citation()`](https://docs.ropensci.org/rgbif/reference/gbif_citation.md)
  : Get citation for datasets used
- [`derived_dataset()`](https://docs.ropensci.org/rgbif/reference/derived_dataset.md)
  [`derived_dataset_prep()`](https://docs.ropensci.org/rgbif/reference/derived_dataset.md)
  : Register a derived dataset for citation.

## Geometry

- [`check_wkt()`](https://docs.ropensci.org/rgbif/reference/check_wkt.md)
  : Check input WKT
- [`gbif_bbox2wkt()`](https://docs.ropensci.org/rgbif/reference/gbif_bbox2wkt.md)
  [`gbif_wkt2bbox()`](https://docs.ropensci.org/rgbif/reference/gbif_bbox2wkt.md)
  : Convert a bounding box to a Well Known Text polygon, and a WKT to a
  bounding box
- [`gbif_geocode()`](https://docs.ropensci.org/rgbif/reference/gbif_geocode.md)
  : Geocode lat-lon point(s) with GBIF's set of geo-polygons
  (experimental)

## Registry

GBIF registry functions <https://www.gbif.org/developer/registry>

- [`dataset_doi()`](https://docs.ropensci.org/rgbif/reference/dataset_doi.md)
  : Get a GBIF dataset from a doi
- [`dataset_gridded()`](https://docs.ropensci.org/rgbif/reference/dataset_gridded.md)
  : Check if a dataset is gridded
- [`dataset_duplicate()`](https://docs.ropensci.org/rgbif/reference/dataset_list_funs.md)
  [`dataset_noendpoint()`](https://docs.ropensci.org/rgbif/reference/dataset_list_funs.md)
  : List datasets that are deleted or have no endpoint.
- [`dataset_export()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  [`dataset_search()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  [`dataset_suggest()`](https://docs.ropensci.org/rgbif/reference/dataset_search.md)
  : Search for dataset metadata.
- [`dataset_get()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_process()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_networks()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_constituents()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_comment()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_contact()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_endpoint()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_identifier()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_machinetag()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_tag()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  [`dataset_metrics()`](https://docs.ropensci.org/rgbif/reference/dataset_uuid_funs.md)
  : Get dataset metadata using a datasetkey
- [`dataset()`](https://docs.ropensci.org/rgbif/reference/dataset.md) :
  Search for more obscure dataset metadata.
- [`organizations()`](https://docs.ropensci.org/rgbif/reference/organizations.md)
  : Organizations metadata.
- [`network()`](https://docs.ropensci.org/rgbif/reference/network.md)
  [`network_constituents()`](https://docs.ropensci.org/rgbif/reference/network.md)
  : Get data about GBIF networks
- [`nodes()`](https://docs.ropensci.org/rgbif/reference/nodes.md) :
  Nodes metadata.
- [`installations()`](https://docs.ropensci.org/rgbif/reference/installations.md)
  : Installations metadata.
- [`installation_search()`](https://docs.ropensci.org/rgbif/reference/installation_search.md)
  : Search for installations
- [`installation_dataset()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_comment()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_contact()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_endpoint()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_identifier()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_machinetag()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  [`installation_tag()`](https://docs.ropensci.org/rgbif/reference/installation_uuid_funs.md)
  : Get installation metadata using an installation key

## OAI

- [`gbif_oai_identify()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  [`gbif_oai_list_identifiers()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  [`gbif_oai_list_records()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  [`gbif_oai_list_metadataformats()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  [`gbif_oai_list_sets()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  [`gbif_oai_get_records()`](https://docs.ropensci.org/rgbif/reference/gbif_oai.md)
  : GBIF registry data via OAI-PMH

## Maps

Work with the GBIF Maps API <https://www.gbif.org/developer/maps>

- [`map_fetch()`](https://docs.ropensci.org/rgbif/reference/map_fetch.md)
  : Fetch maps of GBIF occurrences
- [`mvt_fetch()`](https://docs.ropensci.org/rgbif/reference/mvt_fetch.md)
  : Fetch Map Vector Tiles (MVT)

## GRSciColl

- [`institution_search()`](https://docs.ropensci.org/rgbif/reference/institution_search.md)
  [`institution_export()`](https://docs.ropensci.org/rgbif/reference/institution_search.md)
  : Search GRSciColl institutions
- [`collection_search()`](https://docs.ropensci.org/rgbif/reference/collection_search.md)
  [`collection_export()`](https://docs.ropensci.org/rgbif/reference/collection_search.md)
  : Search GRSciColl collections

## Miscellaneous

- [`rgb_country_codes()`](https://docs.ropensci.org/rgbif/reference/rgb_country_codes.md)
  : Look up 2 character ISO country codes
- [`taxrank()`](https://docs.ropensci.org/rgbif/reference/taxrank.md) :
  Get the possible values to be used for (taxonomic) rank arguments in
  GBIF API methods.
- [`wkt_parse()`](https://docs.ropensci.org/rgbif/reference/wkt_parse.md)
  : parse wkt into smaller bits
- [`elevation()`](https://docs.ropensci.org/rgbif/reference/elevation.md)
  : Get elevation for lat/long points from a data.frame or list of
  points.
- [`enumeration()`](https://docs.ropensci.org/rgbif/reference/enumeration.md)
  [`enumeration_country()`](https://docs.ropensci.org/rgbif/reference/enumeration.md)
  : Enumerations.
- [`gbif_issues()`](https://docs.ropensci.org/rgbif/reference/gbif_issues.md)
  : List all GBIF issues and their codes.
- [`gbif_issues_lookup()`](https://docs.ropensci.org/rgbif/reference/gbif_issues_lookup.md)
  : Lookup issue definitions and short codes
- [`lit_search()`](https://docs.ropensci.org/rgbif/reference/lit_search.md)
  [`lit_count()`](https://docs.ropensci.org/rgbif/reference/lit_search.md)
  [`lit_export()`](https://docs.ropensci.org/rgbif/reference/lit_search.md)
  : Search for literature that cites GBIF mediated data

## Pretty html reports

- [`gbif_names()`](https://docs.ropensci.org/rgbif/reference/gbif_names.md)
  : View highlighted terms in name results from GBIF.
- [`gbif_photos()`](https://docs.ropensci.org/rgbif/reference/gbif_photos.md)
  : View photos from GBIF.

## Defunct and deprecated

- [`name_lookup()`](https://docs.ropensci.org/rgbif/reference/name_lookup.md)
  : Lookup names in all taxonomies in GBIF.
- [`name_suggest()`](https://docs.ropensci.org/rgbif/reference/name_suggest.md)
  : Suggest up to 20 name usages.
- [`name_usage()`](https://docs.ropensci.org/rgbif/reference/name_usage.md)
  : Lookup details for specific names in all taxonomies in GBIF.
- [`name_issues()`](https://docs.ropensci.org/rgbif/reference/name_issues.md)
  : Parse and examine further GBIF name issues on a dataset.
- [`datasets()`](https://docs.ropensci.org/rgbif/reference/datasets.md)
  : Search for datasets and dataset metadata.
- [`rgbif-defunct`](https://docs.ropensci.org/rgbif/reference/rgbif-defunct.md)
  : Defunct functions in rgbif
- [`parsenames()`](https://docs.ropensci.org/rgbif/reference/parsenames.md)
  : Parse taxon names using the GBIF name parser.
- [`networks()`](https://docs.ropensci.org/rgbif/reference/networks.md)
  : Networks metadata.
- [`count_facet()`](https://docs.ropensci.org/rgbif/reference/count_facet.md)
  : Facetted count occurrence search.
- [`occ_facet()`](https://docs.ropensci.org/rgbif/reference/occ_facet.md)
  : Facet GBIF occurrences
- [`occ_issues()`](https://docs.ropensci.org/rgbif/reference/occ_issues.md)
  : Parse and examine further GBIF occurrence issues on a dataset.
