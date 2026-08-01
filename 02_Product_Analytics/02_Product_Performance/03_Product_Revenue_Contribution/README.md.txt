# Product Revenue Contribution

## Business Question

What percentage of total business revenue is contributed by each product?

---

## Business Importance

Revenue contribution helps identify products that have the greatest impact on the business. It enables better prioritization of inventory, promotions, and merchandising strategies.

---

## Grain

Product Level

---

## KPI

Revenue Contribution (%) =
(Product Revenue / Total Revenue) × 100

---

## SQL Approach

Calculated revenue for each product and used a window function to determine each product's percentage contribution to overall revenue.

---

## Output

(Add screenshot)

---


## Key Insights

- Revenue contribution is concentrated among a relatively small number of premium products.
- Google Zip Hoodie F/C contributes the highest percentage of revenue.
- Apparel products consistently contribute more revenue per product than lower-priced accessories.
- Revenue concentration highlights the importance of protecting inventory and visibility for top-performing products.

---

## Business Recommendations

- Prioritize merchandising of high-contributing products.
- Allocate marketing budget towards products with the highest revenue contribution.
- Improve discoverability of premium products through recommendations.
- Monitor inventory closely for top revenue contributors.---

## Interview Discussion

This analysis uses a window function to compare each product's revenue against total business revenue without requiring a separate query for the overall total.