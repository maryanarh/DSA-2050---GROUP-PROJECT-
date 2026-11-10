# Energy Peak-Demand Classification

A reproducible, leakage-safe machine-learning pipeline that classifies **peak-demand
hours** across the three power-consumption zones of Tetuan City. The project compares
six classifiers under a chronological train/validation/test protocol, tunes operating
thresholds on a validation slice only, and produces an auditable diagnostics report.

---

## Overview

Electrical demand peaks drive grid stress and cost. This notebook turns the raw
hourly consumption + weather data into three binary classification problems
(one per zone):

> *"Is this hour a peak-demand hour for zone *k*?"*

A peak is defined as an hour whose consumption exceeds the **monthly 90th
percentile** computed **only from the training window** — so no future
information leaks into the labels, the features, or the thresholds.

The project emphasises:

- **Leakage safety** — monthly thresholds are computed after the chronological
  split boundary is fixed, and the test set is truncated to months that have
  training support.
- **Fair model comparison** — six model families are trained on identical
  features and evaluated on a single locked test set.
- **Validation-only threshold tuning** — a 3-point-smoothed cost sweep is used
  so operating thresholds are not optimised against the test set.
- **Auditable diagnostics** — PR curves, calibration checks, feature/coefficient
  importance, threshold sweeps, monthly distribution plots, and cross-zone
  correlation heatmaps are all saved to disk.

---

## Dataset

**Tetuan City power consumption** — a public dataset of hourly electricity
consumption for three city zones together with weather covariates.

Expected file name:
