# 01 User Segmentation

## Business Question

How many users complete a purchase compared to those who only browse the store?

---

## Business Importance

Not every visitor becomes a customer.

Segmenting users into buyers and non-buyers provides a high-level view of product performance and highlights the overall effectiveness of the ecommerce experience. This metric is often used as a starting point for understanding user conversion and identifying opportunities to improve customer acquisition.

---

## Data Grain

User

Each row in the intermediate dataset represents a unique `user_pseudo_id`.

---

## KPI

- Buyers
- Non-Buyers
- Total Users
- Purchase Rate

---

## Metric Definitions

### Buyer

A unique user who completed at least one valid purchase.

A purchase is considered valid only when:

- `event_name = 'purchase'`
- `transaction_id IS NOT NULL`
- `transaction_id != '(not set)'`

---

### Non-Buyer

A unique user who interacted with the website but never completed a valid purchase.

---

### Purchase Rate

```text
(Buyers / Total Users) × 100
```

---

## SQL Approach

- Group all events by `user_pseudo_id`.
- Flag users who completed at least one valid purchase.
- Classify users as Buyers or Non-Buyers.
- Count the number of users in each segment.

---

## Output

| User Type | Users |
|-----------|------:|
| Non-Buyer | 266,441 |
| Buyer | 3,713 |

---

## Business Insights

- The dataset contains **270,154 unique users**, of which only **3,713** completed a valid purchase.
- Approximately **98.6%** of users did not convert into customers, while only **1.4%** completed a purchase.
- The large gap between buyers and non-buyers indicates that most visitors leave before completing the purchase journey.
- Improving conversion at critical stages such as product discovery, cart, or checkout could have a significant impact on overall business performance due to the large pool of non-buying users.

---

## Product Manager Takeaway

User segmentation provides a high-level measure of overall conversion performance.

With only **1.4%** of users becoming buyers, increasing conversion even by a small percentage could translate into thousands of additional customers. This analysis establishes the foundation for deeper investigations into user behavior, journey analysis, and customer lifetime value.