<!-- README.md is generated from README.Rmd. Please edit that file and re-knit-->
<a rel="Exploration" href="https://github.com/BCDevExchange/docs/blob/master/discussion/projectstates.md"><img alt="Being designed and built, but in the lab. May change, disappear, or be buggy." style="border-width:0" src="http://bcdevexchange.org/badge/2.svg" title="Being designed and built, but in the lab. May change, disappear, or be buggy." /></a>

[![Travis-CI Build Status](https://travis-ci.org/bcgov/bcmaps.svg?branch=master)](https://travis-ci.org/bcgov/bcmaps)

------------------------------------------------------------------------

bcmaps
======

An [R](http://r-project.org) package of map layers for British Columbia

### Features

Various layers of B.C., such as administrative boundaries, natural resource management boundaries, etc. All layers are available as [sp](http://cran.r-project.org/web/packages/sp/index.html) objects, and are in [BC Albers](http://spatialreference.org/ref/epsg/nad83-bc-albers/) projection, which is the [B.C. government standard](https://www.for.gov.bc.ca/hts/risc/pubs/other/mappro/index.htm).

### Installation

The package is not available on CRAN, but can be installed using the [devtools](https://github.com/hadley/devtools) package:

``` r
install.packages("devtools") # if not already installed

library(devtools)
install_github("bcgov/bcmaps", build_vignettes = TRUE)
```

### Usage

At the moment, there are six layers available:

-   `bc_bound`: The provincial boundary of British Columbia (at 1:7.5M scale)

-   `regional_districts_analysis`: Detailed Regional District boundaries (Which are based on Canadian cencus boundaries). Suitable for situations where you need detailed boundaries (faithful to the original representation).

-   `regional_districts_disp`: Simplified Regional District boundaries. Much smaller file size than the analysis layer, suitable for situations where you don't need detailed boundaries, often useful when making maps for display.

-   `ecoprovinces`: Boundaries of B.C.'s ten ecoprovinces (<http://catalogue.data.gov.bc.ca/dataset/ecoprovinces-ecoregion-ecosystem-classification-of-british-columbia>)

-   `ecoregions`: Boundaries of B.C.'s 43 ecoregions (<http://catalogue.data.gov.bc.ca/dataset/ecoregions-ecoregion-ecosystem-classification-of-british-columbia>)

-   `airzones`: Boundaries of B.C.'s seven [Air Zones](http://www.bcairquality.ca/plans/national-air-quality-management-system.html), used for monitoring, reporting and taking action on air quality in British columbia (<http://catalogue.data.gov.bc.ca/dataset/british-columbia-air-zones>)

To load any of them, simply type `data(layer_name)`, where `layer_name` is the name of the layer of interest. Then you can use the data as you would any `sp` object. A couple of simple examples:

``` r
library(bcmaps)
#> Loading required package: sp

# Load and plot the boundaries of B.C.
data(bc_bound)
plot(bc_bound)
```

![](README-plot-maps-1.png)

``` r

## Next load the Regional Districts data, then extract and plot the Kootenays
data(regional_districts_disp)
kootenays <- regional_districts_disp[grep("Kootenay", 
                                          regional_districts_disp$region_name), ]
plot(kootenays)
text(coordinates(kootenays), 
     labels = kootenays$region_name, cex = 0.6)
```

![](README-plot-maps-2.png)
 There is also a simple function that returns the size of B.C. in hectares, square kilometres, or square metres. You can choose total area, land area only, or freshwater area only:

``` r
bc_area("total", "ha")
#> total_ha 
#> 94473500

bc_area("land", "m2")
#>     land_m2 
#> 9.25186e+11

bc_area("freshwater", "km2")
#> freshwater_km2 
#>          19549
```

#### Vignettes

We have written a short vignette on plotting points on one of the layers from `bcmaps`. You can view the vignette online [here](/vignettes/add_points.md) or if you installed the package using `devtools::install_github("bcgov/bcmaps", build_vignettes = TRUE)` you can open it using `browseVignettes("bcmaps")`.

### Project Status

Under active development, we will add different layers iteratively.

### Getting Help or Reporting an Issue

To report bugs/issues/feature requests, please file an [issue](https://github.com/bcgov/bcmaps/issues/).

### How to Contribute

Pull requests of new B.C. layers are welcome. If you would like to contribute to the package, please see our [CONTRIBUTING](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

### Source data

The source datasets used in this package come from various sources under open licenses, including [DataBC](http://data.gov.bc.ca) ([Open Government License - British Columbia](http://www.data.gov.bc.ca/local/dbc/docs/license/OGL-vbc2.0.pdf)) and [Statistics Canada](http://www.statcan.gc.ca/start-debut-eng.html) ([Statistics Canada Open Licence Agreement](http://www.statcan.gc.ca/eng/reference/licence-eng)). See the `data-raw` folder for details on each source dataset.

### License

The data and code in this repository is licensed under multiple licenses.

-   All R code in the `/R` directory and the `/data-raw` directory is licensed under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0.html). See LICENSE.Apache-2.0 in the appropriate directories.

-   Source data in `/data-raw/bc_bound` is licensed under the [Open Government License - Canada version 2.0](http://open.canada.ca/en/open-government-licence-canada). See LICENSE.Canada-OGL-2.0 in the appropriate directory.

-   Source data in `/data-raw/census-divisions_statscan` is licensed under the [Statistics Canada Open License Agreement](http://www.statcan.gc.ca/eng/reference/licence-eng). See LICENSE.StatsCan-OLA in the appropriate directory.

-   Source data in `/data-raw/ecoprovinces` is licensed under the [Open Government License - British Columbia version 2.0](http://www.data.gov.bc.ca/local/dbc/docs/license/OGL-vbc2.0.pdf). See LICENSE.OGL-vbc2.0.pdf in the appropriate directory.

-   Source data in `/data-raw/ecoregions` is licensed under the [Open Government License - British Columbia version 2.0](http://www.data.gov.bc.ca/local/dbc/docs/license/OGL-vbc2.0.pdf). See LICENSE.OGL-vbc2.0.pdf in the appropriate directory.

-   Source data in `/data-raw/airzones` is licensed under the [Open Government License - British Columbia version 2.0](http://www.data.gov.bc.ca/local/dbc/docs/license/OGL-vbc2.0.pdf). See LICENSE.OGL-vbc2.0.pdf in the appropriate directory.
