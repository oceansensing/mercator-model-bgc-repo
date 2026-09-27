# mercator-model-bgc-repo

The Mercator **biogeochemistry** — a data repository of the oceansensing ocean map system: its own
Pages site, its own schedule, its own gigabyte, holding no code of its own.

**Nothing is published yet** (2026-09-27). `PLAN.md` is the founding plan;
`CLAUDE.md` carries what must not be got wrong and the shared doc doctrine.

## What it will publish

Seven **surface** fields from Copernicus Marine's global biogeochemistry
analysis and forecast, `GLOBAL_ANALYSISFORECAST_BGC_001_028`: chlorophyll-a,
pH, surface pCO2, dissolved oxygen, total alkalinity, nitrate and phosphate.

These products are published **operationally but not drawn on the website's
map** — the owner's call, 2026-09-27. The map's status line still reports
them when they fall behind, which is how their health stays visible.

## Where the data comes from

**Source, read 2026-09-26/27** (`copernicusmarine describe`, toolbox 2.4.1,
no login): five daily datasets, `cmems_mod_glo_bgc-{pft,car,co2,bio,nut}_anfc_0.25deg_P1D-m`,
dataset version 202311. A regular **0.25°** global grid, latitude −80 to 90
(681 rows) by 1,440 columns; 50 depth levels whose first is 0.494 m; a daily
time axis running about ten days past today, updated around 03:30 UTC on the
one day read. `spco2` is two-dimensional and in pascals. The ARCO geo-series
chunks are one time, one depth, 681 × 1,440 — one frame is one chunk, the
shape the Mercator fetcher's chunk guard accepts. Access is the sibling
repositories' own: the `copernicusmarine` toolbox and the organization's
Copernicus Marine credentials.

## How it will run

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository will carry `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Sibling repositories of the same model:
`mercator-model-currents-repo` and `mercator-model-fields-repo`.

**Which document gets what, and what "update docs" means across all
seventeen repositories, is the doctrine block at the top of `CLAUDE.md`** —
the same text in all seventeen, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
```
