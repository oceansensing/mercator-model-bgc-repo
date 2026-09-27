# mercator-model-bgc-repo — the founding plan and running record

The Mercator **biogeochemistry**. Created on GitHub by the owner and given its documents on
2026-09-27, the day the owner asked for ECCOFS, CBEFS, Mercator's
biogeochemistry, RTOFS and GFS to be published without the map drawing them.
**Nothing is published yet.**

## What it is for

Seven **surface** fields from Copernicus Marine's global biogeochemistry
analysis and forecast, `GLOBAL_ANALYSISFORECAST_BGC_001_028`: chlorophyll-a,
pH, surface pCO2, dissolved oxygen, total alkalinity, nitrate and phosphate.

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

## Open

1. The fetcher, in the site's `scripts/`, and its self-test.
2. `pipeline/products.toml`, declaring only roots the site's contract
   publishes.
3. The publish workflow, its schedule offset from the siblings', and each
   product's `max_age_hours` measured from when the data really arrives.
4. The secrets only the owner can add: `PIPELINES_SSH_KEY` and the three
   `R2_*` organization secrets, and the two Copernicus Marine credentials.
