# Churn Model Error Analysis

## 1. False Positives (Predicted Churn, but Retained)
* **Business Risk:** Wasting retention budget/discounts on customers who would have purchased at full price anyway (margin dilution).
* **Observation:** The model tends to predict churn for customers who simply have long natural purchasing cycles (e.g., they buy large bulk orders every 6 months).

## 2. False Negatives (Predicted Retain, but Churned)
* **Business Risk:** Losing a customer completely because no intervention was triggered. This is the more expensive error.
* **Observation:** The model misses churners who recently had a terrible support experience if their historical buying frequency was very high.

## 3. Manual Review of 10 Specific Cases
--- FALSE POSITIVES (Predicted Churn, but they Stayed) ---
customer_id  actual_churn  predicted_churn  support_tickets  recent_spend
  CUST02054             0                1                0        818.75
  CUST01969             0                1                1       1641.00
  CUST00437             0                1                0        729.22
  CUST00734             0                1                0       2020.81
  CUST00332             0                1                2       2059.80

  --- FALSE NEGATIVES (Predicted Stay, but they Churned) ---
customer_id  actual_churn  predicted_churn  support_tickets  recent_spend
  CUST01801             1                0                1        371.61
  CUST02238             1                0                1       3352.75
  CUST00591             1                0                0        865.39
  CUST01133             1                0                0        779.15
  CUST00867             1                0                1        424.64

