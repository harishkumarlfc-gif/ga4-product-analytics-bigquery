# 03 Funnel Leakage

## Business Question

At which stage of the purchase funnel are users abandoning the journey?

---

## Business Importance

Understanding where users leave the purchase journey helps product teams identify friction points and prioritize improvements that maximize overall conversion.

Reducing leakage at high drop-off stages can significantly increase completed purchases without acquiring additional traffic.

---

## Data Grain

Funnel Stage

Each row represents one stage of the ecommerce purchase funnel.

---

## KPI

- Users at Each Stage
- Users Lost
- Drop-off Percentage

---

## Metric Definitions

### Users

Number of unique users who reached each funnel stage.

```sql
COUNT(DISTINCT user_pseudo_id)
```

---

### Users Lost

Difference between the previous funnel stage and the current stage.

```text
Users Lost =
Previous Stage Users − Current Stage Users
```

---

### Drop-off Percentage

Percentage of users lost compared to the previous stage.

```text
Drop-off % =
(Users Lost / Previous Stage Users) × 100
```

---

## SQL Approach

- Count distinct users for each funnel event.
- Compare each stage with the previous stage using the `LAG()` window function.
- Calculate the number of users lost.
- Calculate the percentage drop-off between stages.

---

## Output

| Stage | Users | Users Lost | Drop-off % |
|-----------------|------:|-----------:|-----------:|
| View Item | 61,252 | - | - |
| Add to Cart | 12,545 | 48,707 | 79.52% |
| Begin Checkout | 9,715 | 2,830 | 22.56% |
| Purchase | 3,713 | 6,002 | 61.78% |

---

## Business Insights

- More than **61K users** viewed at least one product.
- Nearly **80% of users** dropped before adding a product to their cart, making this the largest leakage point in the funnel.
- Around **77% of users who added a product to their cart** proceeded to checkout, indicating relatively strong purchase intent once users engage with the cart.
- The largest loss after checkout occurred between **Begin Checkout** and **Purchase**, where over **6,000 users** abandoned before completing their order.
- Optimizing product pages, checkout flow, and payment experience could significantly improve overall conversion.

---

## Product Manager Takeaway

The funnel leakage analysis highlights where customers abandon their purchase journey.

The largest opportunity lies in improving the transition from **View Item → Add to Cart**, while reducing friction during the **Checkout → Purchase** stage can directly increase completed orders and revenue without requiring additional user acquisition.