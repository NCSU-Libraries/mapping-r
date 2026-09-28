# Mapping in R workshop

One-hour NC State Libraries (Data Science Services) workshop: read campus spatial data with `sf`,
buffer each landmark, count trees, make a publication-quality map. Attendees download the repo as a
zip and work in the teaching `.qmd`, so everything in the repo ships to them.

## Two worksheets, kept in sync

- `mapping-in-r-workshop-complete.qmd` is the full version. `mapping-in-r-workshop-teaching.qmd` is
  the same document with some code replaced by `____` and a hint comment above each blank.
- Every prose or code edit goes into both files. Where the edit touches a blanked line, update the
  blank's hint instead of filling it in.
- Intended differences: the teaching file has its own subtitle, the "How to use this file" callout, and
  a guess-before-you-run prompt where the complete file states the result. Only the complete file has
  the facilitator-notes callout.
- After editing, `diff` the two files and confirm every difference is one of these.

## What the blanks are for

- Blanks are for what attendees will reuse on their own data: `st_as_sf()` arguments, `st_crs()`,
  `st_transform()`, `st_buffer()`, `st_intersects()`, and `geom_sf(data = ____)`. Each one is a
  decision (which layer, which radius, which order), with a hint comment above it.
- Styling is prefilled: colors, sizes, scales, scale bar, north arrow, titles. The one aesthetic blank
  is `aes(size = ____)` in §4 Step 2. Plain dplyr is prefilled too.
- In the map steps, blank only the layers that are new in that step.
- §1 is prefilled except for the `st_as_sf()` blanks in §1.5.
- Check: fill every blank with its answer and the code should match the complete file exactly.

## Rendering

- After any change to the complete `.qmd`, run `quarto render mapping-in-r-workshop-complete.qmd` and
  commit the `.html`. It is self-contained (`embed-resources`) and is committed on purpose.
- The teaching file cannot render while blanks are empty. Its `.html` is gitignored.

## Things that go stale silently

- Section references in prose are typed by hand (§1, §2.3, §4 …), not Quarto cross-refs. Adding,
  removing or reordering headings means checking them in both `.qmd` files, the facilitator timing
  table, and the README (which cites §1.2). Welcome and Setup are `{.unnumbered}` so content starts at
  §1. A `##` inside a `:::` callout is the callout's title, not a section.
- Results are typed into prose: Court of North Carolina 81 trees, Brickyard 14, the 50 m / 150 m
  comparison, the facilitator "punchline", the 1,217 → 209 buildings and 4,424 → 1,925 trees after
  clipping, the Z / dimension counts in §1.2, the 0.0026 ft false-easting gap in §2.3.1, and the
  feet demo in §3.2 (Court of North Carolina 0 trees at 100 ft). If the data, filters or buffer
  radius change, re-run and update them. Map titles are computed from `winner` and `radius`; keep them that way.

## Conventions

- README is plain language: no emoji, light emphasis, short sentences.
- Never commit `Rplots.pdf` or saved map PNGs (already gitignored).
