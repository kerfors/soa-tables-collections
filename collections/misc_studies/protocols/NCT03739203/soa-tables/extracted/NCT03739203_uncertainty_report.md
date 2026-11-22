# NCT03739203 — uncertainty report (prompt v3.9.4)

## Decisions needed (2)

| # | where | call made | alternative | detail |
|---|---|---|---|---|
| D1 | doc p.85, Table_02 (source Table 4), whole table | Typed as a `track` labelled "COVID-19 Modified". It is an alternative schedule that applies only on a condition (COVID-19 disruption) and, per its title, only to randomized patients who have completed Visit 2. | Type it `domain` (same columns and same participants as Table 1) or `main_soa` (an amended version of the main schedule). Its columns would then join Table 1's with no separate population track. | 2.1 |
| D2 | doc p.85, Table_02 row 28 (Pharmacogenetic Consent), marker k | Footnote k ("Pharmacogenetic consent may be obtained ... may not be obtained remotely.") is printed below the table, but no `k` marker appears anywhere in the grid. It is bound to the Pharmacogenetic Consent row by text match (`method: text_match`), and `k` is added to that row's `annotation_markers`. | Record the location as `unresolved`, since the source prints no marker for k. | 2.4 |

## Recorded, not open (11)

- Table 1 (doc pp.16–17) is one printed table with a reprinted header on p.17, so it is extracted as one table. The reprinted header rows 30–34 are left out and keep their numbers (taxonomy **continuation** / "A page break inside ONE printed table"; §4 **row_position**).
- Table 1 typed `main_soa`: it is the primary anchor grid (§2).
- Pharmacogenetic Consent (T1 row 44, cols 3:7; T2 row 28, cols 4:7) and Pharmacogenetic Sample (T1 row 45, cols 3:7; T2 row 29, cols 4:7) each have a mark in a merged cell. The mark is spread across every column the cell covers, with `source_range` set (§5 **Merged marks — distribute, never centre**).
- In T2, columns 2 and 3 are each one grey cell merged vertically over all 25 activity rows, with rotated pointer text ("Refer to Global Protocol or Country-Specific Amendment for Visit 1 Procedures" / "... Visit 2 Procedures"). This text is emitted as the cell_value on every activity row in that column (50 entries, `method: visual_read`). Rules applied: §5 **Vertically-merged marks**, and §5 **Spanned values**: a pointer that covers only some columns keeps its span, and the whole-schedule exception does not apply.
- The T1 "Note: After completion of Visit 6/ET, ..." line below the frame becomes table-wide note `g1`. It names Visit 6/ET only as a reference point, so it is bound to no visit (§6 **Text above or below the frame**, **Binding by what a note names**).
- T1 markers a,b on Study Week "6" (col 7) and k on Study Week/Study Day col 2 and on Visit Windows col 3 are placed on those `schedule_grid` cells (§6 **Header-cell footnotes**).
- T2 marker `*` on the label "Study Day*" is recorded on the Study Day `schedule_property` row (the marker is printed on the row label) (§6).
- Visit Windows (T1 row 5) is typed `window` with `hierarchical_level` null (§3 **hierarchical_level**).
- Abbreviation blocks on doc pp.17 and 86 produce no annotations (§6 **Abbreviations are not annotations**).
- One label column (L=1), so the first data column is position 2. Data columns 2–8 are Visits 1, 2, 3, 4, 5, 6/ET, 7 in both tables (§5 **Leading label columns**).
- T2 "(X)" in the COVID-19 consent row is transcribed literally (§1, §5 **Qualified marks** / glyph literal).

## 1. Table_01 — source Table 1 "Schedule of Visits and Procedures" (doc pp.16–18)

- table_type `main_soa`. 7 data columns, 5 header rows, 36 activities, 111 marks (all `X`), 12 annotations (11 footnotes a–k plus g1).
- Activity rows per page: p.16 = 24 (rows 6–29); p.17 = 12 (rows 35–46); p.18 = 0. Doc p.18 holds only footnotes g–k, so no rows are expected there.
- Hierarchy: flat table, all rows level 0, no group headers.
- Merged spans: Pharmacogenetic Consent has X at col 2 plus X over 3:7. Pharmacogenetic Sample has X over 3:7. The Study Period band "Double-blind Treatment" spans 4:7.
- Name built from two printed lines: "Blood Alcohol Concentration (by" + "Breathalyzer)" → "Blood Alcohol Concentration (by Breathalyzer)".

## 2. Table_02 — source Table 4 "COVID-19 Modified Schedule of Visits and Procedures (Applicable to Randomized Patients who have completed Visit 2)" (doc pp.85–87)

### 2.1 Classification
- Same 7 visit columns as Table 1, but the title limits it to randomized patients who have completed Visit 2 under COVID-19 modifications. It is a schedule entered on a condition, not in sequence, so it is typed `track` (§2 track vs main_soa) with track_label "COVID-19 Modified". Domain/main_soa is the alternative (D1).
### 2.2 Counts
- 4 header rows (no Visit Windows row), 25 activities (rows 5–29, all from p.85).
- 130 `activity_schedule` entries: 75 `X`, 5 `(X)` and 50 pointer-text cells in cols 2–3.
- 13 annotations (`*`, a–l), all footnotes.
- Activity rows per page: p.85 = 25; p.86 = 0; p.87 = 0. Pages 86–87 hold only the `*` note, abbreviations and footnotes a–l.
### 2.3 Source is an image
- Doc p.85 has no text layer and no vector rules: it is one full-page raster.
- Activity names were transcribed visually (`activity_name_source.method: visual_transcription`, `indentation_method: visual_estimate`). Header values are `visual_read`. Marks are `raster_pixel_detection`. The pointer cells are `visual_read`.
- Footnote text comes from the text layer on pp.86–87.
- Recommend a spot-check of the resolved T2 grid against p.85.
### 2.4 Marker k not printed
- Footnote k is defined on p.86, but no `k` superscript appears in the grid. The Pharmacogenetic Consent row has no marker, and the row below carries `l`. The note is bound to Pharmacogenetic Consent by text match (D2).
- The probable cause is that the marker was omitted in the source, not a missing definition.
- The raw `cell_text` keeps the row as printed (no k).
### 2.5 Names
- "COVID-19 Informed Consent/Reconsent" + "(where applicable)" are joined into one name.
- "Pharmacokinetic Sample" + "(at any time during visit)" are joined into one name. These parentheticals are qualifiers, not section references, so they stay in `activity_name`.

## 3. Synthesised
- Annotation marker `g1` (T1, table-wide note below the frame): `schedule_property` row 1, `method: synthesized`.
- No synthesised property names.

## 4. Mechanical mark-check
- T1 (text layer, §1b): `pdftotext -bbox` mark tokens were binned to column centres taken from the Visit row (x = 290, 360, 429, 494, 559, 623, 687). Merged spans were checked against the vector vertical rules for each row: the internal boundaries 3|4 to 6|7 are missing only on the two Pharmacogenetic rows. This matches the visual read cell for cell, with 0 disagreements.
- T2 (image, §1a/§1d): rules were recovered from the 200 dpi raster. Vertical rules at x = 711, 898, 1098, 1283, 1462, 1641, 1821, 2000 px. Horizontal rules come from the label column: 30 bands, of which 4 are header and 25 are body. The detector counted near-black pixels (<90) per cell with a threshold of about 60. A mark cell scores 71–123; an empty cell scores 0, or 3–24 where an adjacent merged X glyph overlaps. Merged spans were confirmed by the absence of vertical rules over x 1098–1821 in both Pharmacogenetic bands. Cols 2–3 have no horizontal rules over the body, which confirms the vertical merge. The detector was validated against the visual read on every body row (dense: Vital Signs/C-SSRS; sparse: Clinical Laboratory Tests/HAM-A), with 0 disagreements.

## 5. Annotation text integrity
- The text layer is not glyph-spread, and no private-use or U+2011 characters were found.
- T1 h/i and T2 k/l have very similar text (pharmacogenetic consent/sample) but sit in different tables. Within each table, no annotation text contains another.
- The markdown agrees with the PDF text for T1 and the footnotes. The markdown for p.85 is OCR garbage, so it was ignored and the PDF image is authoritative.

## 6. Orphan risk
- T2 k: placed by text match (D2). No other orphans: every annotation has at least one location, and every location's marker is in its row's `annotation_markers`.

## 7. Method provenance
- T2 activities: `visual_transcription` / `visual_estimate` (25 rows).
- T2 schedule_grid: `visual_read` (28 cells).
- T2 activity_schedule: `raster_pixel_detection` (80 mark cells), `visual_read` (50 pointer cells).
- T2 annotation k location: `text_match`.
- T1 g1 location: `synthesized`.
- No `unresolved` locations.
