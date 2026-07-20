# DS-8555: Predictive Analysis

Coursework for **DDS-8555 Predictive Analysis**, National University, School of Technology and Engineering.
Author: **Brandon Perkins**

Each week is a self-contained project folder holding its notebooks, written paper, and any Kaggle
submission files. Notebooks render directly in GitHub, so they can be read without running anything.

---

## Repository structure

```
DS8555-Predictive-Analysis/
├── data/                                   # Kaggle data (not committed — see data/README.md)
├── week2-regression-models/
│   └── submissions/
│       └── submission_gradient_boosting.csv
└── week3-subset-selection-regularization/
    ├── notebooks/
    │   ├── Q1_Subset_Selection_Conceptual.ipynb
    │   ├── Q2_Stepwise_Lasso_Simulation.ipynb
    │   └── Q3_Abalone_Regularization_PCR.ipynb
    ├── paper/
    │   └── PerkinsB_DS8555_Week3.docx
    └── submissions/
        ├── submission_lasso_subset.csv
        └── submission_pcr.csv
```

One notebook per task, rather than one combined file, so that each analysis can be read, run, and
reviewed independently.

---

## Week 3 — Subset Selection, Regularization, and Principal Components Regression

| Notebook | Topic |
|---|---|
| `Q1_Subset_Selection_Conceptual.ipynb` | ISLP Ch. 6 Conceptual Ex. 1 — best subset vs. forward and backward stepwise, with a simulation that verifies each claim |
| `Q2_Stepwise_Lasso_Simulation.ipynb` | ISLP Ch. 6 Applied Ex. 8 — stepwise selection under Mallow's $C_p$, and the lasso with cross-validated $\lambda$ |
| `Q3_Abalone_Regularization_PCR.ipynb` | Kaggle Playground Series S4E4 — lasso-informed subset selection and principal components regression |

### Headline results (Kaggle abalone, metric = RMSLE)

| Model | Validation RMSLE | Predictors |
|---|---|---|
| Baseline (predict the mean) | 0.2881 | 0 |
| Lasso, minimum-error λ | 0.1559 | 35 of 37 |
| **Model A — OLS on 1-SE lasso subset** | **0.1564** | **19 of 37** |
| **Model B — PCR** | **0.1559** | 37 components |

### Findings worth flagging

- **Regularization barely shrinks when `n >> p`.** With ~72,000 training rows against 37 predictors, the
  minimum-error lasso retained 35 of 37 terms. Applying the **one-standard-error rule** produced a real
  subset (19 of 37) at a cost of roughly 0.0005 RMSLE — a strong trade for interpretability.
- **PCR performed no dimension reduction.** Cross-validation error fell monotonically in `M` and selected
  all 37 components. PCR's value here is structural, not predictive: the component VIFs are exactly
  1.000, confirming that the rotation removes collinearity by construction.
- **Assumptions are only partly satisfied.** Independence holds (Durbin–Watson 1.999), but Jarque–Bera and
  Breusch–Pagan both reject at `p < .001`, so residuals are neither normal nor homoscedastic. Reported
  p-values and confidence intervals should be read as approximate; point predictions remain valid.
- **A counterintuitive result in Q2.** When the response depended on `X^7` alone, forward stepwise
  recovered the coefficient almost exactly (7.0026 vs. a true 7.0), while the lasso spread the signal
  across six correlated powers — the reverse of the usual expectation, and a known instability of `L1`
  selection under near-duplicate predictors.

---

## Reproducing the analysis

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

Download the competition data (see `data/README.md`) into the folder alongside the notebook you intend to
run, then execute the notebook top to bottom. Every notebook uses `SEED = 8555`, tied to the course
number, so results are reproducible.

---

## References

James, G., Witten, D., Hastie, T., Tibshirani, R., & Taylor, J. (2023). *An introduction to statistical
learning with applications in Python*. Springer. https://doi.org/10.1007/978-3-031-38747-0

Nash, W. J., Sellers, T. L., Talbot, S. R., Cawthorn, A. J., & Ford, W. B. (1994). *The population biology
of abalone (Haliotis species) in Tasmania* (Technical Report No. 48). Sea Fisheries Division, Department
of Primary Industry and Fisheries, Tasmania.

Tibshirani, R. (1996). Regression shrinkage and selection via the lasso. *Journal of the Royal Statistical
Society: Series B, 58*(1), 267–288. https://doi.org/10.1111/j.2517-6161.1996.tb02080.x

---

## Academic integrity

This repository contains coursework submitted for academic credit. It is published for portfolio and
reproducibility purposes. Please do not submit any part of it as your own work.
