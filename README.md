# Formula 1 Podium Prediction (Milestone 1)

Predicting whether a driver finishes in the top 3 of a Formula 1 race, using only information
available **after qualifying and before the race start**.

**Team:** Malak Soliman (58-8162), Aya Elsaadany (58-3074), Lubna Kudsi (58-11314), Jana Elbehesy (58-8233)
**Kaggle notebook:** https://www.kaggle.com/code/malaksoliman1/milestone-1-f1
**Report:** [`F1_Podium_Prediction_Report(2).pdf`](F1_Podium_Prediction_Report (2).pdf)

## Contents

| File | What it is |
|---|---|
| `milestone-1-f1.ipynb` | The full run-all notebook, with outputs: audit, cleaning, EDA before and after cleaning, the three data-engineering questions, feature engineering, models, experiments, explainability and the inference function |
| `F1_Podium_Prediction_Report(2).pdf` | The analytical report |
| `requirements.txt` | Python packages used |

## Data

[Formula 1 World Championship (1950 - 2024)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)
by Rohan Rao on Kaggle (14 CSV tables). The data is not included in this repository.

## How to run

**On Kaggle (recommended):** open the notebook, add the dataset above with *Add Input*, then *Run All*.

**Locally:** `pip install -r requirements.txt`, download the dataset, put the 14 CSV files in a folder
named `data/` next to the notebook, then *Run All*. No cell needs editing: the first code cells find the
data folder automatically and write `modeling_table.csv` next to the notebook.

Tested with Python 3.13, pandas 2.2.3, numpy 2.3.5, scikit-learn 1.6.1, shap 0.54.1, lime 0.2.0.1,
matplotlib 3.11.2 and seaborn 0.13.2 (a full run takes about one minute on a CPU).

## Approach in brief

- **Modeling table:** one row per driver per race (shared drives resolved by keeping the best
  `positionOrder`); 17 pre-race features in four groups (grid, form, standings, qualifying). History
  features use only earlier races.
- **Split by season:** train 1950-2019, validation 2020-2021, test 2022-2024. Hyperparameters, the
  training window and the probability threshold are chosen on validation only.
- **Models:** grid-only logistic regression (baseline), logistic regression, gradient boosting and a
  shallow neural network (two hidden layers), compared on ROC-AUC, PR-AUC (primary), F1, precision and
  recall.
- **Test PR-AUC:** baseline 0.647, logistic regression 0.720, gradient boosting 0.701 (selected on
  validation), neural network 0.692.
- **Experiments and explainability:** early stopping, class weights, training window, feature-group
  ablation, two preprocessing-order experiments, permutation importance, SHAP and LIME.
