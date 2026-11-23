# Telecom Customer Churn Prediction

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-orange.svg)
![Pandas](https://img.shields.io/badge/Pandas-Latest-blue.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Latest-green.svg)

This repository contains an end-to-end data science project designed to predict customer churn for a telecommunications company. The project was developed as part of the **Data Science and Advanced Analytics Specialization**.

## 🛠️ Technologies Used
- **Programming Language:** Python 3.8+
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning Library:** Scikit-Learn
- **Data Visualization:** Matplotlib, Seaborn
- **Notebook Environment:** Google Colab / Jupyter Notebooks

## 🎯 Project Objective
The primary goal is to build, evaluate, and compare multiple classification models to identify customers at high risk of churning. This allows the business to take proactive retention actions.

## 📊 Dataset Structure & Data Quality
The project utilizes two main datasets:
- `train.csv` (5,634 rows, 21 columns): Training data containing the target variable (`Churn`).
- `test.csv` (1,409 rows, 20 columns): Test set used to generate final predictions.

### Key Data Quality Findings (Data Cleansing):
- **Hidden Imputations:** Customers with `tenure = 0` (newly acquired) had their `TotalCharges` incorrectly imputed with the portfolio's median ($1,397.47). This was corrected by setting their `TotalCharges` to `$0.0` to maintain logical consistency with their zero-month tenure.

## 🔍 Exploratory Data Analysis (EDA)
The most discriminative features influencing customer churn are:
1. **Contract Type (`Contract`):** Month-to-month contracts have a high churn rate of **42.7%**, compared to only **2.9%** for two-year contracts.
2. **Internet Service (`InternetService`):** Fiber optic service subscribers show a worrying churn rate of **42.1%**.
3. **Payment Method (`PaymentMethod`):** Electronic check is the leading payment method among churning customers at **45.7%**, whereas automatic payment methods remain under 20%.
4. **Tenure (`tenure`):** Churn risk is critically concentrated within the first few months of the customer lifecycle.

## 🛠️ Data Preprocessing
The data preparation pipeline includes:
- Dropping irrelevant identifiers (`customerID`).
- Mapping the target variable to binary (`Yes` = 1, `No` = 0).
- **One-Hot Encoding** categorical features, dropping the first category (`drop_first=True`) to avoid perfect multicollinearity.
- Performing a stratified 80/20 train-validation split to preserve the target variable's class distribution (73.5% / 26.5%).
- Scaling numerical features with `StandardScaler` (fitted only on the training set to prevent data leakage).

## 🤖 Model Evaluation & Results
Three classification algorithms were trained and evaluated. 5-fold cross-validation confirmed model stability across different data splits:

| Model | Accuracy | Precision | Recall | F1-Score | ROC AUC |
|---|---|---|---|---|---|
| **Logistic Regression** | **0.815** | **0.691** | 0.545 | **0.609** | **0.848** |
| **kNN (k=100)** | 0.804 | 0.650 | 0.565 | 0.605 | 0.839 |
| **Naive Bayes** | 0.666 | 0.436 | **0.870** | 0.580 | 0.828 |

### 🏆 Selected Model
**Logistic Regression** was chosen as the final model because it achieved the highest **ROC AUC (0.848)**. It provides the best business-oriented balance between precision and recall, minimizing costly false alarms while capturing a solid portion of churners.

## 📁 Repository Structure
- `proyecto_churn.ipynb`: Complete Jupyter/Colab notebook containing step-by-step analysis and model development.
- `submission_churn.csv`: Final predictions generated for the `test.csv` dataset.
