# Model Evaluation Report: Insurance Claim Outcome Classification

This report provides a detailed performance evaluation of the classification models developed to predict insurance claim statuses (**Paid**, **Pending**, or **Rejected**) to support hospital financial forecasting.

***

### 1. Claim Model Evaluation Summary

The evaluation compared a baseline **Logistic Regression** model against an **Advanced Random Forest** classifier. Both models were trained on 80% of historical data and evaluated on a 20% time-based holdout set.


| Metric | Logistic Regression (Baseline) | Random Forest (Advanced) |
| :--- | :--- | :--- |
| **Overall Accuracy** | 46% | **56%** |
| **Paid (Majority) F1-Score** | 0.63 | **0.70** |
| **Pending F1-Score** | 0.18 | **0.23** |
| **Rejected F1-Score** | **0.28** | 0.25 |

**Key Findings:**
*   **Superior Accuracy:** The Random Forest model achieved a 10% higher overall accuracy compared to Logistic Regression.
*   **Reliability for 'Paid' Claims:** Both models are most effective at identifying claims that will be successfully paid, with Random Forest reaching a high F1-score of 0.70.
*   **Minority Class Challenges:** Despite using **SMOTE** to balance the training data, both models struggle significantly to differentiate between 'Pending' and 'Rejected' claims.

***

### 2. Business Metric Analysis

To ensure financial safety and operational reliability, specific business-critical metrics were computed:

*   **Recall for Rejected Claims:** **0.21** (Random Forest).
    *   *Impact:* The model only successfully flags 21% of claims that eventually get rejected. This means 79% of rejections are "surprises" to the finance team.
*   **Recall for Paid Claims:** **0.78** (Random Forest).
    *   *Impact:* The model is highly reliable for predicting successful cash inflows, which is useful for baseline revenue forecasting.

***

### 3. Performance Segmentation & Fairness

Performance was segmented across key categories to identify potential gaps in model reliability:

*   **By Insurance Provider:** Accuracy is highest for major providers like **SecureLife** but drops for smaller providers where rejection patterns are less consistent.
*   **By City:** Minor variations in accuracy were observed between **Hyderabad** and **Pune**, likely due to regional differences in billing documentation standards.
*   **By Chronic Flag:** Claims for patients with a `chronic_flag = 1` show slightly higher predictability, as their billing cycles tend to follow more established clinical paths.

***

### 4. Conclusion & Strategic Next Steps

While the Random Forest model is a significant improvement over the baseline, its low recall for "Rejected" claims limits its use for fully automated financial decisions.

*   **Next Step 1:** Implement **Cost-Sensitive Learning** to penalize the model more heavily for missing a 'Rejected' claim.
*   **Next Step 2:** Perform **Advanced Feature Engineering** on the `amount_difference` and `approval_ratio` variables to better distinguish 'Pending' from 'Rejected' statuses.
*   **Next Step 3:** Use the model as a **Human-in-the-Loop** advisory tool to flag high-probability "Paid" claims for fast-tracking while manually reviewing others.

***

**Financial Disclaimer:** This report is generated as requirement for capstone project and should not be used as a final determination for debt write-offs or legal billing actions.


