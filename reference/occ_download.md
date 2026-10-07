# Spin up a download request for GBIF occurrence data.

Spin up a download request for GBIF occurrence data.

## Usage

``` r
occ_download(
  ...,
  body = NULL,
  type = "and",
  format = "DWCA",
  verbatim_extensions = NULL,
  checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b",
  user = NULL,
  pwd = NULL,
  email = NULL,
  curlopts = list(http_version = 2)
)

occ_download_prep(
  ...,
  body = NULL,
  type = "and",
  format = "DWCA",
  verbatim_extensions = NULL,
  checklistKey = NULL,
  user = NULL,
  pwd = NULL,
  email = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- ...:

  For `occ_download()` and `occ_download_prep()`, one or more objects of
  class `occ_predicate` or `occ_predicate_list`, created by `pred*`
  functions (see
  [download_predicate_dsl](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md)).
  If you use this, don't use `body` parameter.

- body:

  if you prefer to pass in the payload yourself, use this parameter. If
  you use this, don't pass anything to the dots. Accepts either an R
  list, or JSON. JSON is likely easier, since the JSON library jsonlite
  requires that you unbox strings that shouldn't be auto-converted to
  arrays, which is a bit tedious for large queries. optional

- type:

  (character) One of equals (=), and (&), or (\|), lessThan (\<),
  lessThanOrEquals (\<=), greaterThan (\>), greaterThanOrEquals (\>=),
  in, within, not (!), like, isNotNull

- format:

  (character) The download format. One of 'DWCA' (default),
  'SIMPLE_CSV', or 'SPECIES_LIST'

- verbatim_extensions:

  (character vector) A character vector of verbatim extensions to
  include in the download. This parameter is only applied when
  `format = "DWCA"` and will be ignored for other formats.

- checklistKey:

  (character) The UUID key for a checklist dataset to use for taxonomy
  in the download. The default is COL (Catalogue of Life) Extended
  Release (7ddf754f-d193-4cc9-b351-99906754a03b). Optional

- user:

  (character) User name within GBIF's website. Required. See
  "Authentication" below

- pwd:

  (character) User password within GBIF's website. Required. See
  "Authentication" below

- email:

  (character) Email address to receive download notice done email.
  Required. See "Authentication" below

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Note

see [downloads](https://docs.ropensci.org/rgbif/reference/downloads.md)
for an overview of GBIF downloads methods

When numeric taxonomic keys (taxonKey, speciesKey, kingdomKey, etc.) are
detected in predicates and checklistKey is set to COL XR (the default)
or NULL, the function automatically switches to the GBIF Backbone
taxonomy checklistKey and issues a warning. These numeric keys are
legacy identifiers. If you explicitly set checklistKey to Backbone or
another taxonomy, no warning is issued. Consider migrating to COL XR
identifiers using
[`gbif_to_col()`](https://docs.ropensci.org/rgbif/reference/gbif_to_col.md).

## geometry

When using the geometry parameter, make sure that your well known text
(WKT) is formatted as GBIF expects it. They expect WKT to have a
counter-clockwise winding order. For example, the following is clockwise
`POLYGON((-19.5 34.1, -25.3 68.1, 35.9 68.1, 27.8 34.1, -19.5 34.1))`,
whereas they expect the other order:
`POLYGON((-19.5 34.1, 27.8 34.1, 35.9 68.1, -25.3 68.1, -19.5 34.1))`

note that coordinate pairs are `longitude latitude`, longitude first,
then latitude

you should not get any results if you supply WKT that has clockwise
winding order.

also note that
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)/[`occ_data()`](https://docs.ropensci.org/rgbif/reference/occ_data.md)
behave differently with respect to WKT in that you can supply clockwise
WKT to those functions but they treat it as an exclusion, so get all
data not inside the WKT area.

## checklistKey

You can specify the taxonomy to be included in occurrence downloads by
adding the `checklistKey` parameter to the download request. The value
should be a UUID for a checklist dataset in GBIF. By default, the GBIF
Backbone Taxonomy will be used if no `checklistKey` is supplied.

## Methods

- `occ_download_prep`: prepares a download request, but DOES NOT execute
  it. meant for use with
  [`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md)

- `occ_download`: prepares a download request and DOES execute it

## Authentication

For `user`, `pwd`, and `email` parameters, you can set them in one of
three ways:

- Set them in your `.Rprofile` file with the names `gbif_user`,
  `gbif_pwd`, and `gbif_email`

- Set them in your `.Renviron`/`.bash_profile` (or similar) file with
  the names `GBIF_USER`, `GBIF_PWD`, and `GBIF_EMAIL`

- Simply pass strings to each of the parameters in the function call

We strongly recommend the second option - storing your details as
environment variables as it's the most widely used way to store secrets.

See [`?Startup`](https://rdrr.io/r/base/Startup.html) for help.

## Query length

GBIF has a limit of 12,000 characters for a download query. This means
that you can have a pretty long query, but at some point it may lead to
an error on GBIF's side and you'll have to split your query into a few.

## References

See the API docs <https://www.gbif.org/developer/occurrence#download>
for more info, and the predicates docs
<https://www.gbif.org/developer/occurrence#predicates>

## See also

Other downloads:
[`download_predicate_dsl`](https://docs.ropensci.org/rgbif/reference/download_predicate_dsl.md),
[`occ_download_cached()`](https://docs.ropensci.org/rgbif/reference/occ_download_cached.md),
[`occ_download_cancel()`](https://docs.ropensci.org/rgbif/reference/occ_download_cancel.md),
[`occ_download_dataset_activity()`](https://docs.ropensci.org/rgbif/reference/occ_download_dataset_activity.md),
[`occ_download_datasets()`](https://docs.ropensci.org/rgbif/reference/occ_download_datasets.md),
[`occ_download_get()`](https://docs.ropensci.org/rgbif/reference/occ_download_get.md),
[`occ_download_import()`](https://docs.ropensci.org/rgbif/reference/occ_download_import.md),
[`occ_download_list()`](https://docs.ropensci.org/rgbif/reference/occ_download_list.md),
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md),
[`occ_download_queue()`](https://docs.ropensci.org/rgbif/reference/occ_download_queue.md),
[`occ_download_stats_dataset_records()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset_records.md),
[`occ_download_stats_dataset()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_dataset.md),
[`occ_download_stats_export()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_export.md),
[`occ_download_stats_source()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_source.md),
[`occ_download_stats_user_country()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats_user_country.md),
[`occ_download_stats()`](https://docs.ropensci.org/rgbif/reference/occ_download_stats.md),
[`occ_download_wait()`](https://docs.ropensci.org/rgbif/reference/occ_download_wait.md)

## Examples
