# NCT04304508 — uncertainty report (prompt v3.9.4)

## Decisions needed (4)

| # | where | call made | alternative | detail |
|---|---|---|---|---|
| D1 | p.12, Table 1 header row 2 "(Duration)" | Typed as "other": it is a duration line that also carries the "Early termination (ET)" sub-band over Visit 12a. It gets hierarchy level 2 because that cell sets Visit 12a apart within the Intervention period. | Type it as "period" (Early termination is a sub-period of the Intervention period). Or treat it as a duration qualifier that restates the periods, with no hierarchy level (null). | 3.1 |
| D2 | p.12, Table 1 header row 5 "Week [W] / Study day and allowed deviations" | One ruled row, kept as one header row typed "week". Each cell value holds both printed lines (e.g. "W2 15±4", "SCR -2 → 1"). | Split it into two header rows: a "week" row (SCR, RND/W0, W2 …) and a "study_day" row with the windows (-2 → 1, 1, 15±4 …). | 3.1 |
| D3 | p.12, Table 1 header row 4 "Visit type" | Typed as "modality" (site / phone) and given hierarchy level 4. | No hierarchy level (null). Visit number alone tells every column apart, and the visit type is an attribute of the visit. | 3.1 |
| D4 | p.15, Table 2, unmarked paragraph below the frame (g1) | "The exact times of PK, PD and biomarker sampling need to be recorded …" is a table-wide note. It names sample types, not visits or columns. | Bind it to the rows it names: PK, PD, Biomarkers Plasma and Biomarkers Serum (not Genetics), by text match. | 3.2 |

## Recorded, not open (16)

- §2 **reference test first / subsidiary vs track**: Table 1–1 is typed `subsidiary`. It gives finer pre- and post-dose timing for Table 1's PK, PD, biomarker and pharmacogenetic sampling rows, and Table 1 footnote l points to it.
- Taxonomy **continuation** ("A page break inside ONE printed table is not a continuation"): doc pp.12–13 are one table. The header is reprinted on p.13 and has no caption of its own.
- §1b **De-duplicate repeated rows**: the reprinted header rows on p.13 (row positions 25–29) are left out and the other rows are not renumbered.
- §5 **Leading label columns**: L = 1 for both tables. Data columns start at position 2. Table 1 uses positions 2–15 (Visits 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 12a, 13). Table 2 uses positions 2–7.
- §5 **Merged marks / Arrows spanning columns**: Adverse events (row 18) and Outcome events (row 19) are each one merged cell over columns 3–15 (no internal vertical rules). The cell holds "←=== continuously ===→". It is distributed to 13 columns with `source_range` "3:15". The arrow head stops short of the right edge of column 15, but the rule lines decide the span. The run of "=" characters is collapsed to "← continuously →".
- §3 **Header cells over several rows**: the label cell "Study periods / (Duration)", the Screening cell and the Safety Follow-up cell each span header rows 1–2. Each is split by printed line, or recorded on row 1. Covered cells hold "".
- §5 merged header cells: "Intervention period" spans 3:14, "(from RND until … 52 weeks)" spans 3:13, and Table 2's "Week 4 (Visit 4)" spans 3:5. All are confirmed from the vector rule lines.
- §6 **Header-cell footnotes**: Table 1 markers a (Screening, col 2), b (Early termination, col 14), g (Visit 4, col 5) and c (row 5, col 15) sit on their grid cells. In Table 2, marker a sits on each covered position of the merged Week 4 cell (3, 4, 5), d on col 7, b on cols 5 and 6, and c on col 6.
- §6 **annotation_type**: footnote l ("Refer to Table 1–1 …") is a bare pointer, so it is typed `source_note`. Footnotes f, h, m and Table 2 e cite sections but also explain, so they stay `footnote`.
- §6 **Abbreviations are not annotations**: both abbreviation blocks yield zero annotations.
- §6 **Text above or below the frame / Binding by what a note names**: Table 2's unmarked paragraph gets synthesised marker g1, table-wide (the open call is D4).
- §1 visual formatting: the grey-printed X marks in the Early termination column (12a) are transcribed as X. Grey-shaded cells in Table 2 are empty.
- §5 **Glyph case**: Table 2 mixes X and x. Both are transcribed literally and not normalised. Table 1 row 37, col 13 has a smaller-font X, recorded as X.
- §1c **Symbol-font glyphs**: Wingdings private-use code points are restored. U+F028 becomes ☎, U+F0AE becomes →, and U+F0DF / U+F0E0 become ← / →.
- §4 **Hierarchy — printed signals only**: full-width shaded bands (Administrative procedures, Clinical procedures / assessments, IxRS, Laboratory assessments, Study drug administration) are level 0 and mark-free. All other rows are level 1. The Laboratory assessments group stays open across the page break, so the PK, PD, PGx and biomarker rows on p.13 are level 1. Table 2 is flat (`assumed_flat`).
- §4 **Whitespace**: "Biomarke" + "rs Plasma" becomes "Biomarkers Plasma" (a word broken by a narrow column joins with no space). "Stud drug m collection and accountability" keeps the source typo "Stud".

## 1. Per table

**Table 1** — `main_soa`, "Schedule of Activities (SoA)". The title is taken from the section heading 1.3, since no caption is printed. Doc pp.12–13. 5 header rows, 14 data columns, 27 activity rows (5 of them are mark-free group bands), 109 activity_schedule entries, 14 annotations.
- Rows per page: p.12 → 19 rows (rows 6–24). p.13 → 8 rows (rows 30–37).
- Footnotes a–g are printed on p.13 below the frame, and h–n on p.14. p.14 has no table rows, so `page_end` = 13.

**Table 2** — `subsidiary`, "Table 1–1 PK, PD and Biomarker Sampling". Doc p.15. 2 header rows, 6 data columns, 5 activity rows (all on p.15), 16 activity_schedule entries, 6 annotations.

## 2. Merged-mark decisions
- Table 1 rows 18 and 19 (Adverse events, Outcome events): "← continuously →" over columns 3–15 (Visits 2–13).
- There are no other merged body cells. bMRI cells (row 20: "A,B (-2→+3)", "A (±7)", "A,B (±7)", "A,B (+7)") are single ruled cells, and each window is kept in `cell_value`. Row 36, col 13 "no intake" is transcribed as text.

## 3. Synthesised / low-confidence

### 3.1 Table 1 header structure
- Row 2 is named "Duration", with "(Duration)" kept as `cell_value`. It mixes the Intervention period duration text (3:13), "Early termination (ET)" (col 14) and the Safety Follow-up duration "(14 days after EOT or ET)" (col 15, the second printed part of the SFU cell). Typing and level → D1.
- Row 5: one ruled row with two printed lines per cell → D2.
- Row 4: modality, level 4 → D3.

### 3.2 Table 2
- The two header rows have empty label cells. Their names are synthesised: "Week" (row 1, typed by the spanning "Week 4 (Visit 4)" value, with visit numbers kept as qualifiers) and "Timepoint" (row 2). Both have `structure_method: inferred_from_layout`.
- Synthesised annotation marker: g1 (the table-wide paragraph below the frame, underlined in source) → D4.

## 4. Mechanical mark-check
- Method: `pdftotext -bbox` column binning (§1b). All pages have a text layer and vector rule lines; there is no raster page. Column centres come from the Visit number header row (Table 1) and the timepoint header (Table 2). Mark tokens matched `^[Xx]…$`, and superscript markers are separate tokens. Merged spans were checked against the vector vertical rules for each row.
- Result: Table 1 has 78 X tokens. With the 4 bMRI text cells, 1 "no intake" and 2 merged arrow cells (×13), that makes 109 entries. Table 2 has 16 X/x tokens. The bbox matrix matched the visual read cell for cell, with **0 disagreements**.

## 5. Annotation text integrity
- The text layer is not glyph-spread, so nothing was reconstructed.
- No annotation text is contained in another.
- Every note is bounded by its printed marker paragraph. There is no notes column.
- Footnote f's three printed paragraphs are joined with single spaces.
- Footnote m keeps the source's mismatched quotes (“study intervention’).

## 6. Orphan risk / source anomalies
- **Visit 4 header marker g (p.12)**: the superscript g on Visit number "4" points to footnote g (ECG machine), which does not fit a visit header. It is recorded as printed on row 3, col 5. The p.13 reprint has no marker on Visit 4. This is a probable source defect.
- **Marker c on the 12-lead ECG screening cell** (row 16, col 2): footnote c is about the safety follow-up phone call, which does not fit an ECG screening mark. It is recorded as printed. This is a probable source defect.
- **"(SCR)*" on the p.13 reprinted header** instead of "(SCR)a": the "*" has no definition printed in the source. That header is a reprint and is not recorded, so no annotation was emitted. The p.12 marker a is the one used.
- Footnote i reads "within 72 after randomization" (the unit is missing in source). It is transcribed as printed.
- No annotation lacks a location. All markers in `marker_locations` also appear in the row's `annotation_markers`.

## 7. Method provenance
- `activity_name_source.indentation_method = font_signal` on all Table 1 activities (level from shaded bold bands). `assumed_flat` on all Table 2 activities.
- `schedule_property.structure_method = inferred_from_layout` on Table 2 rows 1 and 2.
- `marker_locations.method = synthesized` on Table 2 g1 (schedule_property row 1).
- No `unresolved` locations. No proximity, raster or visual-read methods were used.
- PDF/markdown disagreements: the markdown splits "deviations" into its own row, misreads arrow glyphs and drops the marker g on Visit 4 in places. The PDF was followed throughout.
