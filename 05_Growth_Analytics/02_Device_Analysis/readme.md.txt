# 02 Device Analysis

## Business Question

Which device categories generate the highest revenue, completed orders, and purchasing customers?

---

## Business Importance

Customers shop across multiple devices, but not every platform contributes equally to business growth.

Analyzing business performance by device helps product teams identify where revenue is generated and prioritize platform-specific improvements to maximize business impact.

---

## Data Grain

Device Category

Each row represents one device category.

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

Number of distinct users who completed at least one valid purchase.

```sql
COUNT(DISTINCT user_pseudo_id)
```

---

### Revenue Contribution

Percentage contribution of each device to total revenue.

```text
(Device Revenue / Total Revenue) × 100
```

---

## SQL Approach

- Filter valid purchase events.
- Exclude purchases with `NULL` or `(not set)` transaction IDs.
- Group transactions by device category.
- Calculate revenue, completed orders, buyers, and revenue contribution.
- Rank devices by revenue.

---

## Output

| Device | Orders | Revenue | Buyers | Revenue Contribution |
|--------|-------:|--------:|-------:|---------------------:|
| Desktop | 2,559 | 190,365 | 2,143 | 57.64% |
| Mobile | 1,817 | 133,970 | 1,548 | 40.57% |
| Tablet | 83 | 5,925 | 77 | 1.79% |

---

## Business Insights

- **Desktop** was the strongest revenue-generating platform, contributing **190,365** in revenue (**57.64%**) from **2,559** completed orders.
- **Mobile** generated **133,970** in revenue (**40.57%**) and accounted for **1,817** completed orders, highlighting its importance as the second-largest revenue channel.
- **Tablet** contributed only **1.79%** of total revenue, indicating relatively low customer activity on this platform.
- Together, **Desktop** and **Mobile** generated over **98%** of total revenue, making them the primary platforms for business growth.
- Buyer counts are higher when summed across devices because some customers completed purchases on multiple device categories.

---

## Data Validation Notes

During validation, the total completed orders in this analysis (**4,459**) exceeded the validated KPI total (**4,451**) by **8 orders**.

Further investigation showed that these transactions were recorded under more than one device category in the GA4 public sample dataset. As a result:

- Revenue totals remain accurate.
- Device-level metrics should be interpreted as **platform participation** rather than mutually exclusive attribution.
- The discrepancy reflects a limitation of the public dataset rather than an issue with the SQL logic.

---

## Product Manager Takeaway

Device analysis highlights where the business generates the most value.

Desktop remains the dominant revenue platform, while mobile represents a substantial share of business performance. Product teams should continue optimizing both experiences, while recognizing that a small number of transactions may appear across multiple devices due to data inconsistencies in the public GA4 dataset.