# Register a derived dataset for citation.

Register a derived dataset for citation.

## Usage

``` r
derived_dataset(
  citation_data = NULL,
  title = NULL,
  description = NULL,
  source_url = NULL,
  gbif_download_doi = NULL,
  user = NULL,
  pwd = NULL,
  curlopts = list(http_version = 2)
)

derived_dataset_prep(
  citation_data = NULL,
  title = NULL,
  description = NULL,
  source_url = NULL,
  gbif_download_doi = NULL,
  user = NULL,
  pwd = NULL,
  curlopts = list(http_version = 2)
)
```

## Arguments

- citation_data:

  (required) A data.frame with **two columns**. The first column should
  be GBIF **datasetkey uuids** and the second column should be
  **occurrence counts** from each of your datasets, representing the
  contribution of each dataset to your final derived dataset.

- title:

  (required) The title for your derived dataset.

- description:

  (required) A description of the dataset. Perhaps describing how it was
  created.

- source_url:

  (required) A link to where the dataset is stored.

- gbif_download_doi:

  (optional) A DOI from an original GBIF download.

- user:

  (required) Your GBIF username.

- pwd:

  (required) Your GBIF password.

- curlopts:

  a list of arguments to pass to curl.

## Value

A list.

## Usage

Create a **citable DOI** for a dataset derived from GBIF mediated
occurrences.

**Use-case (1)** your dataset was obtained with
[`occ_search()`](https://docs.ropensci.org/rgbif/reference/occ_search.md)
and never returned a **citable DOI**, but you want to cite the data in a
research paper.

**Use-case (2)** your dataset was obtained using
[`occ_download()`](https://docs.ropensci.org/rgbif/reference/occ_download.md)
and you got a DOI, but the data underwent extensive filtering using
`CoordinateCleaner` or some other cleaning pipeline. In this case be
sure to fill in your original `gbif_download_doi`.

**Use-case (3)** your dataset was generated using a GBIF cloud export
but you want a DOI to cite in your research paper.

Use `derived_dataset` to create a custom citable meta-data description
and most importantly a DOI link between an external archive (e.g.
Zenodo) and the datasets involved in your research or analysis.

All fields (except `gbif_download_doi`) are required for the
registration to work.

We recommend that you run `derived_dataset_prep()` to check registration
details before making it final with `derived_dataset()`.

## Authentication

Some `rgbif` functions require your **GBIF credentials**.

For the `user` and `pwd` parameters, you can set them in one of three
ways:

1.  Set them in your `.Renviron`/`.bash_profile` (or similar) file with
    the names `GBIF_USER`, `GBIF_PWD`, and `GBIF_EMAIL`

2.  Set them in your `.Rprofile` file with the names `gbif_user` and
    `gbif_pwd`.

3.  Simply pass strings to each of the parameters in the function call.

We strongly recommend the **first option** - storing your details as
environment variables - as it's the most widely used way to store
secrets.

You can edit your `.Renviron` with
[`usethis::edit_r_environ()`](https://usethis.r-lib.org/reference/edit.html).

After editing, your `.Renviron` file should look something like this...

GBIF_USER="jwaller"  
GBIF_PWD="fakepassword123"  
GBIF_EMAIL="jwaller@gbif.org"  

See [`?Startup`](https://rdrr.io/r/base/Startup.html) for help.

## References

<https://data-blog.gbif.org/post/derived-datasets/>
<https://www.gbif.org/derived-dataset/about>

## Examples

``` r
if (FALSE) { # \dontrun{
data <- data.frame(
 datasetKey = c(
 "3ea36590-9b79-46a8-9300-c9ef0bfed7b8",
 "630eb55d-5169-4473-99d6-a93396aeae38",
 "806bf7d4-f762-11e1-a439-00145eb45e9a"),
 count = c(3, 1, 2781)
 )

## If output looks ok, run derived_dataset to register the dataset
 derived_dataset_prep(
 citation_data = data,
 title = "Test for derived dataset",
 description = "This data was filtered using a fake protocol",
 source_url = "https://zenodo.org/record/4246090#.YPGS2OgzZPY"
 )

#  derived_dataset(
#  citation_data = data,
#  title = "Test for derived dataset",
#  description = "This data was filtered using a fake protocol",
#  source_url = "https://zenodo.org/record/4246090#.YPGS2OgzZPY"
#  )

## Example with occ_search and dplyr
# library(dplyr)

# citation_data <- occ_search(taxonKey="Q2M4", limit=20)$data %>%
#   group_by(datasetKey) %>% 
#   count()

# # You would still need to upload your data to Zenodo or something similar 
# derived_dataset_prep(
#   citation_data = citation_data,
#   title= "data downloaded for test",
#   description="This data was downloaded using rgbif::occ_search and was 
#   later uploaded to Zenodo.",
#   source_url="https://zenodo.org/record/4246090#.YPGS2OgzZPY",
#   gbif_download_doi = NULL,
# )
} # }
```
