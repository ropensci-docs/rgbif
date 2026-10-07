# Count downloads for a user.

Count downloads for a user.

## Usage

``` r
occ_download_user_count(
  user = NULL,
  pwd = NULL,
  from = NULL,
  status = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- user:

  (character) User name within GBIF's website. Required. See Details.

- pwd:

  (character) User password within GBIF's website. Required. See
  Details.

- from:

  (character) Optional. Start date in format `YYYY-MM-DD`. Only
  downloads created on or after this date will be counted.

- status:

  (character) Optional. Filter by download status. One of `"PREPARING"`,
  `"RUNNING"`, `"SUCCEEDED"`, `"CANCELLED"`, `"KILLED"`, `"FAILED"`,
  `"SUSPENDED"`, or `"FILE_ERASED"`.

- curlopts:

  list of named curl options passed on to
  [`HttpClient`](https://docs.ropensci.org/crul/reference/HttpClient.html).
  see
  [`curl::curl_options`](https://jeroen.r-universe.dev/curl/reference/curl_options.html)
  for curl options

## Value

a single integer with the total number of downloads for the user.

## Details

For `user` and `pwd` parameters, you can set them in one of three ways:

- Set them in your `.Rprofile` file with the names `gbif_user` and
  `gbif_pwd`

- Set them in your `.Renviron`/`.bash_profile` (or similar) file with
  the names `GBIF_USER` and `GBIF_PWD`

- Simply pass strings to each of the parameters in the function call

See [`?Startup`](https://rdrr.io/r/base/Startup.html) for help.

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_user_count(user="jwaller", pwd="your_password")
occ_download_user_count(user="jwaller", pwd="your_password", from="2023-01-01")
occ_download_user_count(user="jwaller", pwd="your_password", status="SUCCEEDED")
} # }
```
