# CIBMTR - Equity in Post-HCT Survival Predictions

## Overview
This project implements a stacking ensemble regression model to predict post–hematopoietic cell transplantation (HCT) survival outcomes using the CIBMTR dataset. The objective is to generate accurate survival predictions while ensuring performance equity across demographic groups.

The approach uses multiple gradient boosting models combined through a stacking regressor to improve predictive performance and robustness.

## Dataset
The project is based on the CIBMTR Equity in Post-HCT Survival Predictions competition dataset available on Kaggle.

Competition link  
https://www.kaggle.com/competitions/equity-post-HCT-survival-predictions

Reference notebook  
https://www.kaggle.com/code/mafiosoquasar/cibmtr-stacking-regressor-lgbm-xgboost-catboost

## Architecture Description

### Data Processing
The dataset is loaded and preprocessed through several steps including:
Handling missing values  
Encoding categorical variables  
Transforming numerical features  
Splitting data into training, validation, and test sets  

Feature engineering may include medically relevant transformations or grouping of clinical attributes.

### Base Models
Three base gradient boosting regressors are used:
LightGBM Regressor  
XGBoost Regressor  
CatBoost Regressor  

Each model is trained independently and learns from the structured clinical and demographic data. Gradient boosting methods are chosen due to their strong performance on tabular medical datasets.

### Stacking Ensemble
A stacking regressor is used to combine the predictions of the three base models.

Level 1  
The base models predict outcomes on the training data. Their predictions serve as meta-features.

Level 2  
A meta-regressor is trained on these meta-features. This final model learns how to best weight and combine the base learner outputs.

This stacking strategy improves accuracy and reduces biases inherent to individual models, supporting fairness objectives.

### Prediction Output
The final model generates continuous predictions representing survival-related risk scores. These predictions are formatted according to competition requirements for submission.

### Evaluation
Performance is assessed using regression metrics such as root mean squared error. Additional fairness and equity metrics are calculated across demographic subgroups to evaluate model consistency and reliability.

### Workflow Summary
Load and clean the dataset  
Preprocess features and encode variables  
Train LightGBM, XGBoost, and CatBoost base models  
Generate base model predictions as meta-features  
Train a stacking meta-regressor  
Generate final predictions for the test dataset  
Export predictions in the required submission format  

## Project Structure
data  
processed and raw dataset files  

models  
lgbm_model  
xgboost_model  
catboost_model  

notebooks  
cibmtr-stacking-regressor-lgbm-xgboost-catboost.ipynb  

output  
submission.csv  

README.md

## Notes
Prediction quality depends on feature quality, training stability, and diversity across the base models. Adding additional models or refining feature engineering can improve overall performance. The stacking design supports flexible model integration for future experimentation.
