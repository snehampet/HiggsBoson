# Higgs Boson Event Classification using XGBoost

## Overview

This repository provides a complete solution for classifying Higgs boson events (signal vs. background) based on the ATLAS Higgs Boson Machine Learning Challenge dataset from CERN. The workflow leverages data preprocessing, feature scaling, and the XGBoost classifier for high-performance rare-event detection in particle physics.

## Table of Contents

- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
- [Code Workflow](#code-workflow)
- [Model Evaluation](#model-evaluation)
- [Reproducibility](#reproducibility)
- [Future Improvements](#future-improvements)
- [Acknowledgments](#acknowledgments)

## Project Structure

```
.
├── README.md
├── HiggbosonFinalcode.ipynb   # Main notebook with code and results
├── atlas-higgs-challenge-2014-v2.csv.gz  # Dataset (not included due to size)
└── Report-higgs boson detection.pdf                   
```

## Dataset

- **Source:** ATLAS experiment, CERN ([CERN Open Data Portal])
- **File:** `atlas-higgs-challenge-2014-v2.csv.gz`
- **Rows:** Each row = collision event.
- **Features:** Derived and primary physics variables.
- **Labels:** `"s"` (signal) or `"b"` (background). Mapped to 1 (signal) and 0 (background).

*Obtain the dataset from the [CERN Open Data Portal] or the original Kaggle challenge pages.*

## Requirements

Install Python dependencies with:

```bash
pip install pandas numpy scikit-learn xgboost matplotlib seaborn
```

## Getting Started

1. **Download** the dataset and place it in your project directory.
2. **Open** the main notebook or Python script.
3. **Run** each code cell in sequence:
    - Data loading and exploration
    - Preprocessing (scaling, encoding)
    - Model training, prediction, and evaluation

## Code Workflow

### 1. Data Preparation

- Loads the compressed CSV containing ATLAS collision events.
- Checks data types and inspects the first few rows.
- Confirms there are no missing values; handles sentinel values as needed.
- Drops non-feature columns (`EventId`, `Weight`, `KaggleSet`, `KaggleWeight`).
- Scales numerical features using `StandardScaler`.
- Maps the `'Label'` column to binary (signal: 1, background: 0).
- Performs a 70/30 train-test split with stratification to preserve class balance.

### 2. Model Training (XGBoost)

- Instantiates an `XGBClassifier` with key parameters:
    - `objective='binary:logistic'`
    - `eval_metric='logloss'`
    - `use_label_encoder=False`
    - `random_state=42`
- Trains the model on the training set.
- Generates probability and hard class predictions for the test set.

### 3. Model Evaluation

- Prints accuracy, precision, recall, and F1-score using `classification_report()`.
- Computes and displays the confusion matrix.
- Analyzes feature importance to identify top physics variables for discrimination.

## Model Evaluation

**Typical performance on the test set:**

| Metric              | Value   |
|---------------------|---------|
| Accuracy            | 0.84    |
| Precision (Signal)  | 0.79    |
| Recall (Signal)     | 0.74    |
| F1-score (Signal)   | 0.76    |

Confusion matrix and feature importance plots can be found within the notebook results.

## Reproducibility

- All random seeds are fixed (e.g., `random_state=42`) for reproducibility.
- Version numbers for critical packages (numpy, pandas, xgboost, scikit-learn) are listed in the requirements.

## Future Improvements

- Hyperparameter tuning for XGBoost (tree depth, learning rate, etc.)
- Advanced feature engineering and domain-driven feature selection.
- Ensemble combinations (e.g., stacking XGBoost with neural networks).
- Calibration techniques for probability outputs.
- Exploration of updated or real detector data as it becomes available.

## Acknowledgments

- **Data:** ATLAS Higgs Boson Challenge, CERN Open Data Portal
- **Libraries:** Python, pandas, scikit-learn, XGBoost, matplotlib
