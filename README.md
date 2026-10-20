# Customer Churn Prediction & Statistical Analysis

## Project Overview

This project investigates customer churn in the IBM Telco Customer Churn dataset using exploratory data analysis, statistical hypothesis testing, and logistic regression.

The objective is to identify patterns associated with churn, evaluate a baseline classification model, and develop evidence-based customer-retention recommendations.

## Tools and Technologies

- Python
- pandas and NumPy
- Matplotlib
- SciPy
- scikit-learn
- Jupyter Notebook

## Data Preparation

- Loaded and inspected 7,043 customer records with 21 columns.
- Identified 11 blank `TotalCharges` values that were initially represented as whitespace.
- Converted `TotalCharges` to a numeric data type.
- Excluded the 11 records with missing total charges from the initial modeling dataset, leaving 7,032 records.
- Checked for missing values and duplicate rows.
- Excluded `customerID` from model features.

## Exploratory and Statistical Analysis

The cleaned dataset had a churn rate of 26.58%.

A chi-square test of independence examined the relationship between contract type and churn:

- Chi-square statistic: 1179.546
- Degrees of freedom: 2
- Cramér's V: 0.410
- P-value: approximately 7.33 × 10⁻²⁵⁷

The results provide strong evidence of an association between contract type and churn in this dataset. The smallest expected cell count was 391.24, satisfying the usual expected-count guideline for the chi-square approximation.

Observed churn rates were:

- Month-to-month contracts: 42.71%
- One-year contracts: 11.28%
- Two-year contracts: 2.85%

These are descriptive associations and do not establish causation.

## Machine Learning Approach

A logistic regression baseline was developed using scikit-learn.

- Training/test split: 80% / 20%
- Stratified split to preserve class proportions
- Numeric preprocessing: median imputation and standardization
- Categorical preprocessing: most-frequent imputation and one-hot encoding
- Preprocessing and model training combined in a pipeline to prevent preprocessing leakage
- Customer IDs excluded from model inputs

The test set contained 1,407 records.

## Model Evaluation

At the default classification threshold of 0.5:

| Metric | Test result |
|---|---:|
| Accuracy | 0.805 |
| Precision | 0.650 |
| Recall | 0.575 |
| F1-score | 0.610 |
| ROC-AUC | 0.836 |

A threshold comparison showed that reducing the threshold to 0.4 increased recall to 0.684 and F1-score to 0.627, while precision decreased to 0.579.

The threshold comparison is exploratory. A final operating threshold should be selected using validation data and the business costs of false positives and false negatives.

## Business Recommendations

1. Investigate the high observed churn rate among month-to-month customers.
2. Examine pricing, service quality, tenure, and support experience as possible contributors to churn.
3. Consider testing targeted retention interventions and measuring their effectiveness.
4. Select model thresholds based on retention-campaign costs and benefits rather than accuracy alone.

## Limitations

- The dataset is a sample dataset and may not represent current customers or other telecommunications businesses.
- The analysis is observational; associations do not prove causation.
- Eleven zero-tenure customers with missing total charges were excluded from the initial model, limiting conclusions about brand-new customers.
- Logistic regression provides a baseline rather than proof of optimal predictive performance.
- The reported metrics come from one stratified test split and may vary on other samples.
- The 0.4 threshold was compared on the test set for exploration; a separate validation set should be used for threshold selection before final unbiased evaluation.

## Reproducibility

The train/test split uses `random_state=42`. Run the notebook cells in order to reproduce the analysis.

## Author

M.Sc. Applied Mathematics student interested in data science, statistical analysis, and machine learning.
