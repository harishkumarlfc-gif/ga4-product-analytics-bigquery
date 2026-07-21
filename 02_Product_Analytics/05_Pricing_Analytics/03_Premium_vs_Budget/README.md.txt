# Premium vs Budget Products

## Business Question

How do budget and premium products compare in terms of product assortment, sales volume, revenue, and pricing?

---

## Business Importance

Comparing budget and premium products helps businesses understand how different pricing segments contribute to overall business performance. These insights support pricing strategy, merchandising decisions, inventory planning, and product portfolio optimization.

---

## Grain

Pricing Segment

---

## KPIs

- Unique Products
- Units Sold
- Total Revenue
- Average Selling Price (ASP)

---

## Data Validation

Initially, products were classified using the transaction-level `price` column. However, validation showed that some products were sold at different prices due to discounts and promotional pricing, causing the same product to appear in multiple pricing segments.

To ensure accurate segmentation:

1. Products were grouped by `item_id`.
2. The average selling price (`AVG(price)`) was calculated for each product.
3. Each product was assigned to a single pricing segment:
   - **Budget:** Average Selling Price < $25
   - **Premium:** Average Selling Price ≥ $25
4. The pricing segments were joined back to the transaction-level data to calculate sales and revenue.

This ensured that:

- Every product belongs to exactly one pricing segment.
- Product counts remain accurate.
- Revenue and units sold include every transaction for each product.

---

## SQL Approach

1. Calculated the average selling price for each product.
2. Classified products into Budget and Premium segments.
3. Joined the pricing segments back to the Product Master dataset.
4. Aggregated:
   - Unique Products
   - Units Sold
   - Total Revenue
   - Average Selling Price

---

## Output

| Pricing Segment | Unique Products | Units Sold | Total Revenue | Average Selling Price |
|-----------------|----------------:|-----------:|--------------:|----------------------:|
| Budget | 520 | 15,890 | 145,025 | 10.91 |
| Premium | 269 | 3,593 | 161,689 | 45.39 |

*(Insert Screenshot Here)*

---

## Business Insights

- The product catalog contains **520 Budget products (65.9%)** and **269 Premium products (34.1%)**, indicating that the assortment is primarily focused on affordable products.
- Budget products generated **15,890 units sold**, more than **four times** the sales volume of Premium products (**3,593 units**), suggesting customers purchase lower-priced products much more frequently.
- Despite lower sales volume, **Premium products generated the highest revenue (161,689)**, outperforming Budget products (**145,025**). This highlights the strong revenue contribution of higher-priced products.
- The average selling price differs significantly between the two segments:
  - **Budget:** **10.91**
  - **Premium:** **45.39**
- These results indicate that **Budget products drive customer demand and transaction volume**, while **Premium products drive overall revenue**.

---

## Product Manager Takeaway

The business benefits from a balanced pricing strategy. Budget products attract customers and generate high purchase volume, while Premium products contribute disproportionately to revenue through higher-value purchases. Maintaining a healthy mix of both segments can maximize customer acquisition while sustaining revenue growth.

---

## Interview Discussion

A key validation step in this analysis was identifying that products were sold at multiple transaction prices due to discounts and promotions. Using transaction-level prices would have assigned the same product to multiple pricing segments.

To address this, each product was classified using its average selling price before calculating business metrics. This ensured accurate product segmentation while preserving complete sales and revenue information for every product.