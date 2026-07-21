# Category Ranking

## Business Question

Which product categories rank highest based on total revenue?

---

## Business Importance

Ranking categories helps identify the strongest-performing product groups and supports strategic decisions around marketing, inventory, and merchandising.

---

## Grain

Category Level

---

## KPIs

- Total Revenue
- Revenue Rank

---

## SQL Approach

Aggregated revenue by category and applied the DENSE_RANK() window function to assign rankings while handling ties appropriately.

---

## Output

(Add Screenshot)

---

## Business Insights

(To be completed after analysing the results.)

---

## Product Manager Takeaway

Category rankings provide a quick view of business priorities. Monitoring changes in rankings over time can reveal shifts in customer demand and category performance.

---

## Interview Discussion

`DENSE_RANK()` was chosen because categories with equal revenue receive the same rank without leaving gaps in the ranking sequence, making the output easier to interpret in business reports.