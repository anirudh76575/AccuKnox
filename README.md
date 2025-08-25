# Fraud Detection Case Study

This repository contains a machine learning workflow for detecting fraudulent transactions using a large-scale financial dataset (**6,362,620 rows × 11 columns**). The project demonstrates the end-to-end pipeline — from data preprocessing and feature engineering to model training, evaluation, and business insights.

---

## 📌 Problem Statement
The objective is to identify fraudulent transactions within financial data and provide actionable business recommendations to minimize future fraud.

---

## 📂 Dataset
- **File:** `Fraud.csv`  
- **Shape:** 6,362,620 rows × 11 columns  
- **Key Columns:**
  - `step`: Time step of the transaction
  - `type`: Transaction type (`PAYMENT`, `TRANSFER`, `CASH_OUT`, etc.)
  - `amount`: Transaction amount
  - `oldbalanceOrg`, `newbalanceOrig`: Account balance changes for origin account
  - `oldbalanceDest`, `newbalanceDest`: Account balance changes for destination account
  - `isFraud`: Target variable (1 = Fraud, 0 = Legitimate)
  - `isFlaggedFraud`: Transactions flagged by rule-based system

---

## ⚙️ Workflow

1. **Data Loading**
   - Import dataset (`Fraud.csv`)
   - Check missing values, duplicates, and class imbalance

2. **Exploratory Data Analysis**
   - Statistical summary
   - Fraud distribution visualization
   - Detection of imbalance in target variable

3. **Feature Engineering & Preprocessing**
   - Dropped irrelevant columns (`nameOrig`, `nameDest`)
   - One-hot encoding for categorical features (`type`)
   - Feature scaling with `StandardScaler`

4. **Train/Test Split**
   - 70% training, 30% testing  
   - Stratified split to maintain class balance

5. **Model Training**
   - **Random Forest Classifier** used as baseline
   - Parameters: `n_estimators=100, random_state=42`

6. **Model Evaluation**
   - Confusion Matrix
   - Classification Report (Precision, Recall, F1-score)
   - ROC-AUC Score (`0.993`)

7. **Feature Importance**
   - Ranked top 10 predictors of fraud
   - Visualized with horizontal bar chart

---

## 📊 Results

- **Confusion Matrix**

