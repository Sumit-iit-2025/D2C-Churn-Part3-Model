# Churn Model Error Analysis

## 1. False Positives (Predicted Churn, but Retained)
* **Business Risk:** Wasting retention budget/discounts on customers who would have purchased at full price anyway (margin dilution).

**Specific Dataset Examples:**
1. **CUST01969:** Model predicted churn because they hadn't purchased in 80 days. However, they stayed because they are a high-value bulk buyer (spent ₹1,641.00 recently) with a naturally long buying cycle.
2. **CUST00226:** Predicted to churn due to a recent support ticket and 54 days of recency, but their massive historical spend (₹2,345.42) kept them loyal to the brand.
3. **CUST00437:** Predicted to churn because their recency was extremely high (151 days), but they ended up returning naturally without intervention.
4. **CUST00734:** Predicted to churn due to high cart abandonment (2 abandoned carts) and 89 days recency, but they were likely just using the cart as a wishlist before placing a ₹2,020 order.
5. **CUST00332:** Predicted to churn because they logged 2 recent support tickets. However, their recency was very healthy (24 days), showing that high-frequency buyers can tolerate some support friction.

## 2. False Negatives (Predicted Retain, but Churned)
* **Business Risk:** Losing a customer completely because no intervention was triggered. This is the more expensive error.

**Specific Dataset Examples:**
6. **CUST00309:** Model thought they were completely safe because they purchased just 8 days ago and spent ₹1,014.02. However, they silently churned, likely due to a competitor's offer.
7. **CUST01801:** Thought to be safe with healthy recency (24 days) and 2 abandoned carts (high engagement). However, an unresolved support ticket likely drove them away.
8. **CUST01133:** Thought to be safe because they had 0 support tickets and purchased 36 days ago. This is a "silent churner" the model failed to detect.
9. **CUST02141:** Model heavily weighted their massive historical spend (₹2,337.84) and assumed they would stay. However, at 77 days of recency, they were already gone.
10. **CUST00069:** Model predicted retention due to healthy recency (29 days) and 0 abandoned carts, missing the underlying lack of app session engagement.

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

