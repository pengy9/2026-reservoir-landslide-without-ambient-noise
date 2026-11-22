# Supplemental Material

**Stiffness-silent sliding: a 10-m reservoir landslide without ambient-noise stiffness precursors**

This repository is the Supplemental Material accompanying the manuscript. It contains all derived time series (as CSV files in [`data/`](data/)), one figure, and the full description of station metadata, processing parameters, and sensitivity tests. Raw waveforms are **not** included.

- Data files: [`data/`](data/)
- Figure: [`figures/figS1_reservoir.png`](figures/figS1_reservoir.png)

---

## S1. Station Metadata and Instrumentation

Six three-component short-period nodal seismometers (5 Hz natural frequency, 250 Hz sampling, 24-bit) recorded continuously on and around the Daijiaping landslide from October 2025 to October 2026. Seven GNSS stations recorded surface displacement from October 2024, and three accelerometers recorded ground acceleration.

To protect the exact engineering coordinates, absolute geographic coordinates are withheld. [`data/station_metadata.csv`](data/station_metadata.csv) reports station positions in a local tangent-plane coordinate system (easting/northing in meters relative to the array centroid), which preserves the relative geometry required to reproduce the cover-thickness inversion and inter-station distances. Elevations are reported to the nearest 0.1 m.

**Table S1.** Station metadata (positions desensitized to local coordinates) — see [`data/station_metadata.csv`](data/station_metadata.csv).

| Station | Easting (m) | Northing (m) | Elevation (m) | f0 (Hz) | H (Vs=295 m/s, m) |
|---|---|---|---|---|---|
| 5200272 | −197.6 | −3.4 | 220.5 | 3.17 | 23.2 |
| 5200326 | −37.5 | 180.8 | 273.8 | 6.22 | 11.9 |
| 5200309 | 7.6 | −16.2 | 211.1 | 3.47 | 21.3 |
| 5200291 | 155.4 | 50.7 | 227.1 | 8.87 | 8.3 |
| 5200314 | −82.6 | −199.8 | 176.4 | 8.12 | 9.1 |
| 5200298 | 172.8 | −49.2 | 204.1 | 2.90 | 25.4 |

---

## S2. Data Processing Parameters

### S2.1. Resonance frequency f0 (HVSR)

- Raw records were streamed from the 512-byte file header and 17076 blocks/file (72-byte block header + 1000 samples of 24-bit big-endian), sampled at 250 Hz; time is GPS week-seconds minus the 18 s leap-second offset, converted to Beijing time (UTC+8).
- Spectral windows: 30 s (7500 samples), detrended (mean removed) and tapered with a Hanning window, zero-padded to NFFT = 16384.
- Quiet-window selection (two stages): windows whose vertical-component power in 0.5–8 Hz exceeded 4× the day's quietest-decile band power were rejected; the noisiest 10% by total RMS were then discarded.
- Only daytime windows (08:00–16:00 Beijing time) were retained.
- Konno–Ohmachi smoothing with b = 40 applied to each horizontal/vertical power spectrum; daily H/V ratios stacked frequency-by-frequency using the median (robust stacking).
- f0 picked as the global maximum of the stacked H/V within 0.5–20 Hz; amplitude A0 taken at f0. Daily f0 time series used in Figure 4 are provided in [`data/f0_daily.csv`](data/f0_daily.csv).

### S2.2. Coda-wave velocity change dv/v and decorrelation K

- Daily cross-correlation functions (CCF) computed between the Z-component records of the six nodes (15 station pairs, 88–434 m), band-pass filtered 5–40 Hz, stacked over full 24-h days (30 s windows, spectral whitening applied).
- dv/v estimated by the stretching method over the coda, relative to the median reference CCF of the entire period.
- Decorrelation K = 1 − CC with the reference; only station-pair days with CC ≥ 0.4 were retained for dv/v and K.
- Full daily dv/v, CC, and K for all pairs are in [`data/dvv_K_daily.csv`](data/dvv_K_daily.csv); per-pair statistics in [`data/dvv_pair_stats.csv`](data/dvv_pair_stats.csv).

### S2.3. Displacement-normalized energy index ηd

- ηd = ⟨v²⟩ / Δd, where ⟨v²⟩ is the daily mean of squared horizontal ground velocity over all valid 30 s windows of the six nodes (each window contributes mean(v²), i.e., RMS²), and Δd is the daily GNSS displacement increment of the fastest station (GP05SX). Using the mean rather than the sum makes ηd robust to data gaps.
- Data coverage: all six nodes recorded the full 17280 windows (6 × 2880) on both 1 June and 7 June 2026 (and on every day of the failure window except the last, 12 June, with 14986 windows), so the ηd contrast is not a coverage artifact.
- Physical basis and units: ⟨v²⟩ is proportional to the radiated seismic-energy density E_s/T_eff = 4πρcR² (∫v²dt)/T_eff, because ∫v²dt ≈ (Σ v²)·Δt with constant window length Δt = 30 s, and ρ, c, R are constant across the failure window; ηd therefore has units of m/s² and is proportional to the radiated energy per unit displacement. Daily values in [`data/eta_d_daily.csv`](data/eta_d_daily.csv).

### S2.4. Cover-thickness inversion

- H = Vs / (4 f0), with Vs = 295 m/s for the colluvial mantle (reference value; sensitivity in S4.1).

---

## S3. Derived Data Files

All derived time series used to generate the figures are provided as CSV files in [`data/`](data/). Raw waveforms are not included.

**Table S3.** Derived data files.

| File | Content |
|---|---|
| [`station_metadata.csv`](data/station_metadata.csv) | Station metadata (desensitized local coordinates, elevation, f0, H) |
| [`f0_daily.csv`](data/f0_daily.csv) | Daily resonance frequency f0 and amplitude (6 stations) |
| [`dvv_K_daily.csv`](data/dvv_K_daily.csv) | Daily dv/v, CC, and decorrelation K (all station pairs) |
| [`dvv_pair_stats.csv`](data/dvv_pair_stats.csv) | Per-pair dv/v statistics (median, std, CC) |
| [`gnss_daily.csv`](data/gnss_daily.csv) | Daily GNSS displacement and rate (7 stations) |
| [`eta_d_daily.csv`](data/eta_d_daily.csv) | Daily ηd and its components |
| [`microseismic_daily.csv`](data/microseismic_daily.csv) | Microseismic statistics (accelerometer maxima and event counts) |
| [`Vs_sensitivity.csv`](data/Vs_sensitivity.csv) | Cover-thickness sensitivity to Vs |
| [`reservoir_level.csv`](data/reservoir_level.csv) | Three Gorges reservoir daily level and rate |
| [`bootstrap_f0.csv`](data/bootstrap_f0.csv) | Moving-block bootstrap of f0 (failure window vs. rest of year) |
| [`environmental_noise.csv`](data/environmental_noise.csv) | Environmental (hydrologic) variables vs. noise metrics |

---

## S4. Sensitivity Tests

### S4.1. Cover-thickness sensitivity to Vs

The absolute cover thickness scales linearly with the assumed Vs; the spatial pattern and relative thickness contrasts are independent of Vs. [`data/Vs_sensitivity.csv`](data/Vs_sensitivity.csv) reports H for Vs = 133–400 m/s.

### S4.2. Reservoir-level drawdown and hydrologic disturbance

The failure occurred during the annual Three Gorges reservoir drawdown: the level fell 13.1 m (161.8 → 148.7 m) over the failure window (20 May–7 June 2026), which is the inferred trigger. Figure S1 shows that, despite this rapid drawdown, f0 and dv/v remained flat through the failure and showed no seasonal hydrologic response across the year, ruling out a hydrologic masking of any stiffness precursor. Daily reservoir levels are project-monitored data provided in [`data/reservoir_level.csv`](data/reservoir_level.csv).

**Figure S1.** Reservoir-level drawdown versus stiffness metrics. (A) Daily Three Gorges reservoir level; the failure window (shaded) coincides with a 13.1 m drawdown. (B) Daily f0 for the six nodes, flat throughout. (C) dv/v (median ± IQR of pairs), indistinguishable from zero. See [`figures/figS1_reservoir.png`](figures/figS1_reservoir.png).

### S4.3. dv/v statistics for all station pairs

[`data/dvv_pair_stats.csv`](data/dvv_pair_stats.csv) reports dv/v statistics for all 15 station pairs; the daily scatter (std 0.03–0.07%) sets the measurement precision quoted in the main text.

### S4.4. Statistical tests and detection limits

Table S4 reports a Mann-Whitney U test comparing the failure-window (20 May–7 June) f0 against the rest of the year, together with the detection limit (2σ) set by the daily scatter. None of the six stations shows a significant f0 shift (p > 0.05), and the failure-window effect size is ≤2%, far below the reported precursor amplitudes (−24% to −30%).

**Table S4.** Mann-Whitney U test of f0 (failure window vs. rest of year).

| Station | f0 median (Hz) | failure-window (Hz) | p (MWU) | effect size (%) | daily std (%) | detection 2σ (%) |
|---|---|---|---|---|---|---|
| 5200272 | 3.17 | 3.12 | 0.712 | −1.8 | 4.8 | 9.6 |
| 5200326 | 6.11 | 6.01 | 0.525 | −1.8 | 9.4 | 18.7 |
| 5200309 | 3.47 | 3.47 | 0.283 | 0.0 | 5.3 | 10.6 |
| 5200291 | 8.87 | 8.87 | 0.546 | 0.0 | 5.4 | 10.8 |
| 5200314 | 7.98 | 8.12 | 0.072 | 1.8 | 5.2 | 10.4 |
| 5200298 | 2.90 | 2.90 | 0.271 | 0.0 | 2.7 | 5.4 |

For dv/v, the failure-window median (−0.01%) does not differ from the yearly median (p = 0.206), and the detection limit is 0.14% (2σ of the pair-level daily scatter, 0.07%).

Because the daily f0 series is serially autocorrelated, the Mann-Whitney p values above are optimistic (they assume independent samples). We therefore repeated the failure-window comparison with a moving-block bootstrap (block length 7 d, 2000 resamples) that preserves the serial correlation: all six stations remain non-significant (p = 0.62–0.95), and the effective sample size (first-order-autocorrelation correction) is 0.3–0.8 of the nominal daily count. The conclusion of no significant f0 shift is robust to this autocorrelation. Full bootstrap output (observed difference, p value, null-distribution quantiles, lag-1 autocorrelation, effective sample size) is in [`data/bootstrap_f0.csv`](data/bootstrap_f0.csv).

### S4.5. Frequency-domain decomposition of the f0 peak

To verify that f0 is the fundamental (first) mode of the cover layer rather than a higher mode or noise, we applied single-station frequency-domain decomposition (FDD; Häusler et al., 2019) to the three-component 30 s windows (daytime 08:00–16:00, 960 windows per day, 5 May 2026). At f0, the first singular vector is dominated by the horizontal components at all six stations (H/V = 4.6–17), consistent with the S-wave resonance of a soft layer over a stiffer basement, and the first singular value is well separated from the second (σ1/σ2 up to 16), indicating a single resolvable mode (Table S5). The array spacing (100–370 m) is too large to image spatial mode shapes, so the attribution is based on polarization rather than spatial coherence; an independent cover-thickness constraint (drilling) would further confirm it.

**Table S5.** Single-station FDD at f0: modal separation (σ1/σ2) and horizontal-to-vertical polarization of the first mode.

| Station | f0 (Hz) | σ1/σ2 at f0 | H/V at f0 |
|---|---|---|---|
| 5200272 | 3.17 | 1.79 | 9.25 |
| 5200326 | 6.22 | 1.48 | 7.03 |
| 5200309 | 3.47 | 15.91 | 7.51 |
| 5200291 | 8.87 | 3.75 | 5.35 |
| 5200314 | 8.12 | 3.55 | 17.16 |
| 5200298 | 2.90 | 2.13 | 4.60 |

### S4.6. Picking bandwidth and double-peak stations

The f0 time series in Figure 4A uses narrowband tracking (±20% around the yearly robust-stack f0), not the global maximum over 0.5–20 Hz. At two stations (5200272 and 5200309) the H/V curve has two comparable peaks, so a global-maximum pick jumps between them, inflating the apparent scatter (Table S6). Narrowband tracking removes these jumps; the coefficient of variation decreases monotonically with narrowing bandwidth (Table S7), and the failure-window offset stays within ±2% for all bandwidths, so the reported <2% shift is a property of the data, not of the tracking band.

The tracking center is the yearly robust-stack f0 (the peak of the yearly median-stacked HVSR), not the median of the daily picks. For 5200314 the center is 8.12 Hz, giving a band of 6.49–9.74 Hz; its June spike (9.52 Hz) and yearly maximum (9.69 Hz) both lie inside this band, so no out-of-band points were removed from Figure 4A.

**Table S6.** Double-peak stations: global-maximum scatter vs. narrowband CV.

| Station | global-max std (%) | jump days | narrowband CV (%) | f0 (Hz) | second peak (Hz) |
|---|---|---|---|---|---|
| 5200272 | 60.1 | 23 | 4.69 | 3.17 | 8.12 |
| 5200326 | 27.8 | 28 | 9.24 | 6.22 | 4.86 |
| 5200309 | 54.5 | 93 | 5.22 | 3.47 | 4.69 |
| 5200291 | 16.9 | 32 | 5.32 | 8.87 | 5.12 |
| 5200314 | 22.6 | 48 | 5.02 | 8.12 | 5.70 |
| 5200298 | 20.5 | 18 | 2.71 | 2.90 | 10.97 |

**Table S7.** Bandwidth scan: coefficient of variation and failure-window offset for ±3% to ±20% tracking bands.

| Station | CV ±20% (%) | CV ±10% (%) | CV ±5% (%) | CV ±3% (%) | offset ±20% (%) |
|---|---|---|---|---|---|
| 5200272 | 4.69 | 2.96 | 2.04 | 1.37 | −1.8 |
| 5200326 | 9.24 | 4.21 | 2.71 | 1.59 | −1.8 |
| 5200309 | 5.22 | 2.89 | 2.13 | 1.42 | 0.0 |
| 5200291 | 5.32 | 4.20 | 2.78 | 1.64 | 0.0 |
| 5200314 | 5.02 | 3.28 | 2.37 | 1.56 | 1.8 |
| 5200298 | 2.71 | 2.48 | 2.09 | 1.47 | 0.0 |

The two peaks of 5200272 (3.2 and ~8.1 Hz) correspond, via H = Vs/4f0 with Vs = 295 m/s, to two interfaces at ~23 m and ~9 m depth, consistent with the thinnest cover resolved in Figure 1A; this is interpreted as a shallow internal interface, not a picking artifact.

### S4.7. Daytime vs. nighttime noise and HVSR stability

The daytime (08:00–16:00) selection was not based on lower noise level; on the contrary, daytime power is higher than nighttime across 0.5–20 Hz (Table S8). Daytime was chosen because the HVSR peak is more stable: nighttime (00:00–04:00) records carry vertically polarized low-frequency energy (wind, microbaroms, teleseismic surface waves) that suppresses the H/V ratio, whereas daytime cultural noise is more isotropic and excites the cover-layer resonance more reliably.

**Table S8.** Ratio of daytime to nighttime spectral power by band (5 May 2026; >1 means daytime louder).

| Station | 0.5–8 Hz | 8–20 Hz | 20–40 Hz |
|---|---|---|---|
| 5200272 | 1.56 | 4.43 | 0.49 |
| 5200291 | 2.93 | 2.76 | 1.69 |
| 5200298 | 1.76 | 3.11 | 0.45 |

### S4.8. dv/v measurement precision

The dv/v precision is set by the time-delay estimation bound. With a coda center frequency f_c ≈ 15 Hz and a coda window length τ ≈ 50 s, the expected precision is σ(dv/v) ≈ 1/(2 f_c τ) ≈ 0.07%, matching the measured pair-level daily scatter (0.07%, Table S3). This is the value quoted in the main text (±0.07%), and it is ~100 times smaller than the 7% precursor reported by Mainsant et al. (2012).

### S4.9. Instrument response and microseismic-event definition

The 5 Hz geophones roll off below ~5 Hz, but (a) the HVSR is a ratio of horizontal to vertical components, which cancels the common response, and (b) dv/v is measured relative to a reference correlogram, so a stable response does not bias the velocity change. Signal-to-noise is reduced only in the 5–8 Hz band. The "microseismic activity" reported in Figure 2A is the daily maximum ground acceleration, a proxy for impulsive events; a formal event detection (STA/LTA, magnitude threshold, and removal of rainfall or reservoir-operation transients) was not performed, so the five- to tenfold increase is a lower-bound indication of precursory microseismicity rather than a cataloged event count. The accelerometers have a nominal 10 Hz bandpass, so "microseismic" here denotes high-frequency ground shaking, not located microearthquakes.

### S4.10. Environmental (hydrologic) variables vs. noise metrics

No rainfall or air-temperature records were available for the site. As hydrologic proxies we therefore provide (i) the Three Gorges reservoir daily level and drawdown rate and (ii) volumetric soil-moisture content from four sensors installed on the slide from 14 June 2026. [`data/environmental_noise.csv`](data/environmental_noise.csv) aligns these variables with the daily medians of K, dv/v, and f0, so the absence of a hydrologic signature in the stiffness metrics can be checked directly.

---

## S5. References (supplemental)

The references cited in this Supplemental Material are the same as in the main manuscript; no additional references are used here.
