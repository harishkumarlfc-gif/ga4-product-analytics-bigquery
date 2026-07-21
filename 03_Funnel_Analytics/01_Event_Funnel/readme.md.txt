# 01 Event Funnel

## Business Question

How many unique users successfully progress through each stage of the ecommerce purchase journey?

---

## Business Importance

The Event Funnel provides a high-level view of customer progression from product discovery to completed purchase.

It helps identify where the largest user drop-offs occur and highlights stages that require optimization to improve conversion rates.

---

## Data Grain

Event Level

Each row in the output represents a funnel event and the number of unique users who reached that stage.

---

## KPI

Unique Users per Funnel Stage

---

## Metric Definition

Unique Users

```sql
COUNT(DISTINCT user_pseudo_id)
```

For the purchase stage, only events with a valid transaction ID are considered completed purchases.

---

## Funnel Stages

1. View Item
2. Add to Cart
3. Begin Checkout
4. Purchase

---

## SQL Approach

- Filter only the four funnel events.
- Count distinct users at each stage.
- Filter purchase events to include only valid transaction IDs.
- Sort events in the natural funnel order.

---

## Output

| Funnel Stage | Users |
|--------------|------:|
| View Item | 61,252 |
| Add to Cart | 12,545 |
| Begin Checkout | 9,715 |
| Purchase | 3,713 |

---

## Business Insights

- Over **61K users** viewed at least one product.
- Approximately **12.5K users** added a product to their cart.
- Around **9.7K users** proceeded to checkout.
- **3.7K users** successfully completed a purchase.
- The largest user drop occurs before the Add to Cart stage, indicating an opportunity to improve product pages and purchase intent.

---

## Product Manager Takeaway

The Event Funnel measures how users progress through the purchase journey.

Unlike Product Analytics, which measures orders and revenue, Funnel Analytics measures people.

This analysis helps product managers identify where customers abandon the buying journey so they can prioritize improvements that increase conversion.