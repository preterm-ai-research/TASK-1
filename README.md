# Preterm Birth Prediction

## Project Overview

This project develops and evaluates machine-learning models for predicting preterm birth using maternal and pregnancy data.

Preterm birth is defined as a delivery before 37 completed weeks of gestation. The goal is to estimate the risk of a preterm delivery using information available before birth. These models are experimental research prototypes and must not be used to make clinical decisions or replace medical professionals.

## First Task

The first task was to prepare the 2025 natality data for machine learning, study it, preprocess it, and compare baseline classification models.

The work included:

1. Extracting the natality dataset and converting it to CSV format.
2. Creating a 10,000-row sample from the source data.
3. Identifying and documenting the target variable: **preterm (1)** for deliveries before 37 weeks and **term (0)** for deliveries at or after 37 weeks.
4. Studying variable types, missing values, class distribution, and feature documentation.
5. Cleaning invalid or unknown codes and handling missing values.
6. Encoding categorical variables and scaling features where required.
7. Splitting the data into training and test sets.
8. Removing gestational age from the predictive features to prevent target leakage.
9. Training and evaluating Logistic Regression and Decision Tree models.
10. Comparing the models using metrics appropriate for the imbalanced target class.

## Repository Structure

- `DATASET/` contains the natality sample data.
- `EDA_task/` contains exploratory data analysis, feature documentation, missing-value reports, and target-distribution results.
- `preprocessing_task/` contains the preprocessing notebook, preprocessed data, preprocessing decisions, objects, and report.
- `Logistic_Regression_task/` contains the Logistic Regression notebook, model, metrics, figures, and evaluation report.
- `DecisionTree_Preterm_task/` contains the baseline and regularized Decision Tree models, notebooks, metrics, figures, and reports.
- `Comparative_Report_LogReg_vs_DecisionTreeB.pdf` contains the side-by-side model comparison.
- `2CS_Project_team_task1.pdf` contains the original first-task assignment and project requirements.

## Data and Experimental Setup

The experiments used a sample of 10,000 records:

- 8,000 records for training
- 2,000 records for testing
- 18 input features
- The same preprocessed data and test split for every model

The test set contained approximately 89.4% term births and 10.6% preterm births. Because the classes are strongly imbalanced, accuracy alone is not sufficient. Recall, precision, F1-score, ROC-AUC, specificity, and balanced accuracy were used to evaluate performance.

## Models Evaluated

### Logistic Regression

Logistic Regression was trained with 1,000 maximum iterations. Its default configuration used a 0.5 prediction threshold and did not apply class weights.

### Baseline Decision Tree

A baseline Decision Tree was trained with scikit-learn defaults and no depth, sample, or class-weight constraints.

### Regularized Decision Tree

A regularized Decision Tree was trained with:

- Maximum depth: 5
- Minimum samples per split: 20
- Minimum samples per leaf: 10
- Balanced class weights

## Main Results

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.9075 | 0.7143 | 0.2123 | 0.3273 | 0.7427 |
| Baseline Decision Tree | 0.8480 | 0.2982 | 0.3208 | 0.3091 | 0.6153 |
| Regularized Decision Tree | 0.7930 | 0.2694 | 0.5566 | 0.3631 | 0.7130 |

Precision, recall, and F1-score are reported for the preterm class.

The Logistic Regression model had the highest accuracy, precision, and ROC-AUC. However, it detected only 21.23% of preterm births.

The baseline Decision Tree was overfitted: its training accuracy was 97.9%, while test accuracy was 84.8%. It was also the weakest model on ROC-AUC and did not provide the best overall result.

The regularized Decision Tree had the highest recall, F1-score, and balanced accuracy. It detected 55.66% of preterm births, compared with 21.23% for Logistic Regression and 32.08% for the baseline tree.

The regularized Decision Tree was selected as the preferred model for the project's screening objective because identifying preterm births was prioritized over limiting false alarms. It still produced 320 false positives and missed 94 preterm cases, so it requires further improvement before any real-world use.

## Limitations

- The dataset is highly imbalanced.
- The experiments use a sample of 10,000 records.
- The models have limited preterm-birth recall.
- The regularized Decision Tree produces a substantial number of false alarms.
- Performance was measured with a train-test split rather than independent external validation.
- The data represents the United States population and may not generalize to other countries or healthcare contexts.
- The study evaluated only Logistic Regression and Decision Tree configurations.
- Logistic Regression could potentially benefit from class weighting or threshold optimization.
- The models are research prototypes and are not clinically validated.

## Future Work

Possible next steps include:

- Comparing additional models such as Random Forest, gradient boosting, and neural networks.
- Applying class weighting and optimizing prediction thresholds.
- Using larger and more diverse datasets.
- Performing external and hospital-level validation.
- Investigating model explainability.
- Developing an application interface only after appropriate validation and medical review.
