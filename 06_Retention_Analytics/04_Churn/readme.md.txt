# 04 Churn Analysis

## Business Question

How many customers churn after their first purchase, and how many become retained customers?

---

## Business Importance

Customer acquisition drives initial growth, but long-term business success depends on retaining customers.

Churn analysis measures the proportion of customers who fail to return after their first purchase, helping product teams evaluate customer loyalty and identify opportunities to improve long-term engagement.

---

## Data Grain

Customer

Each row represents one unique purchasing customer.

---

## KPI

- Churned Customers
- Retained Customers
- Customer Percentage

---

## Metric Definitions

### Churned Customer

A customer who completed exactly one valid purchase.

---

### Retained Customer

A customer who completed two or more valid purchases.

---

### Customer Percentage

```text
(Customer Count / Total Purchasing Customers) × 100
```

---

## SQL Approach

- Filter valid purchase events.
- Remove duplicate purchase records using `ROW_NUMBER()`.
- Count completed orders for each customer.
- Classify customers as either Churned or Retained.
- Calculate the percentage of customers in each segment.

---

## Output

| Customer Status | Customers | Customer Percentage |
|-----------------|----------:|--------------------:|
| Churned Customer | 3,273 | 88.15% |
| Retained Customer | 440 | 11.85% |

---

## Business Insights

- Out of **3,713 purchasing customers**, **3,273 (88.15%)** made only one purchase and never returned.
- Only **440 customers (11.85%)** became repeat buyers, indicating relatively low customer retention.
- The business currently relies heavily on acquiring new customers rather than generating repeat purchases from existing customers.
- Improving customer retention represents a significant opportunity to increase revenue without proportionally increasing customer acquisition costs.

---

## Product Manager Takeaway

Churn is one of the most important indicators of long-term product health.

With nearly **9 out of 10 customers** leaving after their first purchase, improving post-purchase engagement should be a strategic priority. Initiatives such as personalized recommendations, loyalty programs, targeted email campaigns, discounts for repeat purchases, and lifecycle marketing can help reduce churn, increase repeat purchases, and improve customer lifetime value.