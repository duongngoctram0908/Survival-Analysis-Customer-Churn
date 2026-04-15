# 🛡️ Customer Lapse Modeling: A Survival Analysis Approach

![Python](https://img.shields.io/badge/Python-3.13-blue)
![Lifelines](https://img.shields.io/badge/Library-Lifelines-orange)
![Status](https://img.shields.io/badge/Project-Completed-success)

## 📖 Introduction
In the insurance and subscription industries, understanding **when** a customer will leave (Lapse/Surrender) is as critical as knowing **if** they will. This project implements an Actuarial approach to model customer retention using the **Cox Proportional Hazards (CPH)** model. 

The goal is to quantify the impact of various risk factors on the "Time-to-Churn" and generate individual survival curves for dynamic risk assessment.

## 🛠️ Project Pipeline

### 1. Advanced Data Cleaning & Actuarial Preprocessing
Unlike standard machine learning, Survival Analysis requires careful handling of time-to-event data:
- **Deduplication & Missing Value Treatment:** Handled null `TotalCharges` for new customers (`tenure = 0`) by imputing 0, preserving the initial exposure period.
- **Outlier Management (Winsorizing):** Applied IQR-based capping on `MonthlyCharges`. In Actuarial terms, this treats "Jumbo Risks" (extreme premiums) to prevent them from disproportionately biasing the hazard ratios.
- **Feature Encoding:** Transformed categorical variables (Contract, Payment Method, etc.) into numeric formats while ensuring the avoidance of multicollinearity.

### 2. Univariate Analysis (Kaplan-Meier)
- Visualized the overall survival function to identify the baseline retention rate.
- Stratified the portfolio by **Contract Type** to visualize how long-term commitments significantly shift the survival probability "steps."

### 3. Multivariate Modeling (Cox Proportional Hazards)
- **Model Training:** Fitted the CPH model with a `penalizer=0.1` to ensure coefficients remain stable and robust.
- **Hazard Ratio Interpretation:** Analyzed `exp(coef)` to identify key risk drivers.
- **Model Evaluation:** Achieved a **Concordance Index (C-index) of 0.92**, indicating superior predictive power in ranking customer risks.

### 4. Individualized Prediction
- Generated **Individual Survival Curves** for specific customer profiles.
- This allows for "Dynamic Pricing" and "Preventive Underwriting"—identifying high-risk individuals before the lapse event occurs.

## 📊 Key Findings from the Model
- **Contract Power:** 2-year contracts reduce the hazard rate by **95%** compared to month-to-month terms.
- **Service Impact:** Fiber Optic users exhibit a hazard rate **4x higher** than DSL users, suggesting a significant pricing or service quality sensitivity in high-tier segments.
- **Automation:** Customers using electronic checks are **57% more likely** to churn than those on automated payment systems.

## 💻 Technical Requirements
To replicate this analysis, install the following:
```bash
pip install pandas numpy matplotlib lifelines jinja2 openpyxl
