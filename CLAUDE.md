# Mapping in R workshop

One-hour NC State Libraries (Data Science Services) workshop: a short intro to GIS, then read campus
spatial data with `sf`, buffer each landmark, count trees, make a publication-quality map. Attendees
download the repo as a zip and work in the teaching `.qmd`, so everything in the repo ships to them.

## Two worksheets, kept in sync

- `mapping-in-r-workshop-complete.qmd` is the full version. `mapping-in-r-workshop-teaching.qmd` is
  the same document with a few CRS calls replaced by `____` and a hint comment above each blank.
- Every prose or code edit goes into both files. Where the edit touches a blanked line, update the
  blank's hint instead of filling it in.
- Intended differences: the teaching file has its own subtitle and the "How to use this file" callout.
  Only the complete file has the facilitator-notes callout and the hidden `final-map-image` chunk.
- After editing, `diff` the two files and confirm every difference is one of these.

## What the blanks are for

- The only blanks are the six in §3.3 and §3.4: `st_crs()` for the buildings and the landmarks,
  `st_transform()` for the same two, and the `==` check on the `_m` layers. Each has a hint comment
  above it.
- Everything else is prefilled. The session explains each function and its arguments instead.
- Check: fill every blank with its answer and the code should match the complete file exactly, apart
  from the hint comments.

## How each step is laid out

- Explanation comes before the chunk: what the function does, which arguments it wants, and what to
  look for in the output.
- After a chunk, only callouts titled "Gotcha: …" (`callout-warning`) or "Extra: …" (`callout-tip`).
- Code comments go on their own line above the code they describe, never at the end of a line.

## Images

- Pictures live in `images/` and are committed. Every one except `final-map.png` carries a credit in
  its caption: title, creator, source link, license. The README's "Pictures from other sources" table
  lists each one; keep it in step when a picture is added or swapped, because the repo's MIT license
  doesn't cover them.
- The Esri picture is used under Esri's noncommercial teaching terms, which require the "© Esri"
  notice on every copy. Saylor Academy asks that its book's original authors not be credited.
- `images/final-map.png` is the finished map shown under "Where we're headed". The hidden
  `final-map-image` chunk rewrites it on every render of the complete file, so commit it with the `.html`.

## Data

- `data/` holds edited copies of the campus files. The Z values are dropped from the buildings and from
  both tree layers. The buildings and campus boundaries are relabeled to the standard EPSG:2264; the
  originals' `.prj` had a false easting 0.0026 ft off, so they didn't `==` the trees. The unedited
  files are in the `original` tag. If the data is ever refreshed from Campus Planning, redo both edits,
  or the plain `layer[main_campus, ]` clip in §2.3 stops working.

## Rendering

- After any change to the complete `.qmd`, run `quarto render mapping-in-r-workshop-complete.qmd` and
  commit the `.html` and `images/final-map.png`. The `.html` is self-contained (`embed-resources`) and
  is committed on purpose.
- The teaching file cannot render while blanks are empty. Its `.html` is gitignored.
- GitHub Pages serves the repo at <https://ncsu-libraries.github.io/mapping-r/>. `index.html` redirects
  to the complete `.html`, and `.nojekyll` stops Pages running Jekyll, which would try to process the
  `.qmd` files' YAML headers. The README links to the Pages address.

## Things that go stale silently

- Section references in prose are typed by hand (§1, §2.3, §4 …), not Quarto cross-refs. Adding,
  removing or reordering headings means checking them in both `.qmd` files, the "Where we're headed"
  list, the facilitator timing table, and the README (which cites §3). Welcome, "Find your way around
  RStudio" and Setup are `{.unnumbered}` so content starts at §1, and each `###` under them needs its
  own `{.unnumbered}`. A `##` inside a `:::` callout is the callout's title, not a section.
- Results are typed into prose: Court of North Carolina 81 trees, Brickyard 14, the 50 m / 150 m
  comparison in §4, the 1,217 → 209 buildings and 4,424 → 1,925 trees after clipping in §2.3, the
  degree and foot coordinates in §3.3.1, the feet demo (Court of North Carolina 0 trees at 100 ft),
  and the 17 trees with no `dbh`. If the data, filters or buffer radius change, re-run and update
  them. Map titles are computed from `winner` and `radius`; keep them that way.

## Conventions

- README is plain language: no emoji, light emphasis, short sentences.
- Never commit `Rplots.pdf` or saved map PNGs (already gitignored). `images/final-map.png` is the one
  exception.
