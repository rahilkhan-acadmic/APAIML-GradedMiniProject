# Model Explainability Summary: 

## Visit Risk Classification

This summary consolidates the explainability and performance profiles for the two models developed to predict hospital visit operational and clinical risk (**Low, Medium, High**) (p. 2).

---

## 1. Model Overview
Two primary models were evaluated using a time-based train-test split (80/20) and class imbalance mitigation via **SMOTE** (pp. 2, 15, 21):

*   **Model A (Baseline):** Logistic Regression with balanced class weights (pp. 2, 16).
*   **Model B (Advanced):** Random Forest Classifier, including a version optimized via `RandomizedSearchCV` (pp. 2, 18, 20).

---

## 2. Feature Importance & Engineering Logic
The decision logic for both models is driven by four primary categories of engineered features (p. 21):


| Feature Category | Key Drivers | Business Justification |
| :--- | :--- | :--- |
| **Financial** | `amount_difference`, `approval_ratio` | Measures the gap between billed and approved amounts as a proxy for operational friction. |
| **Operational** | `length_of_stay_days`, `days_between_visit_billing` | Captures resource intensity and administrative complexity of the visit. |
| **Patient History** | `avg_days_between_visits`, `chronic_flag`, `age` | Captures frequency of care and clinical vulnerability. |
| **Contextual** | `department`, `visit_type`, `insurance_provider` | Accounts for varying risk levels across specialties (e.g., ICU vs. General). |

---

## 3. Comparative Performance & Interpretability

### Model A: Logistic Regression (Linear Interpretability)
*   **Behavior:** Provides global interpretability through coefficients, showing the direct linear relationship between features and risk (p. 16).
*   **Performance:** Achieved **~33% accuracy** (p. 22).
*   **Limitation:** Highly limited ability to distinguish between risk categories, suggesting non-linear decision boundaries (p. 22).

### Model B: Random Forest (Non-Linear Complexity)
*   **Behavior:** Captures complex interactions between features (e.g., how `age` interacts with `department_ICU`) (p. 18).
*   **Performance:** Achieved **~45-46% accuracy** after tuning (p. 22).
*   **Interpretability:** Performs best at identifying **Low Risk** visits (F1-score ~0.62) but continues to struggle with **High** (F1-score ~0.10) and **Medium** (F1-score ~0.16) categories (p. 22).

---

## 4. Key Findings for Stakeholders

*   **Low Risk Dominance:** Both models find "Low Risk" the most identifiable category, likely due to clearer patterns in shorter stays and higher approval ratios (p. 22).
*   **Separability Challenges:** High error rates in "High" and "Medium" risk categories suggest these classes share similar feature distributions, making them difficult to separate with current data (p. 22).
*   **Model Selection:** The **Random Forest** is the preferred model for deployment, offering a **12-13% performance lift** over the baseline. 

> **Recommendation:** Future iterations should incorporate clinical diagnosis codes (ICD-10) to potentially improve the detection of High-Risk cases (p. 22).
