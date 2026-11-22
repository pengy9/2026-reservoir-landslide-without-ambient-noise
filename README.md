# 2026 Reservoir Landslide Without Ambient-Noise Precursors

Supplemental material and derived data for the manuscript:

> **Stiffness-silent sliding: a 10-m reservoir landslide without ambient-noise stiffness precursors**

This repository hosts all processed (derived) time series, station metadata, sensitivity tests, and the full Supplemental Material description used to produce the figures and results of the paper. **Raw waveforms are not included.**

---

## What is here

- **[`supplemental_material.md`](supplemental_material.md)** — full Supplemental Material (station metadata, processing parameters, sensitivity tests, all tables S1–S8).
- **[`data/`](data/)** — all derived data as CSV files.
- **[`figures/`](figures/) — `figS1_reservoir.png`** — reservoir-level drawdown vs. stiffness metrics.

## Data files (`data/`)

| File | Content | Rows |
|---|---|---|
| `station_metadata.csv` | Station positions (desensitized local easting/northing), elevation, f0, cover thickness | 6 |
| `f0_daily.csv` | Daily resonance frequency f0 and amplitude, 6 stations | ~1990 |
| `dvv_K_daily.csv` | Daily dv/v, correlation coefficient CC, decorrelation K, all station pairs | ~5385 |
| `dvv_pair_stats.csv` | Per-pair dv/v statistics (median, std, CC) | 15 |
| `gnss_daily.csv` | Daily GNSS displacement and rate, 7 stations | ~5056 |
| `eta_d_daily.csv` | Daily displacement-normalized energy index ηd and components | 23 |
| `microseismic_daily.csv` | Daily max acceleration and event counts, 3 accelerometers | ~283 |
| `Vs_sensitivity.csv` | Cover thickness H for Vs = 133–400 m/s | 6 |
| `reservoir_level.csv` | Three Gorges reservoir daily level and drawdown rate | 501 |
| `bootstrap_f0.csv` | Moving-block bootstrap of f0 (failure window vs. rest of year) | 6 |
| `environmental_noise.csv` | Reservoir level + soil moisture vs. K / dv/v / f0 | 501 |

## Coordinate desensitization

Absolute geographic (lon/lat) coordinates of the six seismometers are **withheld** to protect the engineering site. `station_metadata.csv` instead reports positions in a **local tangent-plane coordinate system** (easting/northing in meters relative to the array centroid). This preserves the relative geometry (inter-station distances, cover-thickness pattern) needed to reproduce the analysis, while not disclosing the exact location.

## Key result in one paragraph

A 9.85-m reservoir landslide (Daijiaping, Three Gorges, China) translated as a rigid block along a pre-existing weak plane and failed with **no change in resonance frequency (f0) or coda-wave velocity (dv/v)**, despite a five- to tenfold rise in microseismic activity. A displacement-normalized seismic-energy index (ηd) differs by ~280× between the peak-sliding day (1 June) and a localized-rupture day (7 June), showing that smooth sliding is nearly aseismic. The silent stiffness is the expected mechanical consequence of the slip mode, not a monitoring failure.

## How to cite

If you use these data, please cite the manuscript (citation to be added upon publication) and this repository.

## License

Data and code in this repository are provided for scientific reuse with attribution. Raw field data are subject to project confidentiality and are available only through a formal collaborative agreement with the corresponding author.
