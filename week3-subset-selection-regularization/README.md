# Week 3 — Subset Selection, Regularization, and Principal Components Regression

## Contents

| Path | Description |
|---|---|
| `notebooks/Q1_Subset_Selection_Conceptual.ipynb` | ISLP Ch. 6 Conceptual Exercise 1 |
| `notebooks/Q2_Stepwise_Lasso_Simulation.ipynb` | ISLP Ch. 6 Applied Exercise 8 |
| `notebooks/Q3_Abalone_Regularization_PCR.ipynb` | Kaggle S4E4 — lasso subset selection and PCR |
| `paper/PerkinsB_DS8555_Week3.docx` | APA 7 paper |
| `submissions/submission_lasso_subset.csv` | Kaggle submission — OLS refit on the 1-SE lasso subset |
| `submissions/submission_pcr.csv` | Kaggle submission — principal components regression |

## Running

Download `train.csv` and `test.csv` (see `../data/README.md`) into `notebooks/`, then run
`Q3_Abalone_Regularization_PCR.ipynb` top to bottom. It regenerates both submission files.

`Q1` and `Q2` are fully self-contained — they generate their own simulated data and need no downloads.

## Method summary

**Model A — regularization informing subset selection.** A degree-2 polynomial expansion of the seven
body measurements plus `Sex` indicators produces a 37-term dictionary. A cross-validated lasso is fit to
the standardized dictionary; the **one-standard-error rule** selects the sparsest model within one
standard error of the minimum CV error, retaining 19 of 37 terms. Ordinary least squares is then refit on
that subset (the relaxed lasso) so the coefficients are free of shrinkage bias and interpretable.

**Model B — principal components regression.** The same standardized dictionary is rotated by PCA, with
the number of components chosen by 5-fold cross-validation. Components are orthogonal by construction,
so collinearity is eliminated rather than merely penalized.

All preprocessing (scaling, the PCA rotation, the lasso path) is fit on training data only to prevent
leakage. `SEED = 8555` throughout.
