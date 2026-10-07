# GbifQueue

GBIF download queue

## Public fields

- `reqs`:

  (list) a named list of objects of class
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)

- `queue`:

  (list) holds the queued jobs

## Methods

### Public methods

- [`GbifQueue$print()`](#method-GbifQueue-print)

- [`GbifQueue$new()`](#method-GbifQueue-new)

- [`GbifQueue$add()`](#method-GbifQueue-add)

- [`GbifQueue$add_all()`](#method-GbifQueue-add_all)

- [`GbifQueue$remove()`](#method-GbifQueue-remove)

- [`GbifQueue$next_()`](#method-GbifQueue-next_)

- [`GbifQueue$last_()`](#method-GbifQueue-last_)

- [`GbifQueue$jobs()`](#method-GbifQueue-jobs)

- [`GbifQueue$clone()`](#method-GbifQueue-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for the `GbifQueue` class

#### Usage

    GbifQueue$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `new()`

Create a new `GbifQueue` object

#### Usage

    GbifQueue$new(..., .list = list())

#### Arguments

- `...`:

  any number of
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  requests

- `.list`:

  any number of
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  requests as `lazy` objects, called with e.g.,
  [`lazyeval::lazy()`](https://rdrr.io/pkg/lazyeval/man/lazy_.html)

#### Returns

A new `GbifQueue` object

------------------------------------------------------------------------

### Method `add()`

Add single jobs to the queue

#### Usage

    GbifQueue$add(x)

#### Arguments

- `x`:

  an
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  object

#### Returns

nothing returned; adds job (`x`) to the queue

------------------------------------------------------------------------

### Method `add_all()`

Add all jobs to the queue

#### Usage

    GbifQueue$add_all()

#### Returns

nothing returned

------------------------------------------------------------------------

### Method [`remove()`](https://rdrr.io/r/base/rm.html)

Remove a job from the queue

#### Usage

    GbifQueue$remove(x)

#### Arguments

- `x`:

  an
  [`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
  object

#### Returns

nothing returned

------------------------------------------------------------------------

### Method `next_()`

Get the next job in the `queue`. if no more jobs, returns empty list

#### Usage

    GbifQueue$next_()

#### Returns

next job or empty list

------------------------------------------------------------------------

### Method `last_()`

Get the last job in the `queue`. if no more jobs, returns empty list

#### Usage

    GbifQueue$last_()

#### Returns

last job or empty list

------------------------------------------------------------------------

### Method `jobs()`

Get number of jobs in the `queue`

#### Usage

    GbifQueue$jobs()

#### Returns

(integer) number of jobs

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    GbifQueue$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
if (interactive()) { # dont run in automated example runs, too costly
x <- GbifQueue$new(
  occ_download(pred('taxonKey', "Q2M4"), pred("year", 1976)),
  occ_download(pred('taxonKey', "Q2M4"), pred("year", 2001)),
  occ_download(pred('taxonKey', "Q2M4"), pred("year", 2001), pred_lte("month", 8)),
  occ_download(pred('taxonKey', "Q2M4"), pred("year", 2004)),
  occ_download(pred('taxonKey', "Q2M4"), pred("year", 2005))
)
x
x$reqs
x$add_all()
x
x$jobs()
x
x$remove(x$reqs[[1]])
x
x$reqs[[1]]$run()
x$reqs[[1]]$result

# pre-prepared download request
z <- occ_download_prep(
  pred_in("basisOfRecord", c("HUMAN_OBSERVATION","OBSERVATION")),
  pred("hasCoordinate", TRUE),
  pred("hasGeospatialIssue", FALSE),
  pred("year", 1993),
  user = "foo", pwd = "bar", email = "foo@bar.com"
)
out <- GbifQueue$new(.list = list(z))
out
out$reqs
}} # }
```
