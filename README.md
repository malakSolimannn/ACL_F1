# Formula 1 Podium Prediction (Milestone 1)

Predicting whether a driver finishes in the top 3 of a Formula 1 race, using only information
available **after qualifying and before the race start**.

**Team:** [team members and IDs]
**Kaggle notebook:** [Kaggle link]
**Report:** [`F1_Podium_Prediction_Report.pdf`](F1_Podium_Prediction_Report.pdf)

## Contents

| File | What it is |
|---|---|
| `acl-f1-milestone1-final.ipynb` | The full notebook, with outputs: audit, cleaning, EDA, the three data-engineering questions, feature engineering, models, experiments, explainability and the inference function |
| `F1_Podium_Prediction_Report.pdf` | The analytical report |
| `requirements.txt` | Python packages used |

## Data

[Formula 1 World Championship (1950 - 2024)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)
by Rohan Rao on Kaggle (14 CSV tables). The data is not included in this repository.

## How to run

**On Kaggle (recommended):** open the notebook, add the dataset above with *Add Input*, turn on
*Internet* in the notebook settings (needed to install `lime` if it is missing), then *Run All*.

**Locally:** install the packages with `pip install -r requirements.txt`, download the dataset, and
change `DATA_DIR` in the second code cell to the folder that contains `results.csv`.

## Approach in brief

- **Modeling table:** one row per driver per race; 17 pre-race features in four groups (grid, form,
  standings, qualifying). History features use only earlier races.
- **Split by season:** train 1950-2019, validation 2020-2021, test 2022-2024.
- **Models:** grid-only logistic regression (baseline), logistic regression, gradient boosting and a
  shallow neural network, compared on ROC-AUC, PR-AUC (primary), F1, precision and recall.
- **Test PR-AUC:** baseline 0.647, logistic regression 0.720, gradient boosting 0.701 (selected on
  validation), neural network 0.692.
- **Experiments and explainability:** feature-group ablation, two preprocessing-order experiments,
  permutation importance, SHAP and LIME.
