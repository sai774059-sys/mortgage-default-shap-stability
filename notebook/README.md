# Notebook

This folder contains the main Jupyter notebook for the project.

## File

`mortgage_default_shap_stability.ipynb`

This is the primary analysis notebook structured into the following phases:

1. Data acquisition and file verification
2. Year-by-year processing and default labelling
3. Preprocessing, imputation and train/test split
4. Model training: SGD Logistic Regression, Random Forest, XGBoost
5. SHAP computation and temporal stability analysis
6. Bootstrap stability testing with Kendall's W across 30 runs
7. Perturbation robustness testing at 5%, 10%, and 15% Gaussian noise
8. SMOTE vs class-weighting SHAP comparison

## Running the Notebook

The notebook uses checkpoint reload cells at the top of each major section. Once a phase has been run and outputs saved to disk, you can reload the session and skip directly to any subsequent phase without reprocessing from scratch. Peak RAM usage was kept below 6 GB throughout by processing data year by year and saving intermediate outputs to Parquet format before freeing memory.

## Requirements

See `requirements.txt` in the root of the repository.

## Note on Data

The Freddie Mac dataset must be downloaded separately. See `data/README.md` for full instructions.
