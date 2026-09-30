# Mapping in R

A one-hour workshop from NC State University Libraries, Data Science Services.

The session starts with a short introduction to GIS. Then you will read several kinds of spatial data
into R, ask one question of it, and make a map you could put in a poster or a paper. The question: which
spot on campus has the most trees around it?

**Read the worksheet online: <https://ncsu-libraries.github.io/mapping-r/>**

That is the finished version, with every map already drawn. You can read it or share it without
installing anything. To run the code yourself, download the files below.

## Download the files

**[Download everything as a zip](https://github.com/NCSU-Libraries/mapping-r/archive/refs/heads/main.zip)**

You do not need a GitHub account.

1. Unzip it. You will get a folder called `mapping-r-main`.

   On Windows, right-click the zip and choose **Extract All**. Double-clicking a zip shows you what is
   inside without extracting it, and R cannot read files that are still in the archive. On a Mac,
   double-clicking is enough.

2. Open the folder in your editor:

   | Editor | How to open it |
   |---|---|
   | RStudio | Double-click `mapping-r.Rproj`. |
   | Positron | Open Positron first, then **File > Open Folder** and choose `mapping-r-main`. Double-clicking the `.Rproj` does not reliably launch Positron. |

   Either way, R points at the project folder. That is what makes the file paths in the worksheet work.

3. Open `mapping-in-r-workshop.qmd` and follow along.

## Files in this folder

| File | What it is |
|---|---|
| `mapping-in-r-workshop.qmd` | The worksheet we use in the session. All the code is written for you. Start here. |
| `mapping-in-r-workshop.html` | The same worksheet, already run. Open it in a browser to read the whole thing and see the finished maps without running any code. It is also online at the link above. |
| `mapping-r.Rproj` | Project file. Sets the working directory. Positron users open the folder instead. |
| `data/` | The five datasets. Do not rename anything inside. |
| `images/` | The pictures in the worksheet. Each one is credited where it appears. |

## Install the packages first

The worksheet installs anything missing when you run it, but `sf` can take several minutes to build.
Run this before the session rather than during it:

```r
install.packages(c("sf", "dplyr", "ggplot2", "ggspatial", "readxl"))
```

- `sf` handles vector spatial data: points, lines, polygons
- `dplyr` for the attributes; `sf` objects work with `filter()`, `mutate()` and `count()` directly
- `ggplot2` and `ggspatial` for the map, the scale bar and the north arrow
- `readxl` reads the `.xls` of building attributes

Older tutorials load `sp`, `rgdal`, `rgeos` or `maptools`. Those were retired from CRAN at the end of
2023. Use `sf` instead.

## The data

| File | Type | Source |
|---|---|---|
| `BLDGSCAMPUS.shp` | Polygons: building footprints | NC State Campus Planning & Strategic Investment |
| `NCSU_TreeInventory.gdb` | Points: 4,424 inventoried trees | NC State Campus Planning & Strategic Investment |
| `CAMPUSPERIMETER_ALL.shp` | Polygons: campus precinct boundaries | NC State Campus Planning & Strategic Investment |
| `NCStateBuildingsData.xls` | Table: building names and addresses | NC State Campus Planning & Strategic Investment |
| `NCState_places.csv` | Table: 13 campus landmarks as lat/lon | Compiled for this workshop |

Three of the files are lightly edited copies of the campus originals. We removed the elevation (Z)
values from the building footprints and the tree inventory. We also gave the buildings and the campus
boundaries the standard EPSG:2264 definition of their coordinate system, which the tree inventory
already used. Nothing else changed.

### Data disclaimer

The campus data comes from NC State University, Campus Planning & Strategic Investment, and ships with
a disclaimer at `data/NCSU_TreeInventory/Disclaimer.txt`. The data may be incomplete or inaccurate, and
it is for this workshop only. Do not use it for official, legal or commercial purposes.

> NC State University makes every effort to produce and publish the most current and accurate content
> possible. However, the maps and data are produced for informational purposes and are NOT surveys. The
> information is compiled from various sources and not intended for official use or legal reference.
> The user of this site should not solely rely on the data provided herein. The information provided
> may not be used for commercial purposes or sold.

## Troubleshooting

**"cannot open data source" or "No such file or directory"**
R is in the wrong working directory. Run `getwd()` to see where it thinks it is. Opening
`mapping-r.Rproj`, or the folder in Positron, usually fixes it.

**"there is no package called 'readxl'"**
Run the `install.packages()` line above.

## Going further

- Geocomputation with R, free online: <https://r.geocompx.org/>
- `sf` documentation and vignettes: <https://r-spatial.github.io/sf/>
- r-spatial.org for news from the maintainers

## Before you go

Tell us how the workshop went: [workshop evaluation](https://go.ncsu.edu/dss-workshop-eval)

Questions about this workshop, or about programming in general? Reach out through
[Get Data Help](https://go.ncsu.edu/getdatahelp). Send an email, make an appointment, or reserve a
workstation.

## License

Workshop materials: see [LICENSE](LICENSE). The campus datasets remain the property of NC State
University, Campus Planning & Strategic Investment, and are redistributed here for workshop use only.

### Pictures from other sources

Most pictures in `images/` come from other sources. They are not covered by this repo's MIT license.
Each one keeps its own license, and the worksheet credits it where it appears.

| File | Source | License |
|---|---|---|
| `gis-layers.jpg` | Figure 1.8, *Essentials of Geographic Information Systems*, Saylor Academy (2012) | CC BY-NC-SA 3.0 |
| `points-lines-polygons.jpg` | Figure 4.8, *Essentials of Geographic Information Systems*, Saylor Academy (2012) | CC BY-NC-SA 3.0 |
| `buffers.jpg` | Figure 7.1, *Essentials of Geographic Information Systems*, Saylor Academy (2012) | CC BY-NC-SA 3.0 |
| `spatial-join.jpg` | Figure 7.5, *Essentials of Geographic Information Systems*, Saylor Academy (2012) | CC BY-NC-SA 3.0 |
| `geographic-vs-projected.png` | ArcGIS Pro documentation, "Coordinate systems, map projections, and transformations" | © Esri, used under Esri's terms for noncommercial teaching |
| `intersects.png` | *Introduction to PostGIS*, ch. 11, Paul Ramsey, Mark Leslie and PostGIS contributors | CC BY-SA 3.0 |
| `left-join.gif` | Garrick Aden-Buie, tidyexplain | CC0 |
| `sf-horst.jpg` | Artwork by Allison Horst, stats-illustrations | CC BY 4.0 |

`final-map.png` is made by the worksheet itself, and `rstudio-panes-labeled.png` is our own screenshot.
Both are covered by the MIT license like the rest of the repo.
