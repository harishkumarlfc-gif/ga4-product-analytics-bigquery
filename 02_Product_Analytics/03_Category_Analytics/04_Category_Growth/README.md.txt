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

## Key Insights

- Most categories experienced strong revenue growth during December followed by a decline in January.
- The revenue pattern suggests seasonality, with December generating the highest sales across multiple categories.
- Apparel remained the highest revenue category throughout the analysis period.
- Monitoring category growth helps identify changing customer demand and seasonal purchasing behavior.

---

## Business Recommendations

- Prepare inventory ahead of high-demand periods.
- Increase marketing activity before seasonal revenue peaks.
- Investigate categories with consistent revenue decline.
- Use growth trends to improve demand forecasting and inventory planning.

---

## Key Takeaway

Category growth analysis provides valuable insights into seasonality and changing customer demand, enabling businesses to make proactive merchandising and inventory decisions.