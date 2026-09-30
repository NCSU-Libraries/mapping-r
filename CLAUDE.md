# Mapping in R workshop

One-hour NC State Libraries (Data Science Services) workshop: a short intro to GIS, then read campus
spatial data with `sf`, buffer each landmark, count trees, make a publication-quality map. Attendees
download the repo as a zip and work in `mapping-in-r-workshop.qmd`, so everything in the repo ships to
them, apart from the files `.gitattributes` marks `export-ignore` (this file and `FACILITATOR.md`).

## One worksheet

- `mapping-in-r-workshop.qmd` is the only worksheet. It has no fill-in-the-blanks: all code is written
  out, and facilitators code examples live in the Console instead.
- Facilitator notes (timing, what to slow down for, live demos) live in `FACILITATOR.md`, not in the
  worksheet. Its section numbers are typed by hand, so check them when headings move.
- The hidden `final-map-image` chunk saves `images/final-map.png`, but only while rendering
  (`knitr.in.progress`), so attendees running chunks don't overwrite it.

## How each step is laid out

- Explanation comes before the chunk: what the function does, which arguments it wants, and what to
  look for in the output.
- After a chunk, only callouts titled "Gotcha: …" (`callout-warning`) or "Extra: …" (`callout-tip`).
- Code comments go on their own line above the code they describe, never at the end of a line. No
  alignment spaces in code (`x <- 1`, not `x   <- 1`).

## Section references

- In the worksheet, cross-references are Quarto links (`@sec-crs`), which render as "Section 3.3" and
  renumber themselves. A new reference needs a `{#sec-…}` id on its heading. Don't use `§`.
- Code comments can't hold links, so they name the section in words ("the map section").
- Welcome, "Find your way around RStudio" and Setup are `{.unnumbered}` so content starts at Section 1,
  and each `###` under them needs its own `{.unnumbered}`. A `##` inside a `:::` callout is the
  callout's title, not a section.

## Images

- Pictures live in `images/` and are committed. Every third-party one carries a credit in its caption:
  title, creator, source link, license. The README's "Pictures from other sources" table lists each
  one; keep it in step when a picture is added or swapped, because the repo's MIT license doesn't
  cover them.
- The Esri picture is used under Esri's noncommercial teaching terms, which require the "© Esri"
  notice on every copy. Saylor Academy asks that its book's original authors not be credited.
- `rstudio-panes-labeled.png` is our own screenshot with labels drawn on in R; `final-map.png` is made
  by the worksheet.

## Data

- `data/` holds edited copies of the campus files. The Z values are dropped from the buildings and from
  both tree layers. The buildings and campus boundaries are relabeled to the standard EPSG:2264; the
  originals' `.prj` had a false easting 0.0026 ft off, so they didn't `==` the trees. The unedited
  files are in the `original` tag. If the data is ever refreshed from Campus Planning, redo both edits,
  or the plain `layer[main_campus, ]` clip in Section 2.3 stops working.

## Rendering

- After any change to the `.qmd`, run `quarto render mapping-in-r-workshop.qmd` and commit the `.html`
  and `images/final-map.png`. The `.html` is self-contained (`embed-resources`) and is committed on
  purpose.
- GitHub Pages serves the repo at <https://ncsu-libraries.github.io/mapping-r/>. `index.html` redirects
  to the rendered `.html`, and `.nojekyll` stops Pages running Jekyll, which would try to process the
  `.qmd` file's YAML header. The README and the worksheet's "How to use this file" callout link to the
  Pages address.

## Things that go stale silently

- Results are typed into prose: Court of North Carolina 81 trees, Brickyard 14, the 50 m / 150 m
  comparison in Section 4, the 1,217 → 209 buildings and 4,424 → 1,925 trees after clipping in
  Section 2.3, the degree and foot coordinates in Section 3.3.1, the feet demo (Court of North
  Carolina 0 trees at 100 ft), and the 17 trees with no `dbh`. If the data, filters or buffer radius
  change, re-run and update them. Map titles are computed from `winner` and `radius`; keep them that
  way.
- Facts about places are checked, not remembered: the Brickyard is about an acre (45,240 sq ft).

## Conventions

- README is plain language: no emoji, light emphasis, short sentences.
- Never commit `Rplots.pdf` or saved map PNGs (already gitignored). `images/final-map.png` is the one
  exception.
