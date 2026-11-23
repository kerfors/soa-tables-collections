# NCT02701985 — Uncertainty report (PDF_TO_JSON_PROMPT v3.9.4)

## Decisions needed (0)

| # | where | call made | alternative | detail |
|---|---|---|---|---|

None. Every judgement call in this extraction is decided by a stated rule (next block).

## Recorded, not open (11)

- §2 **Tables — classify before extracting**: one table, `main_soa`. Doc p.91 ("Appendix 1 Schedule of Assessments (cont.)") is the footnote table for p.90. Its rows are the numbered notes 1-8 keyed to markers in the grid, so they are extracted as annotations, not as a table (taxonomy, `reference` note).
- §5 **Leading label columns are excluded**: L = 1 (activity-name column, which also carries the header-row labels "Visit" / "Days"). The first data column is position 2. Data columns run 2-9.
- §5 **Vertically-merged marks** + §5 **Merged marks — distribute, never centre**: rows 34 (Adverse Event or Intercurrent Illness) and 35 (Previous and Concomitant Treatments) share one data cell. Its rule lines enclose columns 2-9 and both rows: the label column has its own rule at y=576.1, but the data area has no internal vertical or horizontal rule between y=557.7 and 597.8. The single 'x' goes on both rows × columns 2-9, `source_range` "2:9" (16 entries).
- §3 **Header bands — typing** / §3 **property_type**: row 1 is an unlabelled band. Its only value, "Treatment Period", is merged across positions 4-7 (Week 2 to Week 12). Typed `epoch`. The blank cells over Screening, Baseline, Follow-Up and Early Termination stay "" (§5 **Empty cells**).
- §3 synthesised name: row 1 `property_name` "Epoch", synthesised, `structure_method: inferred_from_layout`.
- §3 **Header cells over several rows** / qualifier: the Days row keeps the printed window inside each cell ("14 (± 7)") and the "(NA)" for Early Termination. No separate window row was created.
- §3 **hierarchical_level**: Epoch 1, Visit 2, Days 3. The Days values do not follow from the visit labels (the Screening and Baseline ranges cannot be derived from them), so the row is not nulled.
- §6 **Header-cell footnotes**: Baseline¹ → marker "1" on the `schedule_grid` cell (row 2, col 3). Visit⁸ sits on the row label, so marker "8" goes on the `schedule_property` row 2.
- §6 **annotation_type**: footnote 4 points ("see Section 4.6.1.3.4.") and also explains, so it stays a `footnote`. All 8 annotations are `footnote`.
- §4 **Hierarchy — printed signals only**: the table is flat. Every label is Arial Bold 7 pt at the same x (109.6), with no indent and no shading. All rows are level 0 (`indentation_method: assumed_flat`).
- §1c **Symbol-font glyphs**: header cells use U+2010 hyphens ("‐28 to ‐8", "Follow‐Up") and no-break spaces. They are written as '-' and ' '.

## Per table

**Table 01**: `main_soa`, "Appendix 1 Schedule of Assessments", doc pp. 90-91.
- 9 columns: 1 label column plus 8 data columns (Screening, Baseline, Week 2, Week 6, Week 9, Week 12, Follow-Up Visit, Early Termination Visit).
- 3 header rows, 32 activities, 130 marks, 8 annotations.
- Activity rows per page: p.90 = 32; p.91 = 0. Page 91 is the footnote table, with notes 1-8 only and no activity rows. This is expected, not a skipped page.

## Merged-mark decisions

- Rows 34 and 35, columns 2:9: one 'x' in a cell that is merged both vertically and horizontally, distributed to both rows (see Recorded).
- Header: "Treatment Period" merged 4:7 (`merged_cell_range` "4:7" on each covered grid cell).

## Synthesised

- `property_name` "Epoch" (row 1).
- No synthesised annotation markers. Every note has a printed numeric marker.

## Mechanical mark-check

- Method: §1b bbox column-binning. `pdftotext -bbox` mark tokens (`^[Xx]…`) were binned to the header x-centres. Row bands came from the vector horizontal rule lines (the page has full vector rules; all vertical and horizontal rules were extracted with pymupdf drawings).
- Result: matches the visual read cell for cell on rows 4-33, which hold 114 marks.
- One disagreement, resolved by rule-line geometry: the bbox binned the single merged 'x' (glyph at y 575-582, straddling the label-column rule) to row 35 col 6 only, and nothing to row 34. The rule lines show one cell spanning rows 34-35 × cols 2-9, so the final grid has 16 marks there.
- Footnoted marks tokenise as a separate superscript token ('x' + '5', 'x' + '7'). They were reattached as cell markers at (24,8), (24,9) and (33,7).
- Glyph case: all marks are lowercase 'x'. The Screening mark on ECG - 12 Lead is in Arial rather than Calibri and renders slightly larger, but it is still 'x' in the text layer, so it was transcribed as 'x'.

## Annotation text integrity

- The text layer is not glyph-spread, so no reconstruction was needed.
- Note text comes from the ruled footnote table on p.91. Each note is one rule-bounded cell.
- The markdown renders note 1 with italic-underscore artefacts ("the_last_baseline_assessment_"). The PDF text layer reads "the last baseline assessment." and that is what the JSON holds.
- No containment or overlap pairs between notes.

## Low-confidence calls / PDF–markdown disagreements

- Markdown places the merged 'x' under Week 9 for "Previous and Concomitant Treatments" only, and leaves "Adverse Event or Intercurrent Illness" empty. The PDF rule lines show a 2-row × 8-column merged cell, and the PDF is followed.
- Markdown splits "MSG biopsy (optional sub-" / "study only)" across two rows. The PDF shows one ruled label cell, joined per §4 **Whitespace** as "MSG biopsy (optional sub-study only)".
- The Baseline column (Days -7 to -1) lies outside the "Treatment Period" band. This is transcribed as printed.

## Orphan risk

- None. Every annotation has at least one `marker_location`, and every location's marker is present in that row's `annotation_markers` (checked by script).

## Method provenance

- Row 1 `structure_method: inferred_from_layout` (unlabelled band typed from its spanning value).
- `indentation_method: assumed_flat` on all 32 activities.
- No `unresolved` locations, no proximity-bounded text, and no visual-read or raster cells.
