# Convert GBIF Backbone taxon keys to COL Extended Release keys

Convert GBIF Backbone taxon keys to COL Extended Release keys

## Usage

``` r
gbif_to_col(
  key,
  checklistKey = "7ddf754f-d193-4cc9-b351-99906754a03b",
  curlopts = list(http_version = 2)
)
```

## Arguments

- key:

  (integer or character) One or more GBIF Backbone numeric taxon keys to
  convert to COL Extended Release alpha-numeric keys. Can be a single
  value or a vector of values.

- checklistKey:

  (character) The key of the COL checklist to use. Defaults to COL
  Extended Release. Generally should not need to change this.

- curlopts:

  A list of curl options passed on to
  [`httr::GET()`](https://httr.r-lib.org/reference/GET.html).

## Value

A list containing the full API response for each input key. Each element
includes:

- `gbif_key` - The input GBIF Backbone key

- `usage` - The matched COL taxon usage details (including the COL key)

- `classification` - Full taxonomic classification path

- `diagnostics` - Match quality information (matchType, confidence,
  etc.)

- `additionalStatus` - Additional status information (e.g., IUCN status)

- `synonym` - Whether the match is a synonym

If only one key is provided, returns an object of class `gbif_to_col`
with a custom print method. If multiple keys are provided, returns an
object of class `gbif_to_col_list`. The full API response data is always
accessible in the returned list structure.

## Details

This function uses the GBIF species matching API with the
`scientificNameID` parameter to resolve GBIF Backbone taxonomy keys to
COL Extended Release keys. This is useful when migrating existing code
from numeric GBIF Backbone keys to the new COL XR alpha-numeric keys.

## References

<https://techdocs.gbif.org/en/openapi/v2/species>

## Examples

``` r
if (FALSE) { # \dontrun{
# Convert a single GBIF Backbone key to COL XR
result <- gbif_to_col(5231190)  # Calopteryx splendens

# The print method shows a clean summary:
# <<GBIF to COL key conversion>>
#   GBIF Backbone key: 5231190
#   COL Extended Release key: Q2M4
#   Scientific name: Calopteryx splendens
#   Rank: SPECIES
#   Match type: EXACT
#   Confidence: 100

# Access the full data structure:
result$usage$key                # COL XR key: "Q2M4"
result$usage$name               # Scientific name
result$classification           # Full taxonomic hierarchy
result$diagnostics$matchType    # Quality of match
result$diagnostics$confidence   # Confidence score

# Convert multiple keys at once
results <- gbif_to_col(c(5231190, 2435099, 2877951))
results  # Shows summary for all matches

# Extract specific data from multiple results:
sapply(results, function(x) x$usage$key)  # Extract all COL keys
sapply(results, function(x) x$usage$name) # Extract all names
} # }
```
