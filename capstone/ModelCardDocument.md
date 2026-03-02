# Consolidated Model Card: Healthcare Operational & Financial Analytics

This Model Card provides a structured overview of the **Visit Risk Classification** and **Claim Outcome Prediction** models developed to optimize hospital resource management and financial forecasting.

---

## 1. Model Details
- **Organization:** Hospital Data Science & Finance Department
- **Model Date:** October 2025
- **Model Type:** Random Forest Classifier (Ensemble Learning)
- **Task:** Multi-class classification for Clinical Risk and Financial Claim Status.
- **Target Variables:**
    - `risk_score`: High, Medium, Low
    - `claim_status`: Paid, Pending, Rejected

---

## 2. Intended Use
- **Primary Use:** Advisory support for hospital administrators to allocate staff based on visit risk and for finance teams to forecast cash flow.
- **Intended Users:** Hospital Operations Managers, Clinical Leads, and Medical Billing Specialists.
- **Out-of-Scope:** Clinical diagnosis or automated denial of insurance coverage without human review.

---

## 3. Training Data & Factors
- **Dataset Size:** 25,000 merged records (Patients, Visits, and Billing).
- **Feature Groups:**
    - **Demographic:** `age`, `gender`, `city`.
    - **Clinical/Operational:** `chronic_flag`, `department`, `visit_type`, `length_of_stay_days`.
    - **Financial:** `billed_amount`, `approved_amount`, `amount_difference`, `approval_ratio`.
- **Temporal Handling:** A **time-based split** (earliest 80% for training, latest 20% for testing) was used to simulate real-world deployment.
- **Imbalance Mitigation:** **SMOTE** was applied to create a balanced training distribution of 11,941 instances per class.

---

## 4. Quantitative Performance
*Evaluation performed on a 20% holdout test set.*


| Metric | Visit Risk Model | Claim Outcome Model |
| :--- | :--- | :--- |
| **Overall Accuracy** | **~46%** | **56%** |
| **Primary Class F1-Score** | 0.62 (Low Risk) | 0.70 (Paid) |
| **Critical Class Recall** | **0.10 (High Risk)** | **0.21 (Rejected)** |

---

## 5. Assumptions & Limitations
- **Assumptions:** 
    - Future billing patterns and clinical protocols will remain consistent with 2025 data.
    - Missing values (e.g., `approved_amount`) are accurately represented by training set medians.
- **Limitations:**
    - **Poor Minority Recall:** Both models struggle to identify "High Risk" visits and "Rejected" claims, leading to a high rate of false negatives for critical events.
    - **Feature Overlap:** Inherent similarities between "Pending" and "Rejected" financial markers limit the model's ability to distinguish between them effectively.

---

## 6. Explainability Summary
- **Risk Drivers:** `length_of_stay_days` and `department` (e.g., ICU) are the strongest predictors of high clinical risk.
- **Financial Drivers:** `amount_difference` and `approval_ratio` are the primary signals for claim outcomes.
- **Patient Behavior:** `avg_days_between_visits` acts as a proxy for patient stability, influencing both risk and billing complexity.

---

**Disclaimer:** This model is an advisory tool for operational efficiency. It does not provide medical advice or legal financial determinations. 

