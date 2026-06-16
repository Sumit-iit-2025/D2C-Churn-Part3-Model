# Churn Model Error Analysis

## 1. False Positives (Predicted Churn, but Retained)
* **Business Risk:** Wasting retention budget/discounts on customers who would have purchased at full price anyway (margin dilution).
* **Observation:** The model tends to predict churn for customers who simply have long natural purchasing cycles (e.g., they buy large bulk orders every 6 months).

## 2. False Negatives (Predicted Retain, but Churned)
* **Business Risk:** Losing a customer completely because no intervention was triggered. This is the more expensive error.
* **Observation:** The model misses churners who recently had a terrible support experience if their historical buying frequency was very high.

## 3. Manual Review of 10 Specific Cases
*(Note: Replace these IDs and notes with actual outputs from your test set analysis)*
1. **CUST02352:** False Positive. High web activity, zero purchases in 30 days. Model thought they were leaving, but they were just browsing before a big holiday purchase.
2. **CUST02364:** False Negative. High historical spend, but an unresolved 40-hour support ticket caused them to leave. Model under-weighted the negative ticket rate.
3. [Add CUST_ID 3]
4. [Add CUST_ID 4]
5. [Add CUST_ID 5]
6. [Add CUST_ID 6]
7. [Add CUST_ID 7]
8. [Add CUST_ID 8]
9. [Add CUST_ID 9]
10. [Add CUST_ID 10]
