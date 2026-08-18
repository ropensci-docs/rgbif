# Check if a dataset is gridded

Check if a dataset is gridded

## Usage

``` r
dataset_gridded(
  uuid = NULL,
  min_dis = 0.05,
  min_per = 50,
  min_dis_count = 30,
  return = "logical",
  warn = TRUE
)
```

## Arguments

- uuid:

  (vector) A character vector of GBIF datasetkey uuids.

- min_dis:

  (numeric) (default 0.02) Minimum distance in degrees to accept as
  gridded.

- min_per:

  (integer)(default 50%) Minimum percentage of points having same
  nearest neighbor distance to be considered gridded.

- min_dis_count:

  (default 30) Minimum number of unique points to accept an assessment
  of 'griddyness'.

- return:

  (character) (default "logical"). Choice of "data" will return a
  data.frame of more information or "logical" will return just TRUE or
  FALSE indicating whether a dataset is considered 'gridded".

- warn:

  (logical) indicates whether to warn about missing values or bad
  values.

## Value

A logical `vector` indicating whether a dataset is considered gridded.
Or if `return="data"`, a `data.frame` of more information.

## Details

Gridded datasets are a known problem at GBIF. Many datasets have
equally-spaced points in a regular pattern. These datasets are usually
systematic national surveys or data taken from some atlas (“so-called
rasterized collection designs”). This function uses the percentage of
unique lat-long points with the most common nearest neighbor distance to
identify gridded datasets.

<https://data-blog.gbif.org/post/finding-gridded-datasets/>

I recommend keeping the default values for the parameters.

## Examples

``` r
if (FALSE) { # \dontrun{

dataset_gridded("9070a460-0c6e-11dd-84d2-b8a03c50a862")
dataset_gridded(c("9070a460-0c6e-11dd-84d2-b8a03c50a862",
               "13b70480-bd69-11dd-b15f-b8a03c50a862"))


} # }
```
