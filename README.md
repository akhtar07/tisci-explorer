# TiSci Explorer

A read-only, static explorer for **TiSci**, an autonomous research agent for titanium alloys. TiSci reads the
titanium-alloy literature, builds a knowledge graph and a table of measured values, proposes hypotheses where the
graph has gaps, and tests them with DFT (MACE / VASP) and the ICME-lite multiscale chain.

**Live site:** https://akhtar07.github.io/tisci-explorer/

The site has seven sections:

| Section | What it shows |
|---|---|
| Overview | Corpus → graph → facts → hypotheses → verdicts, with the snapshot's counts |
| Worked example | One full loop for W in α-Ti: graph path, hypothesis, novelty check, DFT test, verdict, follow-up, DAMASK |
| Hypotheses | Every hypothesis with its critic score, novelty verdict, status, test results and prior art |
| Solute DFT map | Periodic-table view of single-solute changes in C11, C33, C44, c/a, volume and formation energy, plus every single, pair and triple run |
| ICME-lite cells | τ₀, yield and flow ratios against pure Ti per cell, with the critic codes and the known VPSC twin-mode defect |
| Literature facts | ~100k extracted values in 37 property tables, filterable, each linked to its source |
| Knowledge graph | Statistics and the 400 largest communities with their leading nodes |

## What is and is not published

* Every fact shows its value, unit, conditions and a DOI or landing-page link.
* The source sentence is quoted **only** when the paper carries a Creative Commons or public-domain licence.
  No full texts are published.
* Only the graph's statistics and its largest communities are included, not the full graph. Local file paths are
  stripped.
* Nothing on the site runs a model or a calculation. It is a snapshot; the date is in the page footer.

## Running locally

```
python3 -m http.server 8000     # then open http://127.0.0.1:8000/
```

The page fetches `data/*.json`, so it needs to be served over HTTP. Opening the file directly will not load the data.

## Regenerating the data

The data comes from TiSci's stored records via `scripts/export_site.py` in the TiSci repository. That script shares
its loaders with the paper's number generator (`scripts/gen_paper_tisci.py`), so the site and the paper report the
same numbers.

```
PYTHONPATH=src TISCI_DATA_ROOT=<data root> python scripts/export_site.py --out site
```

## Citing

Please cite the accompanying paper: Md Faiz Akhtar, Nilesh P. Gurao and Somnath Bhowmick, *TiSci: A
Literature-Grounded Agent That Decides What to Compute for α-Titanium, Running on a Validated, Self-Executing ICME
Chain* (under review; full reference to follow).
