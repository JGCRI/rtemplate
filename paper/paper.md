---
title: 'rtemplate: Template to build R packages with GitHub actions and CI/CD, tests, codecov and documentation'

tags:
  - 
authors:
  - name: Zarrar Khan
    orcid: 0000-0002-8147-8553
    affiliation: 1
  - name: Chris R. Vernon
    orcid: 0000-0002-3406-6214
    affiliation: 1  
  - name: Mengqi Zhao
    orcid: 0000-0001-5385-2758
    affiliation: 2 
affiliations:
 - name: Joint Global Change Research Institute, Pacific Northwest National Laboratory, College Park, MD, USA
   index: 1
 - name: Pacific Northwest National Laboratory, Richland, MD, USA
   index: 2
date: 21 May 2023
bibliography: paper.bib
---

# Summary
`rmap` is an R package that allows users to easily plot tabular data (CSV or R data frames) on maps without any Geographic Information Systems (GIS) knowledge. Maps produced by `rmap` are `ggplot` objects and thus capitalize on the flexibility and advancements of the `ggplot2` package [@wickham_ggplot2_2011] and all elements of each map are thus fully customizable. Additionally, `rmap` automatically detects and produces comparison maps if the data has multiple scenarios or time periods as well as animations for time series data. Advanced users can load their own shapefiles if desired. `rmap` comes with a range of pre-built color palettes but users can also provide any `R` color palette or create their own as needed. Four different legend types are available to highlight different kinds of data distributions. The input spatial data can be either gridded or polygon data. `rmap` comes preloaded with standard country, state, and basin maps as well as custom maps compatible with the Global Change Analysis Model (GCAM) spatial boundaries [@Calvin:2019]. `rmap` has a growing number of users and its products have been used in multiple multisector dynamics publications [@wild_implications_2021; @wild_integrated_2021; @khan_future_2021]. `rmap` is also a required dependency in other R packages such as `rfasst` [@sampedro_rfasst_2021]. `rmap's` automatic processing of tabular data using pre-built map selection, difference map calculations, faceting, and animations offers unique functionality that makes it a powerful and yet simple tool for users looking to explore multi-sector, multi-scenario data across space and time.

# Statement of need
`rmap` is meant to help users having limited to no GIS knowledge use R for spatial visualization of tabular spatial data. `rmap` is not meant to be a replacement for spatial manipulation or cartographic software but focuses on the simple plotting of polygon and gridded data for spatio-temporal visualization of tabular data with a focus on comparing across scenarios and time periods. Several existing R packages such as tmap [@tennekes_tmap_2018], cartography [@giraud_cartography_2016], rworldmap [@south_rworldmap_2011], choroplethr [@lamstein_choroplethr_2020], sp [@pebesma_s_2005], and sf [@pebesma_simple_2018], have been developed to conduct spatial visualization and analytics in R without depending on external software such as ArcGIS [@esri_arcgis_2020], GRASS [@grass_development_team_grass_2020], or QGIS [@qgis_development_team_qgis_2021]. `rmap` enhances the following key capabilities which are limited in these existing packages:

1. **Pre-built maps**: Existing packages come with only a few examples of built-in maps as package data. `rmap` comes with a growing collection of  country, state, river basin, as well as other customized maps that are added into the package data based on user needs and requests. While built-in maps increase the size of the package, having direct access to these allows for automated searching and quick deployment of relevant shapefiles without the need to download any data. A list of pre-built maps in `rmap` can be found in the [Built-in Maps](https://jgcri.github.io/rmap/articles/vignette_map.html#maps) section of the user guide.
2. **Difference maps**: Existing packages do not produce difference maps to compare across scenarios or time periods. `rmap` provides this functionality by automatically recognizing multiple scenarios and time periods to produce difference maps across these dimensions. An important aspect of spatial data is exploring the difference between two scenarios or time periods and `rmap` makes this a seamless process.
3. **Post-process customization**: Existing packages do not produce output objects that can be saved and then customized. Customization of the maps in existing packages is limited to package specific functionality and arguments. `rmap` produces `ggplot` chart objects in which every element (axis, grids, titles, colors, line widths, facets) can all be customized after the map has been produced. This allows users to capitalize on existing knowledge of the widely-used `ggplot2` package and its functionality.

# Functionality

A detailed [User Guide](https://jgcri.github.io/rmap/articles/vignette_map.html) walks users step-by-step through all the available functionality of `rmap`. A simpler [Cheatsheet](https://jgcri.github.io/rmap/cheatsheet.pdf) is also provided to help users remember some of the key functionality in a single sheet. The following few examples demonstrate the simplicity of using `rmap`.

## Basic map

```
library(rmap)

data = data.frame(subRegion = c("China","India","Pakistan","Iran","Afghanistan"),
                  value = c(5,10,15,34,2))
map(data)
```

![Basic map plotted on data provided. `rmap` automatically chooses a country map based on the names in the 'subRegion' column in the data table.](mapCountries.png)

## Map with labels and underlayer

```
library(rmap)

data = data.frame(subRegion = c("CA","FL","ID","MO","TX","WY"),
                  value = c(5,10,15,34,2,7))
map(data, 
	underLayer = mapUS52Compact, 
	crop_to_underLayer = T, 
	labels = T)
```

![Map with chosen underLayer and labels for data provided. `rmap` automatically chooses the U.S. state map based on the names in the 'subRegion' column in the data table.](mapUScompact.png)

## Compare Scenarios

```
library(rmap)

data = data.frame(subRegion = c("Spain","Germany","Austria","Greece","Italy",
								"Spain","Germany","Austria","Greece","Italy",
								"Spain","Germany","Austria","Greece","Italy"),
                  value = c(5,10,15,34,2,
				           15,50,34,50,20,
						   1,2,7,13,5),
				  scenario = c("scen1","scen1","scen1","scen1","scen1",
							   "scen2","scen2","scen2","scen2","scen2",
							   "scen3","scen3","scen3","scen3","scen3"))
map(data,
	underLayer = "mapCountries",
	scenRef = "scen1",
	background = T)
```

![Maps showing absolute values for all three scenarios in data table.](mapScenarios.png)

![Maps showing absolute difference between chosen reference scenario ("scen1") and remaining scenarios ("scen2" and "scen3") in data table.](mapScenariosDiff.png)


# Acknowledgements
This research was supported by the US Department of Energy, Office of Science, as part of research in MultiSector Dynamics, Earth and Environmental System Modeling Program. The Pacific Northwest National Laboratory is operated for DOE by Battelle Memorial Institute under contract DE-AC05-76RL01830. The views and opinions expressed in this paper are those of the authors alone.

# References
