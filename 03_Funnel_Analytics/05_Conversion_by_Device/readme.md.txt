# 05 Conversion by Device

## Business Question

How does purchase conversion differ across desktop, mobile, and tablet users?

---

## Business Importance

User behavior varies across devices due to differences in screen size, browsing experience, and checkout usability.

Analyzing conversion by device helps identify whether a specific platform has a weaker purchase experience and requires optimization.

---

## Data Grain

Device Category

Each row represents one device category.

---

## KPI

- Product View Users
- Purchase Users
- Conversion Rate

---

## Metric Definitions

### View Users

Number of unique users who viewed at least one product.

```sql
COUNT(DISTINCT user_pseudo_id)
```

---

### Purchase Users

Number of unique users who completed a purchase with a valid transaction ID.

```sql
COUNT(DISTINCT user_pseudo_id)
```

---

### Conversion Rate

```text
(Purchase Users / View Users) × 100
```

---

## SQL Approach

- Group users by device category.
- Count unique users who viewed a product.
- Count unique users who completed a valid purchase.
- Calculate the purchase conversion rate for each device.

---

## Output

| Device | View Users | Purchase Users | Conversion Rate |
|---------|-----------:|---------------:|----------------:|
| Mobile | 24,810 | 1,548 | 6.24% |
| Desktop | 36,323 | 2,143 | 5.90% |
| Tablet | 1,443 | 77 | 5.34% |

---

## Business Insights

- **Desktop** generated the highest number of product views (**36,323**) and purchases (**2,143**), making it the largest traffic source by volume.
- **Mobile** achieved the highest purchase conversion rate (**6.24%**), indicating that mobile users who view products are slightly more likely to complete a purchase.
- **Tablet** users represented the smallest audience and recorded the lowest conversion rate (**5.34%**).
- Although conversion rates are relatively similar across devices, improving the desktop checkout experience could have the greatest business impact because it serves the largest number of users.

---

## Product Manager Takeaway

Device-level funnel analysis helps determine whether conversion issues are platform-specific.

Since desktop attracts the largest user base while mobile converts slightly better, optimizing the desktop browsing and checkout experience could produce the largest increase in completed purchases while maintaining the strong mobile experience.