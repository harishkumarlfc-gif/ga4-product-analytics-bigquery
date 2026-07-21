# Price Buckets

## Business Question

How do different product price segments contribute to the product catalog, sales volume, and revenue?

---

## Business Importance

Price bucket analysis helps businesses understand how products are distributed across different pricing tiers and how each tier contributes to sales performance. These insights support pricing strategy, product assortment planning, merchandising decisions, and revenue optimization.

---

## Grain

Price Bucket

---

## KPIs

- Unique Products
- Units Sold
- Total Revenue

---

## Data Validation

Initially, products were grouped using the transaction-level `price` column. This resulted in products appearing in multiple price buckets because some products were sold at different prices due to discounts and promotional pricing.

Validation showed:

- Total unique products in `product_master`: **789**
- Sum of products across price buckets: **910**

To eliminate double counting:

1. Grouped the data at the product level (`item_id`).
2. Calculated the **average selling price** for each product using `AVG(price)`.
3. Assigned each product to a single price bucket based on its average selling price.
4. Joined the bucket assignments back to the transaction-level data to calculate units sold and revenue.

This ensured that:

- Every product belongs to exactly one price bucket.
- The total number of products across buckets equals **789**.
- Revenue and units sold include every transaction for each product.

---

## SQL Approach

1. Calculated the average selling price for each product.
2. Assigned products to predefined price buckets using a `CASE` statement.
3. Joined the bucketed products back to the Product Master dataset.
4. Aggregated:
   - Unique Products
   - Units Sold
   - Total Revenue

---

## Output

| Price Bucket | Unique Products | Units Sold | Total Revenue |
|--------------|----------------:|-----------:|--------------:|
| Under $10 | 148 | 8,714 | 32,676 |
| $10 - $24.99 | 372 | 7,176 | 112,349 |
| $25 - $49.99 | 171 | 2,534 | 90,920 |
| $50+ | 98 | 1,059 | 70,769 |

*(Insert Screenshot Here)*

---

## Business Insights

- The catalog contains **789 unique products**, with **372 products (47.1%)** priced between **$10 and $24.99**, making it the largest pricing segment.
- Although the **Under $10** segment contains **148 products** and sold the highest number of units (**8,714**), it generated the **lowest revenue (32,676)** due to its lower price point.
- The **$10–$24.99** segment generated the **highest revenue (112,349)** while also maintaining strong sales volume, making it the business's strongest performing price tier.
- Premium-priced products (**$50+**) account for only **98 products (12.4%)** and **1,059 units sold**, yet generated **70,769** in revenue, demonstrating that higher-priced products can contribute significant revenue despite lower sales volume.
- Overall, the results indicate that the business primarily relies on **mid-priced products for revenue**, while premium products provide additional value through higher revenue per unit.

---

## Product Manager Takeaway

The product portfolio is heavily centered around the **$10–$24.99** price range, which balances a broad product assortment with the highest revenue contribution. Budget products drive customer purchases through high sales volume, while premium products generate substantial revenue with relatively few transactions. Maintaining a balanced pricing strategy across these segments can maximize both customer reach and profitability.

---

## Interview Discussion

A key validation step in this analysis was identifying that products were sold at multiple transaction prices. Assigning price buckets directly from transaction-level prices caused products to appear in multiple buckets and inflated the product count.

To resolve this, the average selling price was calculated for each product before assigning price buckets. The bucket assignments were then joined back to the transaction-level dataset, allowing all units sold and revenue to be captured while ensuring each product belonged to only one pricing segment. This approach produced accurate product-level pricing insights without double counting.