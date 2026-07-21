# Category Growth

## Business Question

How has revenue changed month-over-month for each product category?

---

## Business Importance

Category growth analysis reveals how demand changes over time. It helps identify growing categories, detect declining trends, and supports decisions around marketing, inventory, and merchandising.

---

## Grain

Category × Month

---

## KPIs

- Monthly Revenue
- Previous Month Revenue
- Month-over-Month Growth (%)

---

## SQL Approach

1. Aggregated monthly revenue for each product category.
2. Excluded records with blank category values (`item_category = ''`) to ensure accurate category reporting.
3. Used the `LAG()` window function to retrieve the previous month's revenue.
4. Calculated month-over-month (MoM) growth using `SAFE_DIVIDE()` to avoid division-by-zero errors.

---

## Output

(Add Screenshot)

---

## Business Insights

(To be completed after analysing the output.)

---

## Product Manager Takeaway

Monitoring monthly category growth helps identify categories gaining or losing momentum. Growing categories may warrant increased marketing or inventory investment, while declining categories should be investigated for pricing, merchandising, or demand issues.

---

## Interview Discussion

This analysis demonstrates time-series analytics using the `LAG()` window function. Compared with self-joins, `LAG()` provides a simpler and more efficient way to compare a category's current performance with its previous month.