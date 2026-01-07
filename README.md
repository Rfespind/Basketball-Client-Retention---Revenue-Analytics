# 🏀 Basketball Client Retention ML Project

## Project Overview
This project analyzes client behavior from a small basketball coaching business to **predict client retention** (whether a client books another session) and identify the **key behavioral factors** that drive repeat bookings.

Using real session-level data, I engineered time-based and cumulative features, built end-to-end machine learning pipelines, and compared baseline and ensemble models to determine the most effective approach for a small, real-world dataset.

---

## Business Problem
Client retention is critical for small service-based businesses.  
The goal of this project was to answer:

- Which client behaviors indicate a higher likelihood of booking again?
- Can we reliably predict repeat bookings using historical session data?
- Which model performs best on a **small, grouped dataset**?

---

## Dataset
- **Source:** Personal basketball coaching business
- **Size:** ~36 sessions across ~20 clients
- **Granularity:** One row per training session
- **Target Variable:** `Booked_Again` (1 = booked another session, 0 = did not)

> ⚠️ Client data is anonymized or excluded where necessary to preserve privacy.

---

## Feature Engineering
To avoid data leakage and better reflect real client behavior, I created **time-aware and cumulative features**, including:

- Session month and day of week
- Session number per client
- Days since previous session
- Cumulative hours and spend to date
- Running averages of hours and spend
- Client demographics and location (one-hot encoded)

All features were engineered **chronologically per client**.

---

## Modeling Approach

### Key Design Choices
- **GroupKFold cross-validation**  
  Ensures the same client never appears in both train and test folds.
- **End-to-end pipelines**  
  Preprocessing and modeling are combined to prevent data leakage.
- **Class weighting**  
  Used to handle slight class imbalance in repeat bookings.

---

## Models Evaluated

### Logistic Regression (Baseline)
A strong, interpretable baseline model.

**Cross-validated performance:**

| Metric     | Score |
|-----------|-------|
| F1        | ~0.51 |
| Precision | ~0.45 |
| Recall    | ~0.60 |
| ROC-AUC   | ~0.48 |

📌 *Result:* Performance was near random guessing (ROC-AUC < 0.50), indicating linear decision boundaries were insufficient.

---

### 2️⃣ Random Forest Classifier (Final Model)
An ensemble model better suited for nonlinear patterns and small datasets.

**Cross-validated performance:**

| Metric     | Score |
|-----------|-------|
| F1        | **0.63** |
| Precision | **0.71** |
| Recall    | **0.60** |
| ROC-AUC   | **0.67** |

📌 *Result:* Random Forest significantly outperformed Logistic Regression across all metrics, especially ROC-AUC and precision.

---

## Feature Importance (Random Forest)
The Random Forest model highlighted the most influential predictors of retention:

![Feature Importance](images/feature_importance_rf.png)

**Top drivers included:**
- Session month and day of week
- Cumulative spend and hours
- Client age
- Time since previous session
- Client session count

These features reflect **engagement consistency and investment over time**, which aligns with real-world business intuition.

---

## Final Deliverables
- 📓 **Notebook:** Full analysis, modeling, and evaluation  
- 📊 **Visualization:** Feature importance chart  
- 📄 **Report:** Detailed written analysis and conclusions  

📄 **Full Project Report:**  
[Download the report](reports/Basketball_Client_Retention_Report.docx)

---

## Technologies Used
- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib, Seaborn

---

## Key Takeaways
- Group-aware validation is essential for client-level prediction problems.
- Ensemble models can significantly outperform linear baselines on small, behavioral datasets.
- Cumulative engagement metrics are strong predictors of retention.
- Thoughtful feature engineering can outweigh dataset size.

---

## Future Improvements
- Collect additional longitudinal data
- Tune Random Forest hyperparameters
- Explore gradient boosting models
- Deploy as a lightweight retention scoring tool

---

## Author
**Roman Espindola**  
Data Analytics Student | Syracuse University
