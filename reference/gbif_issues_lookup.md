# Lookup issue definitions and short codes

Lookup issue definitions and short codes

## Usage

``` r
gbif_issues_lookup(issue = NULL, code = NULL)
```

## Arguments

- issue:

  Full name of issue, e.g, CONTINENT_COUNTRY_MISMATCH

- code:

  An issue short code, e.g. 'ccm'

## Examples

``` r
gbif_issues_lookup(issue = 'CONTINENT_COUNTRY_MISMATCH')
#>   code                      issue
#> 2  ccm CONTINENT_COUNTRY_MISMATCH
#>                                              description       type
#> 2 The interpreted continent and country do not match up. occurrence
gbif_issues_lookup(code = 'ccm')
#>   code                      issue
#> 2  ccm CONTINENT_COUNTRY_MISMATCH
#>                                              description       type
#> 2 The interpreted continent and country do not match up. occurrence
gbif_issues_lookup(issue = 'COORDINATE_INVALID')
#>   code              issue
#> 5 cdiv COORDINATE_INVALID
#>                                                               description
#> 5 Coordinate value given in some form but GBIF is unable to interpret it.
#>         type
#> 5 occurrence
gbif_issues_lookup(code = 'cdiv')
#>   code              issue
#> 5 cdiv COORDINATE_INVALID
#>                                                               description
#> 5 Coordinate value given in some form but GBIF is unable to interpret it.
#>         type
#> 5 occurrence
```
