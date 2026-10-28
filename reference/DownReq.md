# DownReq

handles single requests for
[GbifQueue](https://docs.ropensci.org/rgbif/reference/GbifQueue.md)

## Public fields

- `req`:

  (list) internal holder for the request

- `type`:

  (list) type, one of "lazy" (to be lazy evaluated) or "pre" (run with
  `occ_download_exec` internal fxn)

- `result`:

  (list) holds the result of the http request

## Methods

### Public methods

- [`DownReq$new()`](#method-DownReq-new)

- [`DownReq$print()`](#method-DownReq-print)

- [`DownReq$run()`](#method-DownReq-run)

- [`DownReq$status()`](#method-DownReq-status)

- [`DownReq$clone()`](#method-DownReq-clone)

------------------------------------------------------------------------

### Method `new()`

Create a new `DownReq` object

#### Usage

    DownReq$new(x)

#### Arguments

- `x`:

  either a lazy object with an object of class `occ_download`, or an
  object of class `occ_download_prep`

#### Returns

A new `DownReq` object

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for the `DownReq` class

#### Usage

    DownReq$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `run()`

execute http request

#### Usage

    DownReq$run()

#### Returns

nothing, puts the http response in `$result`

------------------------------------------------------------------------

### Method `status()`

check http request status

#### Usage

    DownReq$status()

#### Returns

output of
[`occ_download_meta()`](https://docs.ropensci.org/rgbif/reference/occ_download_meta.md)

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    DownReq$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
if (FALSE) { # \dontrun{
res <- DownReq$new(occ_download_prep(pred("basisOfRecord", "LITERATURE"), 
  pred("year", "1956")
))
res
# res$run()
# res
# res$status()
# res$result
} # }
```
