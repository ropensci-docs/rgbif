# Get installation metadata using an installation key

Get installation metadata using an installation key

## Usage

``` r
installation_dataset(
  uuid = NULL,
  limit = 20,
  start = NULL,
  curlopts = list(http_version = 2)
)

installation_comment(uuid = NULL, curlopts = list(http_version = 2))

installation_contact(uuid = NULL, curlopts = list(http_version = 2))

installation_endpoint(uuid = NULL, curlopts = list(http_version = 2))

installation_identifier(uuid = NULL, curlopts = list(http_version = 2))

installation_machinetag(uuid = NULL, curlopts = list(http_version = 2))

installation_tag(uuid = NULL, curlopts = list(http_version = 2))
```

## Arguments

- uuid:

  A GBIF installationKey uuid.

- limit:

  The number of results to return. Default is 20.

- start:

  The offset of the first result to return.

- curlopts:

  A list of curl options to pass to the request.

## Value

A `tibble` or a `list`.

## Examples

``` r
if (FALSE) { # \dontrun{
# Get all datasets for a given installation 
installation_dataset(uuid="d209e552-7e6e-4840-b13c-c0596ef36e55", limit=10)
installation_comment(uuid="a0e05292-3d09-4eae-9f83-02ae3516283c")
installation_contact(uuid="896898e8-c0ac-47a0-8f38-0f792fbe3343")
installation_endpoint(uuid="896898e8-c0ac-47a0-8f38-0f792fbe3343")
installation_identifier(uuid="896898e8-c0ac-47a0-8f38-0f792fbe3343")
installation_machinetag(uuid="896898e8-c0ac-47a0-8f38-0f792fbe3343")
} # }
```
