# Model Card: D2C Customer Churn Prediction

## 1. Intended Use
* **Primary Use Case:** To predict which active customers are at high risk of churning in the next 60 days, allowing the retention team to proactively deploy targeted campaigns.
* **Target Audience:** Internal Marketing, Product, and Customer Support teams.
* **Out of Scope:** This model is NOT intended to predict exact lifetime value (LTV) or recommend specific products.

## 2. Data Used
* **Source:** Internal D2C platform data including customer profiles, web events, support tickets, and order history up to the strict snapshot date of `2025-09-30`.
* **Target Variable:** `churn_next_60d` (1 = Churned, 0 = Retained).
* **Leakage Prevention:** All transaction data occurring after `2025-09-30` was strictly excluded from feature creation to prevent the model from learning from the future.

## 3. Model Approach & Top Features
* **Champion Model:** XGBoost Classifier/Random Forest was selected due to its ability to handle non-linear relationships and complex interactions between recent behavior and historical spend.
* **Top Drivers of Churn:** The model identified that churn is heavily driven by:
  1. `recency_days` (Days since last purchase)
  2. `last_visit_days_ago` (App engagement drop-off)
  3. `monetary_180d` (Historical 6-month spend)
  4. `days_since_signup` (Customer maturity)
  5. `avg_discount_pct_180d` (Discount sensitivity)

## 4. Performance & Thresholding
* **Evaluation Metrics:** Evaluated primarily on Precision, Recall, and F1-Score, rather than pure accuracy, due to the imbalanced nature of churn. 
* **Business Threshold:** The default 0.5 probability threshold was lowered to **0.35** to capture more At-Risk customers (increasing recall). The cost of a false positive (giving a discount to someone who wasn't going to churn) is lower than the cost of a false negative (losing a high-value customer completely).

## 5. Ethical Risks & Limitations
* **Limitations:** The model heavily relies on recent web activity; customers who purchase purely offline or through third-party marketplaces may be inaccurately scored.
* **Ethical Considerations:** Ensure that retention campaigns do not inadvertently discriminate against demographic groups by heavily weighting `city_tier` or `age_group` without regular fairness audits.
