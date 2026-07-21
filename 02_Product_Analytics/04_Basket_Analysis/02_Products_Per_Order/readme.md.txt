# Products Per Order

## Business Question

How many unique products does a customer typically purchase in a single order?

---

## Business Importance

Products Per Order measures basket diversity by showing how many different products customers include in each purchase. It helps evaluate cross-selling effectiveness and identify opportunities to increase basket variety.

---

## Grain

Order Level

---

## KPIs

- Unique Products per Order
- Average Unique Products per Order

---

## SQL Approach

1. Counted the number of distinct products in each transaction.
2. Calculated the average number of unique products purchased per order.

---

## Output

(Add Screenshot)

---

## Business Insights

(To be completed after analysing the results.)

---

## Product Manager Takeaway

Customers purchasing multiple different products in a single order indicate successful cross-selling. Increasing this metric through recommendations, bundles, or complementary products can improve the shopping experience and overall revenue.

---

## Interview Discussion

The analysis uses `COUNT(DISTINCT item_id)` instead of `SUM(quantity)` because the objective is to measure basket diversity rather than the total number of units purchased. Counting distinct products provides a clearer view of customer purchasing behavior and cross-selling opportunities.