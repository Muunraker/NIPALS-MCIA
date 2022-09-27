
<!-- README.md is generated from README.Rmd. Please edit that file -->

# nipalsMCIA: Software to Compute Multi-Block Dimensionality Reduction

<!-- badges: start -->
<!-- badges: end -->

This package computes Multiple Co-Inertia Analysis (MCIA) on multi-block
data using the Nonlinear Iterative Partial Least Squares (NIPALS)
method.

## Installation

This package currently can only be installed using
`devtools::install_github()`. A CRAN/Bioconductor version is in
progress.

You can install the development version of nipalsMCIA from
[GitHub](https://github.com/) with:

``` r
library(devtools)
devtools::install_github("Muunraker/nipalsMCIA", ref = "code-development",
                         force = TRUE, build_vignettes = TRUE)
library(nipalsMCIA)
```

## Basic Example

The package currently includes one test dataset: `data_blocks`. This is
a list of dataframes containing observations of variables from three
omics types (mRNA, proteins, and micro RNA) on 21 cancer cell lines from
the NCI60 cancer cell lines. The data file includes a `metadata` data
frame containing the cancer type associated with each cell line.

``` r
data(NCI60) # import data as "data_blocks" and metadata as "metadata_NCI60"

summary(data_blocks)
#>       Length Class      Mode
#> mrna  12895  data.frame list
#> miRNA   537  data.frame list
#> prot   7016  data.frame list

metadata_NCI60
#>               cancerType
#> CNS.SF_268           CNS
#> CNS.SF_295           CNS
#> CNS.SF_539           CNS
#> CNS.SNB_19           CNS
#> CNS.SNB_75           CNS
#> CNS.U251             CNS
#> LE.CCRF_CEM     Leukemia
#> LE.HL_60        Leukemia
#> LE.K_562        Leukemia
#> LE.MOLT_4       Leukemia
#> LE.RPMI_8226    Leukemia
#> LE.SR           Leukemia
#> ME.LOXIMVI      Melanoma
#> ME.MALME_3M     Melanoma
#> ME.M14          Melanoma
#> ME.SK_MEL_2     Melanoma
#> ME.SK_MEL_28    Melanoma
#> ME.SK_MEL_5     Melanoma
#> ME.UACC_257     Melanoma
#> ME.UACC_62      Melanoma
#> ME.MDA_MB_435   Melanoma
```

Note: this dataset is reproduced from the [omicade4
package](https://www.bioconductor.org/packages/release/bioc/html/omicade4.html)
(Meng et. al., 2014). This package assumes all input datasets are in
sample by feature format.

The main MCIA function can be called on `data_blocks` and optionally can
include `metadata_NCI60` for plot coloring by cancer type:

``` r
mcia_results <- nipals_multiblock(data_blocks, preprocMethod = 'colprofile',
                                  metadata = metadata_NCI60, coloring = "cancerType", 
                                  num_PCs = 10, tol = 1e-12)
```

<img src="man/figures/README-call-mcia-1.png" width="100%" />

Here `numPCs` is the dimension of the low-dimensional embedding of the
data chosen by the user.
