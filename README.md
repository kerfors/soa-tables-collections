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

## License

Derived content is shared under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) (see [LICENSE-CONTENT](LICENSE-CONTENT)). Any code in this repo is under the [MIT License](LICENSE). Source protocol documents remain the property of their respective sponsors. Full protocols are not redistributed here; the SoA page excerpts are included for review.
