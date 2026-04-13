# Mortgage Default Prediction: Temporal Stability of SHAP Explanations

MSc Dissertation | Coventry University | 2025-2026

---

## Overview

This project investigates whether SHAP-based feature importance explanations remain stable when a mortgage default prediction model is trained on pre-COVID data and evaluated on post-COVID data. The Freddie Mac Single-Family Loan-Level Dataset is used, covering 14,146,041 loan originations from 2016 to 2021. COVID-19 serves as a natural and externally defined distributional boundary, with 2016 to 2019 originations forming the training period and 2020 to 2021 originations forming the test period.

---

## Research Question

How do SHAP-based feature importance explanations maintain stability in mortgage credit risk models under temporal distributional shift, and how sensitive are those explanations to data perturbations and imbalance-handling strategy?

---

## Key Findings

- XGBoost achieved the highest Average Precision of 0.2615 on the post-COVID test set (AUC-ROC: 0.750)
- Spearman rank correlation between pre-COVID and post-COVID SHAP rankings: 0.9447 (p < 0.0001), indicating strong structural stability
- Kendall's W across 30 bootstrap resamples: 0.9671, confirming within-period consistency
- Top-5 feature agreement held at 100% across all perturbation noise levels (5%, 10%, 15%)
- SMOTE vs class-weighting produced a Spearman correlation of only 0.7742, meaning imbalance-handling strategy introduces more explanation divergence than the COVID distributional shift itself

---

## Repository Structure

```
mortgage-default-shap-stability/
|
|-- notebook/
|   |-- mortgage_default_shap_stability.ipynb    # Main analysis notebook
|   |-- README.md                                # Notebook usage guide
|
|-- data/
|   |-- README.md                                # Data access and download instructions
|
|-- results/
|   |-- README.md                                # Summary of key outputs
|
|-- requirements.txt                             # Python dependencies
|-- .gitignore
|-- README.md
```

---

## Dataset

The data used in this project is the Freddie Mac Single-Family Loan-Level Dataset, which is publicly available but requires free registration.

Access the dataset here: https://www.freddiemac.com/research/datasets/sf-loanlevel-dataset

The dataset is not included in this repository due to its size (approximately 50GB uncompressed). See `data/README.md` for full download and setup instructions.

---

## Models

Three classifiers were trained and evaluated:

| Model | AUC-ROC | Avg Precision | F1 (Default Class) |
|---|---|---|---|
| SGD Logistic Regression | 0.7189 | 0.2033 | 0.25 |
| Random Forest | 0.7533 | 0.2304 | 0.31 |
| XGBoost | 0.7504 | 0.2615 | 0.31 |

All models were trained on 2016 to 2019 originations and evaluated on 2020 to 2021 originations without retraining, representing a genuine out-of-time validation under economic regime change.

---

## SHAP Stability Results

| Metric | Value | Interpretation |
|---|---|---|
| Spearman (pre vs post-COVID) | 0.9447 | Strong cross-period rank preservation |
| Kendall's W (30 bootstrap runs) | 0.9671 | Strong within-period consistency |
| Spearman at 15% noise | 0.9408 | Robust to data quality degradation |
| SMOTE vs class-weight Spearman | 0.7742 | Imbalance strategy significantly affects explanations |

---

## Technical Stack

| Tool | Version | Purpose |
|---|---|---|
| Python | 3.9 | Primary language |
| pandas | 1.5+ | Data processing |
| numpy | 1.23+ | Array operations |
| scikit-learn | 1.2+ | Models and preprocessing |
| xgboost | 1.7+ | Primary classifier |
| shap | 0.49 | Explainability analysis |
| imbalanced-learn | 0.10+ | SMOTE experiment |
| matplotlib | 3.6+ | Visualisations |
| pyarrow | 11.0+ | Parquet file handling |
| joblib | 1.2+ | Model serialisation |

---

## How to Run

1. Clone the repository
```
git clone https://github.com/sai774059-sys/mortgage-default-shap-stability.git
cd mortgage-default-shap-stability
```

2. Install dependencies
```
pip install -r requirements.txt
```

3. Download the Freddie Mac dataset following the instructions in `data/README.md`

4. Open and run the notebook
```
jupyter notebook notebook/mortgage_default_shap_stability.ipynb
```

Note: The notebook is structured with checkpoint reload cells. You do not need to rerun data processing from scratch on each session. Each major phase saves outputs to disk.

---

## Class Imbalance

The dataset exhibits a severe class imbalance of 115:1 (non-default to default). The primary strategy used is 1:10 undersampling combined with class_weight='balanced' for all classifiers. A separate SMOTE experiment (sampling_strategy=0.3) is included to assess the effect of oversampling on SHAP explanations.

---

## Ethical Statement

The Freddie Mac dataset is publicly available and contains no personally identifiable information. Borrower identities are anonymised at source. No individual lending decisions are made as part of this project. The models produced are not deployed in any live system.

---

## Author

Sai Krishna Bikkini | MSc Data Science | Coventry University | 2025-2026
