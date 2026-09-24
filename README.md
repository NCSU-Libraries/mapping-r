# Mapping in R

**Understanding spatial data and making a good map with `sf`**

A one-hour workshop from **NC State University Libraries — Data Science Services**.

We start with three real campus datasets and finish with one publication-quality map that answers a
question you can only ask of spatial data: **which spot on campus has the most trees around it?**

---

## ⬇️ Download the workshop files

### [**Click here to download everything (zip, ~1 MB)**](https://github.com/NCSU-Libraries/mapping-r/archive/refs/heads/main.zip)

That single link gives you the data, both versions of the worksheet, and the project file. You do not
need a GitHub account, and you do not need to know anything about GitHub.

Then:

1. **Unzip it.** You'll get a folder called `mapping-r-main`.
2. **Open `mapping-r.Rproj`** inside that folder. RStudio or Positron will launch with the working
   directory already set — which is what makes the file paths in the worksheet work.
3. **Open `mapping-in-r-workshop-teaching.qmd`** and follow along.

> **Unzip properly, don't peek inside the zip.** On Windows, double-clicking a zip shows you the
> contents without actually extracting them, and R can't read files that are still inside. Right-click
> the zip → **Extract All**. On a Mac, double-clicking is genuinely enough.

---

## Which file do I open?

| File | What it's for |
|---|---|
| **`mapping-in-r-workshop-teaching.qmd`** | **Start here.** The worksheet we use in the session. Some code is left blank (`____`) for you to fill in as we go. |
| `mapping-in-r-workshop-complete.qmd` | Every blank filled in. Use it if you fall behind, or as your reference afterwards. |
| `mapping-r.Rproj` | Open this first. Sets the working directory. |
| `data/` | All five datasets. Don't rename anything inside. |

---

## Before the workshop: install three packages

Run this once in the R console. It takes a few minutes, so please do it **before** the session rather
than during it:

```r
install.packages(c("sf", "dplyr", "ggplot2", "ggspatial", "readxl"))
```

- **`sf`** — the modern standard for vector spatial data (points, lines, polygons)
- **`dplyr`** — attribute wrangling; `sf` objects work with `filter()`, `mutate()`, `count()` directly
- **`ggplot2`** + **`ggspatial`** — mapping, scale bars, north arrows
- **`readxl`** — reads the `.xls` of building attributes

If a tutorial you find elsewhere loads `sp`, `rgdal`, `rgeos`, or `maptools`, it's out of date — those
were retired from CRAN at the end of 2023. Today's world is `sf`.

---

## What's in the data

| Dataset | Type | Source |
|---|---|---|
| `BLDGSCAMPUS.shp` | Polygons — building footprints | NC State Campus Planning & Strategic Investment |
| `NCSU_TreeInventory.gdb` | Points — 4,424 inventoried trees | NC State Campus Planning & Strategic Investment |
| `CAMPUSPERIMETER_ALL.shp` | Polygons — campus precinct boundaries | NC State Campus Planning & Strategic Investment |
| `NCStateBuildingsData.xls` | Table — building names, addresses | NC State Campus Planning & Strategic Investment |
| `NCState_places.csv` | Table — 13 campus landmarks as lat/lon | Compiled for this workshop |

### Data disclaimer — please read

The campus data is provided by **NC State University, Campus Planning & Strategic Investment**, and
ships with a disclaimer (`data/NCSU_TreeInventory/Disclaimer.txt`). Two things every participant
should understand: the data **may be incomplete or inaccurate**, and it should be used **for this
workshop only** — not for official, legal, or commercial purposes.

> NC State University makes every effort to produce and publish the most current and accurate content
> possible. However, the maps and data are produced for informational purposes and are NOT surveys.
> The information is compiled from various sources and not intended for official use or legal
> reference. The user of this site should not solely rely on the data provided herein. The information
> provided may not be used for commercial purposes or sold.

---

## What you'll be able to do by the end

1. **Explain what makes data "spatial"** — geometry, coordinate reference systems (CRS), and the fact
   that an `sf` object is *just a data frame with a geometry column*.
2. **Get your data into R** — shapefile, geodatabase, Excel attribute table, or a spreadsheet of
   coordinates.
3. **Ask a question only spatial data can answer** — buffer each landmark, count what falls inside,
   and find the shadiest spot on campus.
4. **Make a publication-quality map** you'd actually put in a poster or paper.

---

## Troubleshooting

**"cannot open data source" / "No such file or directory"**
You're in the wrong working directory. Run `getwd()`. The fix is almost always to open
`mapping-r.Rproj` and try again.

**"there is no package called 'readxl'"**
Run the `install.packages()` line above.

**`OGR: Corrupt data` / `Error: OGR error` partway through**
You skipped an `st_zm()`. Both the buildings and the tree layers carry an unused elevation
coordinate, and some spatial operations choke on it. The worksheet has `st_zm()` where it's needed —
see the callout in §1.2.

**Rendering the teaching file fails**
Expected, while any `____` is still unfilled — `____` isn't valid R. Run chunks one at a time with
the ▶ button instead. Render once everything's filled in.

---

## Going further

- **Geocomputation with R** — free online, the standard reference: <https://r.geocompx.org/>
- **`sf` documentation and vignettes** — <https://r-spatial.github.io/sf/>
- **r-spatial.org** — news and deeper dives from the maintainers

Questions, or want to talk about your own spatial data? Data Science Services offers consultations:
<https://www.lib.ncsu.edu/services/data-science>

---

## License

Workshop materials: see [`LICENSE`](LICENSE). The campus datasets remain the property of NC State
University, Campus Planning & Strategic Investment, and are redistributed here for workshop use only.
