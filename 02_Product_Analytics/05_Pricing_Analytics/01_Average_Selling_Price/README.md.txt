# Average Selling Price (ASP)

## Business Question

What is the average selling price of products sold across all transactions?

---

## Business Importance

Average Selling Price (ASP) is a key pricing metric that helps businesses understand the typical selling price of products. It provides insights into the overall pricing strategy and serves as a benchmark for comparing product categories, monitoring pricing trends, and evaluating changes in product mix.

---

## Grain

Overall Sales Level

---

## KPI

- Average Selling Price (ASP)

---

## SQL Approach

1. Used the validated `product_master` dataset.
2. Calculated the average of the `price` column across all sold products.
3. Rounded the result to two decimal places for reporting.

---

## Output

| Metric | Value |
|--------|------:|
| Average Selling Price | **19.52** |

*(Insert Screenshot Here)*

---

## Business Insights

- The average selling price across all products sold is **19.52**.
- This indicates that most purchases occur within a relatively affordable price range.
- The ASP can be used as a baseline for comparing premium and budget products in subsequent pricing analyses.

---

## Product Manager Takeaway

Monitoring Average Selling Price helps product and merchandising teams evaluate pricing strategy and identify shifts in customer purchasing behavior. Changes in ASP over time may indicate successful premiumization, increased discounting, or changes in the overall product mix.

---

## Interview Discussion

Average Selling Price (ASP) is calculated using the selling price of every product sold, making it a sales-weighted pricing metric. It reflects the average price customers actually paid across all product purchases rather than the average price of the product catalog.