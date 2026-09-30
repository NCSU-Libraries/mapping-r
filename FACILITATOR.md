# Facilitator notes: Mapping in R

For whoever teaches the session. This file is left out of the attendee zip. Section numbers match
the headings in `mapping-in-r-workshop.qmd`.

## One-hour timing

Budget about 50 minutes of content and 10 for questions and install triage.

| Min   | Section                                                                  |
|------:|--------------------------------------------------------------------------|
| 0–5   | Welcome, where we're headed, orientation, start the Setup chunk          |
| 5–12  | Section 1: A short introduction to GIS                                   |
| 12–24 | Section 2: Get four files in (`.shp`, `.gdb`, `.xls`, `.csv`), look, clip |
| 24–32 | Section 3: What makes data spatial in R                                  |
| 32–40 | Section 4: Explore, then the spatial question (buffer and count)         |
| 40–52 | Section 5: Making the map                                                |
| 52–55 | Section 6: Checklist for your own data (skim it; it's for later)         |
| 55–60 | Wrap-up, resources, questions                                            |

## Notes

**Start the Setup chunk early.** Installing `sf` can take several minutes, so have everyone run it
during the orientation. It can finish while you talk through Section 1.

**Live demos, no pictures:** the paper-around-a-globe idea in Section 1.4 (a sheet of paper and a ball
or globe), and in the orientation, where the Outline panel is and what the Source | Visual switch does.

**Code live in the Console.** Nothing in the worksheet is blank. When a question comes up, try it
together in the Console rather than editing the worksheet, so everyone's copy keeps running.

**Slow down for the CRS**, both the idea in Sections 1.3–1.4 and the hands-on part in Sections
3.3–3.4. Most later headaches trace back to it.

**Section 2 is the tight spot.** Four file formats is a lot of reading-in before anybody sees a map.
Don't live-type it. Run the chunks and talk over them. One stop is worth the time: the before-clipping
map in Section 2.3. Ask the room what's wrong with it before you open the gotcha under it.

**If you run long,** Section 4's buffer table is the part that has to survive, because Section 5's
map is *about* that result. The map of all the circles in Section 4.2 is the first thing to cut,
and the feet demo after it is the second. Section 6 can be left for people to read afterwards.

**Before class:** confirm the data folder downloads and reads on the room's setup. Ask everyone to
run `install.packages(c("sf", "dplyr", "ggplot2", "ggspatial", "readxl"))` beforehand.
