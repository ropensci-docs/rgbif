# Get dataset metadata using a datasetkey

Get dataset metadata using a datasetkey

## Usage

``` r
dataset_get(uuid = NULL, curlopts = list(http_version = 2))

dataset_process(
  uuid = NULL,
  limit = 20,
  start = NULL,
  curlopts = list(http_version = 2)
)

dataset_networks(
  uuid = NULL,
  limit = 20,
  start = NULL,
  curlopts = list(http_version = 2)
)

dataset_constituents(
  uuid = NULL,
  limit = 20,
  start = NULL,
  curlopts = list(http_version = 2)
)

dataset_comment(uuid = NULL, curlopts = list(http_version = 2))

dataset_contact(uuid = NULL, curlopts = list(http_version = 2))

dataset_endpoint(uuid = NULL, curlopts = list(http_version = 2))

dataset_identifier(uuid = NULL, curlopts = list(http_version = 2))

dataset_machinetag(uuid = NULL, curlopts = list(http_version = 2))

dataset_tag(uuid = NULL, curlopts = list(http_version = 2))

dataset_metrics(uuid = NULL, curlopts = list(http_version = 2))
```

## Arguments

- uuid:

  A GBIF datasetkey uuid.

- curlopts:

  options passed on to
  [crul::HttpClient](https://docs.ropensci.org/crul/reference/HttpClient.html).

- limit:

  Number of records to return.

- start:

  Record number to start at.

## Value

A `tibble` or a `list`.

## Details

`dataset_metrics()` can only be used with checklist type datasets.

## References

<https://techdocs.gbif.org/en/openapi/v1/registry>

## Examples

``` r
if (FALSE) { # \dontrun{
dataset_get("38b4c89f-584c-41bb-bd8f-cd1def33e92f")
dataset_process("38b4c89f-584c-41bb-bd8f-cd1def33e92f",limit=3)
dataset_networks("3dab037f-a520-4bc3-b888-508755c2eb52")
dataset_constituents("7ddf754f-d193-4cc9-b351-99906754a03b",limit=3)
dataset_comment("2e4cc37b-302e-4f1b-bbbb-1f674ff90e14")
dataset_contact("7ddf754f-d193-4cc9-b351-99906754a03b")
dataset_endpoint("7ddf754f-d193-4cc9-b351-99906754a03b")
dataset_identifier("7ddf754f-d193-4cc9-b351-99906754a03b")
dataset_machinetag("7ddf754f-d193-4cc9-b351-99906754a03b")
dataset_tag("c47f13c1-7427-45a0-9f12-237aad351040")
dataset_metrics("7ddf754f-d193-4cc9-b351-99906754a03b")
} # }
```
