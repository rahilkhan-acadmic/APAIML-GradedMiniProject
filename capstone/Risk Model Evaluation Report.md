# Risk Model Evaluation Report

## Executive Summary
The evaluation focused on comparing a **baseline Logistic Regression** model against an **advanced Random Forest** classifier to predict hospital visit risk levels (**Low, Medium, High**) (pp. 2, 15).

---

## Performance Metrics Comparison


| Metric | Logistic Regression (Baseline) | Random Forest (Untuned) | Random Forest (Tuned) |
| :--- | :---: | :---: | :---: |
| **Overall Accuracy** | ~33% (p. 22) | ~45% (p. 22) | **~46% (p. 22)** |
| **High Risk F1-Score** | **0.26 (p. 16)** | 0.14 (p. 18) | ~0.10 (p. 22) |
| **Low Risk F1-Score** | 0.41 (p. 16) | 0.60 (p. 18) | **~0.62 (p. 22)** |
| **Medium Risk F1-Score** | **0.28 (p. 16)** | 0.23 (p. 18) | ~0.16 (p. 22) |

---

## Key Findings

1. **Ensemble Advantage**  
   The Random Forest models significantly outperformed Logistic Regression in overall accuracy, showing a marked improvement in general classification capability (p. 22).

2. **Class Specificity**  
   All models performed best at identifying **'Low'** risk visits. However, they struggled significantly with **'High'** and **'Medium'** risk categories. Notably, the "advanced" models actually performed worse on High-Risk detection than the baseline (p. 22).

3. **Tuning Impact**  
   Hyperparameter tuning via `RandomizedSearchCV` provided a marginal **1% accuracy boost**. However, it did not resolve the underlying difficulty in distinguishing higher-risk classes and led to a further decline in the High-Risk F1-score (p. 22).

4. **Key Business Metrics**
*   **Recall for High Risk Class:** **~0.10**. 
    *   *Analysis:* The model captures only 10% of actual high-risk visits. This poses a safety risk for operations if used for automated staffing, as 90% of high-risk cases are missed.
*   **Confusion Matrix Insight:** The model frequently misclassifies "High" and "Medium" risk visits as "Low" risk due to the overwhelming historical volume of low-risk data.

5. **Fairness & Segmentation**
*   **By Gender/City:** Performance is consistent across demographics, indicating no significant algorithmic bias.
*   **By Chronic Flag:** Accuracy is slightly higher for patients with a `chronic_flag`, as their visit patterns are more predictable.
  
---

## Conclusion
* While the **Random Forest (Tuned)** model provides the highest overall accuracy, the **Logistic Regression** baseline remains more effective at identifying critical **High-Risk** cases. Future iterations should  prioritize class-balancing techniques to improve clinical utility.
