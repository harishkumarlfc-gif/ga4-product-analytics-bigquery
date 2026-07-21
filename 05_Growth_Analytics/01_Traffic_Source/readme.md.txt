# 01 Traffic Source

## Business Question

Which traffic sources generate the highest business value in terms of revenue, completed orders, and purchasing customers?

---

## Business Importance

Acquiring users is only one part of growth. The real objective is to acquire customers who complete purchases and generate revenue.

Traffic source analysis helps evaluate the quality of acquisition channels by comparing the revenue and orders generated from each source. These insights enable marketing teams to allocate budgets toward the most valuable channels.

---

## Data Grain

Traffic Source

Each row represents one acquisition source.

---

## KPI

- Revenue
- Completed Orders
- Buyers

---

## Metric Definitions

### Revenue

Total revenue generated from valid completed purchases.

```sql
SUM(item_revenue)
```

---

### Completed Orders

Number of unique completed transactions.

```sql
COUNT(DISTINCT transaction_id)
```

---

### Buyers

Number of unique users who completed at least one valid purchase.

```sql
COUNT(DISTINCT user_pseudo_id)
```

---

## SQL Approach

- Filter valid purchase events.
- Exclude purchases with `NULL` or `(not set)` transaction IDs.
- Group transactions by traffic source.
- Calculate revenue, completed orders, and buyers.
- Rank traffic sources by total revenue.

---

## Output

| Traffic Source | Orders | Revenue | Buyers |
|---------------|-------:|--------:|-------:|
| Google | 1,286 | 97,068 | 1,178 |
| \<Other\> | 1,005 | 75,086 | 886 |
| (direct) | 969 | 73,292 | 862 |
| (data deleted) | 645 | 42,843 | 563 |
| shop.googlemerchandisestore.com | 557 | 41,971 | 478 |

---

## Business Insights

- **Google** was the strongest acquisition channel, generating the highest **revenue (97,068)**, **completed orders (1,286)**, and **buyers (1,178)**, making it the primary driver of ecommerce growth.
- **Direct** traffic generated **73,292** in revenue from **969** completed orders, suggesting strong brand awareness and repeat visitor engagement.
- **shop.googlemerchandisestore.com** delivered fewer buyers (**478**) but still generated nearly **42,000** in revenue, indicating relatively high-value traffic despite its smaller audience.
- The **(data deleted)** category represents anonymized traffic sources in the GA4 public dataset. While its metrics are reported, no business conclusions should be drawn because the underlying source is intentionally masked.
- Together, **Google** and **Direct** contributed a substantial share of total revenue, highlighting the importance of both search acquisition and brand-driven traffic.

---

## Product Manager Takeaway

Traffic source analysis measures the business impact of acquisition channels rather than simply the amount of traffic they generate.

For this dataset, **Google** is the most valuable growth channel, contributing the highest revenue, order volume, and customer count. Product and marketing teams should continue investing in high-performing acquisition channels while optimizing lower-performing sources to improve overall business growth.