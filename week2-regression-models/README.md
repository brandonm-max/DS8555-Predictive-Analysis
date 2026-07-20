# Week 2 — Building Regression Models

Kaggle Playground Series S4E4, first entry.

| Path | Description |
|---|---|
| `submissions/submission_gradient_boosting.csv` | Public leaderboard RMSLE **0.14813** (private 0.14783) |

## Summary

Two models were built on `log1p(Rings)` to match the RMSLE metric:

| Model | Validation RMSLE |
|---|---|
| Baseline (predict the mean) | 0.291 |
| Ordinary least squares | 0.167 |
| Gradient boosting | 0.152 |

Variance inflation factors confirmed severe collinearity (whole weight ≈ 69). Residual diagnostics showed
independence held (Durbin–Watson 1.996) but normality and constant variance were both rejected.

> **To add:** the Week 2 notebook and APA paper. Drop them into `notebooks/` and `paper/` to match the
> Week 3 layout.
