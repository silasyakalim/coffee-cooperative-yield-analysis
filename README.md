# Coffee Cooperative Yield Analysis

Analysis of coffee delivery performance across three cooperatives in Côte d'Ivoire, evaluating how farmers' yields are distributed and how that distribution drives total delivered volume.

## Objectives

1. **Assess yield distribution** — determine how coffee yield is distributed across classes, and the share of farmers/volume in each class per cooperative.
2. **Analyze farmer distribution** — evaluate what percentage of farmers fall into each yield class.
3. **Measure volume contribution** — quantify each yield class's contribution to total coffee volume per cooperative.
4. **Identify performance trends** — compare cooperatives to highlight strengths and areas for improvement.

## Method

1. **Data cleaning** — removed duplicates, standardized column headings from French to English.
2. **Data integration** — merged traceability, mapping, and cooperative register data on the shared `Farmer Code` key.
3. **Data processing** — processed cooperative by cooperative (COOP1, COOP2, COOP3).
4. **Yield calculation** — yield = delivered volume (KG) / surface area. Where mapped surface area was missing, the declared surface area from the cooperative register was used as a fallback.
5. **Results & visualization** — farmers and volume were split into three yield classes:
   - `[0, 400]` — under-delivering
   - `[401, 800]` — delivering normally
   - `[801, ∞)` — over-delivering
6. **Discussion** — findings and commentary are in the notebook's final section.

## Key findings

- **Cooperative One**: heavily concentrated in the under-delivering class, with a small share performing normally or over-delivering.
- **Cooperative Two**: entirely under-delivering — no farmers in the normal or over-delivering classes, suggesting significant room for improvement.
- **Cooperative Three**: the most balanced distribution, with substantial contributions from both the normal and over-delivering classes.

See the notebook's "Analysis and discussion" section for the full breakdown, and "Comments" for a note on how including plantation polygon/geometry data would improve surface-area accuracy (and therefore yield accuracy) going forward.

## Repository structure

```
.
├── notebooks/
│   └── coffee_cooperative_yield_analysis.ipynb   # full analysis
├── data/
│   ├── raw/                                      # source registers (not committed, see below)
│   └── processed/                                # de-duplicated intermediate files (not committed)
├── requirements.txt
└── README.md
```

## Data

The source Excel registers (traceability data, mapping data, and each cooperative's producer register) contain personal data on individual farmers and are **not included in this repository**. To reproduce the analysis, place the following files under `data/raw/` (and `data/processed/` for the de-duplicated intermediates) using the filenames referenced in the notebook:

- `data/raw/traceability_data.xlsx`
- `data/raw/mapping_data.xlsx`
- `data/raw/registre_producteur_coop1.xlsx`
- `data/raw/registre_producteur_coop2.xlsx`
- `data/raw/registre_producteur_coop3.xlsx`
- `data/processed/cleaned_trace_data.xlsx`
- `data/processed/cleaned_mapping_data.xlsx`

> **Note:** the committed notebook retains its original run outputs (tables/charts), which include farmer names and codes from the source data, kept intentionally for this case study.

## Setup

```bash
pip install -r requirements.txt
jupyter notebook notebooks/coffee_cooperative_yield_analysis.ipynb
```
