# Model Card: D2C Customer Churn Prediction

## 1. Intended Use
* **Primary Use Case:** To predict which active customers are at high risk of churning in the next 60 days, allowing the marketing and customer success teams to proactively deploy targeted retention campaigns.
* **Target Audience:** Internal Marketing, Product, and Customer Support teams.
* **Out of Scope:** This model is NOT intended to predict lifetime value (LTV) or recommend specific products.

## 2. Data Used
* **Source:** Internal D2C platform data including customer profiles, web events, support tickets, and order history up to the strict snapshot date of `2025-09-30`.
* **Target Variable:** `churn_next_60d` (1 = Churned, 0 = Retained).
* **Leakage Prevention:** All transaction data occurring after `2025-09-30` was strictly excluded from feature creation. 

## 3. Model Approach
* **Baseline Model:** Logistic Regression was used to establish a baseline.
* **Champion Model:** XGBoost Classifier was selected due to its ability to handle non-linear relationships and missing values.

## 4. Performance & Thresholding
* **Evaluation Metrics:** Evaluated primarily on Precision, Recall, and F1-Score, rather than pure accuracy, due to the imbalanced nature of churn. 
* **Business Threshold:** The default 0.5 probability threshold was lowered to [Insert your chosen threshold, e.g., 0.35] to capture more At-Risk customers (increasing recall), as the cost of a false positive (giving a discount to someone who wasn't going to churn) is lower than the cost of a false negative (losing a high-value customer).

## 5. Ethical Risks & Limitations
* **Limitations:** The model heavily relies on recent web activity; customers who purchase purely offline or through third-party marketplaces may be inaccurately scored.
* **Ethical Considerations:** Ensure that retention campaigns do not inadvertently discriminate against demographic groups by heavily weighting 'city_tier' or 'age_group' without regular fairness audits.
