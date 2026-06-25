# 📊 Telco Customer Churn Prediction & Segmentation

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)

An end-to-end machine learning and customer analytics project focused on predicting customer churn and segmenting subscribers to enable targeted retention strategies. This project utilizes the **Telco Customer Churn** dataset to identify high-risk customers, optimize model recall, and group subscribers into actionable behavioral profiles.

---

## 🗺️ Project Architecture & Pipeline

The project is structured into simple, sequential steps as executed in the Jupyter notebook:

### Step-by-Step Overview:
1. **Setup & Load Data**: Import libraries and read the Telco dataset.
2. **Exploratory Data Analysis (EDA)**: Analyze churn rates, tenure distributions, contract types, and service relationships.
3. **Data Cleaning**: Handle missing values (impute empty `Total Charges` to `0`) and drop non-predictive metadata.
4. **Feature Engineering**: One-hot encode categorical features.
5. **Train / Test Split**: Segment the dataset into an 80/20 train/test split.
6. **Model Training & Tuning**: Train baseline and balanced Random Forest classifiers, perform hyperparameter grid search, and run feature selection.
7. **Validation**: Execute 5-fold cross-validation and calculate the ROC-AUC curve.
8. **Customer Segmentation**: Cluster customers using K-Means (K=3) based on tenure, monthly spend, total charges, and predicted churn probability.
---
## 📋 About the Dataset
The analysis is based on the **Telco Customer Churn** dataset ([Telco_customer_churn.xlsx](Telco_customer_churn.xlsx)), which contains subscriber profiles for a telecommunications provider.
*   **Total Records**: `7,043` customers
*   **Total Columns**: `33` columns (including demographics, service settings, billing info, and churn status)
*   **Target Variable**: `Churn Value` (`1` = Churned, `0` = Retained)
*   **Class Balance**:
    *   **Retained (0)**: `5,174` customers (**73.46%**)
    *   **Churned (1)**: `1,869` customers (**26.54%**)

---
## 📈 Key Findings & Insights
*   **Tenure & Churn**: Churned customers have a much shorter average tenure (**17.98 months**) compared to active ones (**37.57 months**).
*   **Contract Type Influence**: Customers on a **Month-to-month** contract have a high churn rate of **42.7%**, compared to just **11.3%** for One-year and **2.8%** for Two-year contracts.
*   **Support Services Impact**: Subscribers who do not have Online Security, Online Backup, or Tech Support show a significantly higher propensity to churn.
*   **Customer Segments (K-Means Clustering)**:
    *   **Cluster 0 (Low Churn Risk / Low Spend)**: 484 customers | Avg Tenure: 33.3 mos | Avg Monthly Charges: $33.40 | Avg Churn Prob: **12.6%**
    *   **Cluster 1 (Moderate Risk / High Spend / Long-Term)**: 391 customers | Avg Tenure: 58.7 mos | Avg Monthly Charges: $90.99 | Avg Churn Prob: **22.7%**
    *   **Cluster 2 (High Risk / Low Tenure / Moderate Spend)**: 534 customers | Avg Tenure: 11.0 mos | Avg Monthly Charges: $72.21 | Avg Churn Prob: **68.0%**

---
## 🤖 Model Performance & Evaluation Metrics
Here are the exact performance metrics obtained from the trained classifiers:

### 1. Classification Metrics Summary
| Model Configuration | Accuracy | Churn Recall (Class 1) | Churn Precision (Class 1) | Churn F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Baseline Random Forest** | 79.28% | 53.00% | 63.00% | 57.00% |
| **Balanced Random Forest** | 79.77% | 51.00% | 65.00% | 57.00% |
| **Tuned Random Forest (Best)** | **77.00%** | **74.00%** | **55.00%** | **63.00%** |
| **Feature-Selected Random Forest** | 77.00% | 73.00% | 56.00% | 63.00% |

### 2. Validation Metrics (Tuned & Final Models)
*   **ROC-AUC Score**: **0.8518** (indicating strong performance in distinguishing churners)
*   **5-Fold Cross-Validation Accuracy**: **77.92% ± 1.35%**
*   **5-Fold Cross-Validation Recall**: **73.30% ± 2.56%**
---
## 📝 Summary

| Step | Key Finding |
|------|-------------|
| EDA | ~26 % churn rate; short-tenure & month-to-month customers churn most |
| Baseline RF | ~78 % accuracy; recall on churners only ~51 % |
| Balanced RF | Better recall (~52 %) with slight accuracy gain |
| Tuned RF (depth=10) | Best balance — recall ~74 %, F1 ~66 % |
| AUC | ~0.857 — good discrimination power |
| K-Means (k=3) | 3 clear segments: high-risk new customers, mid-risk, low-risk long-tenured |
