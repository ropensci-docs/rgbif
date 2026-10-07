# Download occurrence data using a SQL query

Download occurrence data using a SQL query

## Usage

``` r
occ_download_sql(
  q = NULL,
  format = "SQL_TSV_ZIP",
  user = NULL,
  pwd = NULL,
  email = NULL,
  validate = TRUE,
  curlopts = list(http_version = 2)
)

occ_download_sql_validate(
  q = NULL,
  user = NULL,
  pwd = NULL,
  curlopts = list(http_version = 2)
)

occ_download_sql_prep(
  q = NULL,
  format = "SQL_TSV_ZIP",
  user = NULL,
  pwd = NULL,
  email = NULL,
  validate = TRUE,
  curlopts = list(http_version = 2)
)
```

## Arguments

- q:

  sql query

- format:

  only "SQL_TSV_ZIP" is supported right now

- user:

  your GBIF user name

- pwd:

  your GBIF password

- email:

  your email address

- validate:

  should the query be validated before submission. Default is TRUE.

- curlopts:

  list of curl options

## Value

an object of class 'occ_download_sql'

## Details

This is an experimental feature, and the implementation may change
throughout 2024. The feature is currently only available for preview by
invited users. Contact `helpdesk@gbif.org` to request access.

Please see the article here for more information:
<https://docs.ropensci.org/rgbif/articles/gbif_sql_downloads.html>

## References

<https://techdocs.gbif.org/en/data-use/api-sql-downloads>

## Examples

``` r
if (FALSE) { # \dontrun{
occ_download_sql("SELECT gbifid,countryCode FROM occurrence 
                  WHERE genusKey = 2435098")
} # }
```
