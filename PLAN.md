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

## 2026-09-27 — built, and rehearsed end to end

**The fetcher** is the site's `scripts/fetch-mercator-bgc.py`, a sibling of
the physics fetcher that imports its tested helpers and holds its own
0.25-degree grid, so nothing here can move a physics product. Measured on the
first live run: each dataset opens in 4-12 s and a global surface frame reads
in about 1.3 s; all seven products took 35 s.

**The first live run refused two products, correctly and for the wrong
reason.** Range bounds set from open-ocean intuition refused real model
water at 4,871 mmol m-3 of alkalinity and 111 of nitrate — river mouths and
enclosed seas. The bounds were widened, and the check that catches a unit
fault became a band on each frame's MEDIAN, since alkalinity left in
mol m-3 reads 2.3, inside any wide range. Medians on 2026-09-27: chl 0.20
mg m-3, pH 8.036, pCO2 387 uatm, O2 257, alkalinity 2,349, nitrate 1.11,
phosphate 0.43 mmol m-3.

**Rehearsed through the orchestrator** in a throwaway copy of the site with
the seven roots added to its contract: `7 published file(s) match the
contract`, every fate `fresh`, `deploy=True`, a 39 MB tree, and
`schedule: {crons: [], longestGapHours: null}` — the dispatch-only state.

## Open

1. **Went live 2026-09-27** — the entry below.
2. **A day's frame is not refreshed when the service re-runs it.** Today's
   frame exists before the 03:30 UTC update (the axis runs ten days ahead),
   and the probe compares `refTime` only, so a run before the update
   publishes yesterday's forecast of today and later runs call it current.
   Worth a model-run stamp if a reader ever needs the newest forecast.
3. The secrets only the owner can add: `PIPELINES_SSH_KEY` and the three
   `R2_*` organization secrets, and the two Copernicus Marine credentials.

## 2026-09-27 — live

The owner added the secrets; the site's commit `d978a1b` put this
repository's roots in the contract and its origin in `MAP_ORIGINS`; the
dispatched run 36296048841 went green on its first try — build, Pages and R2 — and
`status/status.json` read, at 2026-09-27T05:04:30Z: every product `fresh`
(7 of 7), the nearest frame 5.08 h from the
reader, `contract: 1`. Each root was fetched from Pages
and served. The schedule, `37 4,10,16,22 * * *`, was then uncommented (longest gap
6 h, so the watchdog's silence budget is 10 h); the
first scheduled run is the next reading.

## The workflow's packages come from the site — 2026-09-27

The publish workflow installs `site/scripts/requirements-mercator.txt`, one file
per fetcher family, instead of naming packages in its own `pip install`
line. Dependabot reads requirements files and never a workflow line: an
inline pin elsewhere had carried `requests` 2.32.3, a version with two
advisories, unflagged. The site's `check:docs` now refuses an inline package
here. Confirmed by a dispatched run, green on build, Pages and R2.
