# Product Ranking

## Business Question

How do products rank based on revenue?

---

## Business Importance

Ranking helps identify top-performing products and understand how products compare when multiple products generate the same revenue.

---

## Grain

Product Level

---

## SQL Concepts

- ROW_NUMBER()
- RANK()
- DENSE_RANK()

---

## SQL Approach

Calculated total revenue for each product and applied three different ranking window functions.



---

## Key Insights

- Revenue rankings clearly distinguish premium products from lower-performing products.
- Hoodie and sweatshirt variants consistently occupy the highest positions.
- Product ranking provides a straightforward method for identifying products requiring promotional support or inventory planning.
- Revenue rankings can also support pricing and merchandising decisions.

---

## Business Recommendations

- Feature top-ranked products on high-traffic pages.
- Review lower-ranked products for pricing or promotional opportunities.
- Continuously monitor ranking changes to detect emerging trends.
- Use rankings to prioritize marketing campaigns.---

## Interview Discussion

Different ranking functions serve different reporting needs depending on how ties should be handled.