# soa-tables-collections

Schedule of Activities (SoA) transcriptions of clinical trial protocols, produced with the
[soa-tables](https://github.com/kerfors/soa-tables) pipeline and organised as collections of studies.

**Browse:** [kerfors.github.io/soa-tables-collections](https://kerfors.github.io/soa-tables-collections/) — the root
index links each collection index, and from there each protocol's review page, extraction log, consolidated view and
RDF.

## Origin

The inputs (SoA pages, extraction JSON, correction sidecars, extraction logs) were copied from
[soa2usdm-collections](https://github.com/kerfors/soa2usdm-collections) at `cdecda08`; everything derived was
regenerated with soa-tables. soa2usdm-collections is frozen and keeps the Towards CDISC outputs.

## Layout

```
register.csv                              # file of record per protocol: sha256, File IRI, source
collections/{collection}/
├── collection.json
├── studies_protocols.xlsx
└── protocols/
    ├── index.html                        # collection index (generated)
    └── {protocol}/
        ├── {protocol}_soa.pdf            # SoA pages excerpted from the protocol
        ├── {protocol}_soa_pages/         # rendered page images + pages.json
        └── soa-tables/
            ├── extracted/                # Layer 1: extraction JSON, corrections, extraction log, review page
            ├── resolved/                 # Layer 2
            ├── consolidated/             # Layer 3 + consolidation corrections sidecar
            └── rdf/{protocol}_facts.trig # transcription facts as RDF
```

Full protocol PDFs are not stored here. `register.csv` names each file of record (the posted protocol document) by
its sha256 and source address; the RDF identifies the file by the same hash. The RDF interface is described in
soa-tables [`documents/rdf-interface.md`](https://github.com/kerfors/soa-tables/blob/main/documents/rdf-interface.md).

## Manifest

`collections/{collection}/studies_protocols.xlsx`: sheet `studies` (`nct_id`, `sponsor`, `study_acronym`, `study_code`,
`therapeutic_area`, `excluded_reason`; usdm_data has `d4k_folder` in place of `sponsor`, and a collection may add
columns of its own, e.g. `document_file`) and sheet `protocols` (`nct_id`, `soa_pages`, `protocol_url`; `soa_pages`
may list several comma-separated ranges).

**`sponsor` is the sponsor as printed on the protocol document**, the file of record — the organisation name as the
document gives it, not the current lead sponsor in ClinicalTrials.gov / AACT, which can name a later owner
(NCT03739203: Allergan on the document, AbbVie in AACT). A sub-study whose document prints no sponsor takes the sponsor
its master protocol prints (the cpmp sub-studies of H0P-MC-CPMP). Where `collection.json` derives the sponsor instead
(usdm_data, from `d4k_folder`), this rule does not apply.

## RDF

One TriG file per protocol, holding one named graph (the protocol's transcription). The vocabulary is the SHACL file
[`schemas/rdf/soa-tables-facts.shacl.ttl`](https://github.com/kerfors/soa-tables/blob/main/schemas/rdf/soa-tables-facts.shacl.ttl)
in soa-tables. To load every protocol into one dataset (Python, rdflib), from the repository root:

```python
from pathlib import Path
from rdflib import Dataset

ds = Dataset()
for f in sorted(Path("collections").glob("*/protocols/*/soa-tables/rdf/*_facts.trig")):
    ds.parse(f, format="trig")
ds.serialize("soa-tables-facts.nq", format="nquads")  # optional: all protocols as one N-Quads file (about 64 MB)
```

## License

Derived content is shared under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) (see [LICENSE-CONTENT](LICENSE-CONTENT)). Any code in this repo is under the [MIT License](LICENSE). Source protocol documents remain the property of their respective sponsors. Full protocols are not redistributed here; the SoA page excerpts are included for review.
