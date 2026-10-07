# Check input WKT

Check input WKT

## Usage

``` r
check_wkt(wkt = NULL, skip_validate = FALSE)
```

## Arguments

- wkt:

  (character) one or more Well Known Text objects

- skip_validate:

  (logical) whether to skip
  [`wk::wk_problems`](https://paleolimbot.github.io/wk/reference/wk_problems.html)
  call or not. Default: `FALSE`

## Examples

``` r
if (FALSE) { # \dontrun{
check_wkt('POLYGON((30.1 10.1, 10 20, 20 60, 60 60, 30.1 10.1))')
check_wkt('POINT(30.1 10.1)')
check_wkt('LINESTRING(3 4,10 50,20 25)')

# check many passed in at once
check_wkt(c('POLYGON((30.1 10.1, 10 20, 20 60, 60 60, 30.1 10.1))',
  'POINT(30.1 10.1)'))

# bad WKT
# wkt <- 'POLYGON((30.1 10.1, 10 20, 20 60, 60 60, 30.1 a))'
# check_wkt(wkt)

# many wkt's, semi-colon separated, for many repeated "geometry" args
wkt <- "POLYGON((-102.2 46.0,-93.9 46.0,-93.9 43.7,-102.2 43.7,-102.2 46.0))
;POLYGON((30.1 10.1, 10 20, 20 40, 40 40, 30.1 10.1))"
check_wkt(gsub("\n", '', wkt))
} # }
```
