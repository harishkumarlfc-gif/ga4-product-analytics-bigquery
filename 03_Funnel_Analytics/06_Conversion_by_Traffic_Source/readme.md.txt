# 06 Conversion by Traffic Source

## Business Question

Which traffic sources generate the highest purchase conversion rates?

---

## Business Importance

Different acquisition channels attract users with different levels of purchase intent.

Analyzing conversion by traffic source helps product and marketing teams identify high-quality traffic, optimize acquisition strategies, and maximize return on marketing spend.

---

## Data Grain

Traffic Source

Each row represents one traffic source.

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

- Group users by traffic source.
- Count unique users who viewed products.
- Count unique users who completed valid purchases.
- Calculate purchase conversion rate for each traffic source.
- Rank traffic sources by conversion rate.

---

## Output

| Traffic Source | View Users | Purchase Users | Conversion Rate |
|---------------|-----------:|---------------:|----------------:|
| (data deleted) | 4,924 | 563 | 11.43% |
| shop.googlemerchandisestore.com | 6,180 | 478 | 7.73% |
| (direct) | 16,492 | 862 | 5.23% |
| google | 25,105 | 1,178 | 4.69% |
| \<Other\> | 19,201 | 886 | 4.61% |

---

## Business Insights

- The **(data deleted)** traffic source recorded the highest conversion rate (**11.43%**), although the source is anonymized in the public dataset and cannot be interpreted further.
- **shop.googlemerchandisestore.com** achieved the second-highest conversion rate (**7.73%**), suggesting visitors arriving from the official merchandise store have relatively strong purchase intent.
- **Google** generated the highest number of product viewers (**25,105**) and purchases (**1,178**), making it the largest acquisition channel by volume despite a moderate conversion rate (**4.69%**).
- **Direct** visitors converted slightly better (**5.23%**) than Google search traffic, indicating users who visit the site directly may have stronger brand familiarity or purchase intent.
- Improving conversion for high-volume channels such as **Google** could produce a larger increase in total purchases than optimizing smaller, higher-converting channels.

---

## Product Manager Takeaway

Traffic source analysis helps distinguish **traffic quality** from **traffic volume**.

While some channels convert at higher rates, acquisition decisions should consider both conversion efficiency and the number of users each channel brings. Optimizing the conversion rate of high-volume sources like Google can often deliver the greatest business impact.