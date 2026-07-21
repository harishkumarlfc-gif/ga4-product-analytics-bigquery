# 01 Repeat Purchases

## Business Question

How many customers return to make repeat purchases?

---

## Business Importance

Acquiring new customers is expensive, making customer retention a critical driver of long-term business growth.

Analyzing repeat purchasing behavior helps measure customer loyalty and indicates whether the business is successfully encouraging customers to return after their first purchase.

---

## Data Grain

Customer

Each row represents one unique `user_pseudo_id`.

---

## KPI

- One-Time Buyers
- Repeat Buyers
- Repeat Purchase Rate

---

## Metric Definitions

### One-Time Buyer

A customer who completed exactly one valid purchase.

---

### Repeat Buyer

A customer who completed two or more valid purchases.

---

### Repeat Purchase Rate

```text
(Repeat Buyers / Total Buyers) × 100
```

---

## SQL Approach

- Filter valid purchase events.
- Remove duplicate purchase records using `ROW_NUMBER()`.
- Count completed orders for each customer.
- Classify customers as either One-Time Buyers or Repeat Buyers.
- Count customers within each segment.

---

## Output

| Customer Type | Customers |
|--------------|----------:|
| One-Time Buyer | 3,273 |
| Repeat Buyer | 440 |

---

## Business Insights

- Out of **3,713 purchasing customers**, **3,273 (88.15%)** made only a single purchase.
- Only **440 customers (11.85%)** returned to make additional purchases, indicating a relatively low repeat purchase rate.
- The business currently depends heavily on acquiring new customers rather than generating repeat revenue from existing customers.
- Increasing customer retention presents a significant opportunity, as even a modest improvement in repeat purchases could substantially increase lifetime customer value.

---

## Product Manager Takeaway

Repeat purchase analysis provides an early indicator of customer loyalty.

With nearly **9 out of 10 buyers purchasing only once**, improving customer retention should be a strategic priority. Initiatives such as loyalty programs, personalized recommendations, post-purchase engagement, and targeted remarketing campaigns can encourage repeat purchases and increase long-term revenue.