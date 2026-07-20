# Data

The competition data is **not committed to this repository**. Kaggle's competition rules govern
redistribution, and the files are large enough that tracking them in Git adds little value.

## Download

Source: [Kaggle Playground Series S4E4 — Regression with an Abalone Dataset](https://www.kaggle.com/competitions/playground-series-s4e4/data)

Files needed:

- `train.csv` (90,615 rows)
- `test.csv` (60,411 rows)
- `sample_submission.csv`

Place them in the folder alongside the notebook you plan to run.

## A note on column names

The Kaggle files label the three meat weights as `Whole weight`, `Whole weight.1`, and `Whole weight.2`.
The notebooks rename these to the standard UCI abalone names before modeling:

| Kaggle column    | Renamed to       |
|------------------|------------------|
| `Whole weight`   | `Whole_weight`   |
| `Whole weight.1` | `Shucked_weight` |
| `Whole weight.2` | `Viscera_weight` |
| `Shell weight`   | `Shell_weight`   |

## Target

`Rings` is a proxy for age (age ≈ Rings + 1.5). The competition metric is **root mean squared logarithmic
error (RMSLE)**, so the notebooks model `log1p(Rings)` to align the loss function with the metric.
