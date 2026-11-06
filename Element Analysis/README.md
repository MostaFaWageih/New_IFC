# Element Analysis - element-level progress from the 31 Oct 2026 site walk

## Why this was made

The site walk of 31 Oct 2026 (Insta360 X3) produced 360° photos and 360° videos. This folder turns them into an
**element-by-element progress check against the IFC models**: for every photo spot and every video keyframe it shows
the real 360° view, the same view rendered from the combined IFC (structure + architecture), and a table with one row
per IFC element marked **Complete**, **In progress** or **Not started**, plus a final comment. The image is the main
subject; the video keyframes are the same kind of report, so a spot can be followed from a photo to the clips that
passed it.

## How to open it

| Open | What it is |
|---|---|
| [360 Images Elements/index.html](360%20Images%20Elements/index.html) | 10 photo spots (P01 to P10), one report each. **Start here.** |
| [360 Videos Elements/index.html](360%20Videos%20Elements/index.html) | 9 clips, one page per clip with a section per keyframe (21 keyframes). |
| [360 Images Elements/SUMMARY.md](360%20Images%20Elements/SUMMARY.md), [360 Videos Elements/SUMMARY.md](360%20Videos%20Elements/SUMMARY.md) | Totals, per-storey breakdown, page table, most/least advanced spots. |
| [elements_status.csv](elements_status.csv) | The combined element list: every judged IFC GUID with its IFC file, class, storey, status and the pages that show it. |
| [observations.csv](observations.csv), [comments.csv](comments.csv) | The judged statuses (one row per image and element) and the written comments. These are the source of everything above. |

Every report starts with the status tags (Structure and Architecture, each Complete / In progress / Not started),
then the image header, the real 360°, the IFC 360°, the element table, the "not visible" list, links to the same spot in
other photos and clips, and the final comment. Each report header links to the structure IFC and the architecture IFC
(both at the root of this repository) and to the combined element list. In the tables, "Also seen in" links the same element in other
photos and keyframes.

## Where the numbers stand

Snapshot of the build of 6 Nov 2026 (unique IFC elements). After any edit to `observations.csv`, the live numbers are
the tags on each page and the two `SUMMARY.md` files; this table is not regenerated.

| | Complete | In progress | Not started |
|---|---:|---:|---:|
| Structure | 6 | 27 | 13 |
| Architecture | 0 | 0 | 76 |

122 elements were judged in total. The 13 structure elements "not started" are the slab-on-grade level above the raft.
Everything seen so far sits at raft level (column cages, rebar mat, crane base) or on the GF slab formwork deck.

## Method

- **Positions are AI estimates.** Photo and keyframe positions and headings come from the earlier video/photo analysis
  (sun-heading based); the photo spots use the video-corrected positions. Confidence is low to medium everywhere.
- **Candidate elements:** every IFC element within 12 m in plan of the camera, up to 4 m above eye level, numbered by
  distance. The number is drawn on both 360° views at the element's bearing and height.
- **Statuses are judged by eye**, one image at a time, from the real view compared with the IFC view. They are not
  inferred by rule, and the older `Video_360_Analysis/element_status.csv` is not used.
- One element has one status for 31 Oct. If two images disagree, the build stops and names the GUID and the images.

## Status rules (my calls, change them in `observations.csv` if you disagree)

1. Concrete cast = **Complete**. Rebar fixed or formwork up = **In progress**. Nothing there yet = **Not started**.
2. A cast lift with starter bars at raft level is **In progress** (the column is not finished). A column that stands up
   to a slab-formwork deck is **Complete** (the starter bars then belong to the next storey).
3. **Not visible** (out of view, hidden or not identifiable at the estimated position) is listed per image but left out
   of the tags and the counts. Absence of a structural element at an estimated bearing is *not* recorded as "not
   started"; "not started" is kept for architectural and slab-on-grade levels where open air is seen.
4. Tags are split by discipline so architectural finishes on structural elements are not double counted.
5. Tag and summary counts use unique GUIDs, never sums over images.

## Limits

- **Low position confidence.** The bays look alike, so an element can be one bay (about 6-8 m) off its marker. Photos
  P03 to P05 do not line up well with the model renders, so only clear matches are marked.
- The video frames are stitched with ffmpeg; the stitching seam shows in some frames.
- **No baseline programme**, so the reports say what stands on site, not whether it is behind or ahead of plan.
- One capture date only, so there is no progress-over-time view yet.
- Statuses are an engineer's reading of images, not a survey.

## How to update

This folder holds the **finished results only**. The build tools, the plan and the judging working files are not part
of this repository; they stay in `Final_Models/Element Analysis` (`tools/`, `PLAN.md`, `_work/`). To change a status or a
comment: edit `observations.csv` / `comments.csv` there, run `python tools/build.py` from that folder, then copy the
rebuilt folders and files here again.

## Data that would improve the next report

1. **Baseline programme or planned dates per zone**, to say behind / on / ahead instead of only what stands.
2. **The next capture date**, to compare two dates and show change per element.
3. **Insta360 Studio stitched exports** of the clips, for cleaner frames without the ffmpeg seam.
4. **A few surveyed points, or a grid line marked in a photo**, to confirm camera positions and remove the one-bay
   uncertainty.
5. **The element or zone naming the team uses in progress meetings** (pours, zones, levels), so the table can use the
   same names.

## Files

`360 Images Elements/` and `360 Videos Elements/` are the reports (open `index.html`; each also has a `SUMMARY.md`).
`observations.csv` and `comments.csv` are the judged statuses and comments the reports are built from, and
`elements_status.csv` is the combined element list.
