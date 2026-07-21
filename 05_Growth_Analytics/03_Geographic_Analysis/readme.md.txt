# 03 Geographic Analysis

## Business Question

Which countries generate the highest revenue, completed orders, and purchasing customers?

---

## Business Importance

Understanding geographic performance helps businesses identify their strongest markets and prioritize regional growth opportunities.

By analyzing revenue, orders, and buyers across countries, product and business teams can make informed decisions about market expansion, localization, inventory planning, and regional marketing investments.

---

## Data Grain

Country

Each row represents one country.

---

## KPI

- Revenue
- Completed Orders
- Buyers
- Revenue Contribution

---

## Metric Definitions

### Revenue

Total revenue generated from valid completed purchases.

```sql
SUM(item_revenue)
```

---

### Completed Orders

Number of distinct completed transactions.

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

### Revenue Contribution

Percentage contribution of each country to total revenue.

```text
(Country Revenue / Total Revenue) × 100
```

---

## SQL Approach

- Filter valid purchase events.
- Remove duplicate purchase records using `ROW_NUMBER()`.
- Exclude purchases with `NULL` or `(not set)` transaction IDs.
- Group transactions by country.
- Calculate revenue, completed orders, buyers, and revenue contribution.
- Rank countries by revenue.

---

## Output

| Country | Orders | Revenue | Buyers | Revenue Contribution |
|---------|-------:|--------:|-------:|---------------------:|
| United States | 1,939 | 136,029 | 1,619 | 44.35% |
| India | 405 | 28,640 | 339 | 9.34% |
| Canada | 362 | 26,135 | 298 | 8.52% |
| United Kingdom | 136 | 9,756 | 118 | 3.18% |
| Spain | 106 | 6,859 | 76 | 2.24% |
| ... | ... | ... | ... | ... |

---

## Business Insights

- **United States** was the largest market, generating **136,029** in revenue (**44.35%**) from **1,939** completed orders and **1,619** buyers.
- **India** ranked second with **28,640** in revenue (**9.34%**), followed by **Canada** with **26,135** (**8.52%**).
- The top three countries contributed over **62%** of total revenue, indicating that business growth is concentrated in a relatively small number of markets.
- Several European and Asia-Pacific countries generated meaningful revenue, suggesting opportunities for continued international growth and localization.

---

## Data Validation Notes

Revenue from the geographic analysis reconciles with the validated business KPI (**306,714**).

However, the total number of completed orders across countries (**4,462**) is **11 higher** than the validated KPI total (**4,451**).

Validation revealed that **11 transaction IDs were associated with multiple countries** in the GA4 public sample dataset. As a result, those transactions are counted in more than one geographic group when aggregating by country.

This discrepancy is a limitation of the public dataset rather than an issue with the SQL logic and should be considered when interpreting country-level order counts.

---

## Product Manager Takeaway

Geographic analysis identifies where business growth is concentrated and helps prioritize regional investment.

The United States is the primary revenue-generating market, while India and Canada represent important secondary markets. These insights can guide decisions around localization, marketing allocation, inventory planning, and future market expansion, while acknowledging minor geographic inconsistencies present in the public GA4 dataset.