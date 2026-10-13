# GBIF registry data via OAI-PMH

GBIF registry data via OAI-PMH

## Usage

``` r
gbif_oai_identify(...)

gbif_oai_list_identifiers(
  prefix = "oai_dc",
  from = NULL,
  until = NULL,
  set = NULL,
  token = NULL,
  as = "df",
  ...
)

gbif_oai_list_records(
  prefix = "oai_dc",
  from = NULL,
  until = NULL,
  set = NULL,
  token = NULL,
  as = "df",
  ...
)

gbif_oai_list_metadataformats(id = NULL, ...)

gbif_oai_list_sets(token = NULL, as = "df", ...)

gbif_oai_get_records(ids, prefix = "oai_dc", as = "parsed", ...)
```

## Arguments

- ...:

  Curl options passed on to
  [`httr::GET`](https://httr.r-lib.org/reference/GET.html)

- prefix:

  (character) A string to specify the metadata format in OAI-PMH
  requests issued to the repository. The default (`"oai_dc"`)
  corresponds to the mandatory OAI unqualified Dublin Core metadata
  schema.

- from:

  (character) string giving datestamp to be used as lower bound for
  datestamp-based selective harvesting (i.e., only harvest records with
  datestamps in the given range). Dates and times must be encoded using
  ISO 8601. The trailing Z must be used when including time. OAI-PMH
  implies UTC for data/time specifications.

- until:

  (character) Datestamp to be used as an upper bound, for
  datestamp-based selective harvesting (i.e., only harvest records with
  datestamps in the given range).

- set:

  (character) A set to be used for selective harvesting (i.e., only
  harvest records in the given set).

- token:

  (character) a token previously provided by the server to resume a
  request where it last left off. 50 is max number of records returned.
  We will loop for you internally to get all the records you asked for.

- as:

  (character) What to return. One of "df" (for data.frame; default),
  "list" (get a list), or "raw" (raw text). For `gbif_oai_get_records`,
  one of "parsed" or "raw"

- id, ids:

  (character) The OAI-PMH identifier for the record. Optional.

## Value

raw text, list or data.frame, depending on requested output via `as`
parameter

## Details

These functions only work with GBIF registry data, and do so via the
OAI-PMH protocol
(https://www.openarchives.org/OAI/openarchivesprotocol.html)

## Examples

``` r
if (FALSE) { # \dontrun{
gbif_oai_identify()

today <- format(Sys.Date(), "%Y-%m-%d")
gbif_oai_list_identifiers(from = today)
gbif_oai_list_identifiers(set = "country:NL")

gbif_oai_list_records(from = today)
gbif_oai_list_records(set = "country:NL")

gbif_oai_list_metadataformats()
gbif_oai_list_metadataformats(id = "9c4e36c1-d3f9-49ce-8ec1-8c434fa9e6eb")

gbif_oai_list_sets()
gbif_oai_list_sets(as = "list")

gbif_oai_get_records("9c4e36c1-d3f9-49ce-8ec1-8c434fa9e6eb")
ids <- c("9c4e36c1-d3f9-49ce-8ec1-8c434fa9e6eb",
         "e0f1bb8a-2d81-4b2a-9194-d92848d3b82e")
gbif_oai_get_records(ids)
} # }
```
