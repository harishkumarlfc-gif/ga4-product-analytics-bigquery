# 03 Retention Analysis

## Business Question

How well does the business retain customers after their first purchase?

---

## Business Importance

Customer retention measures the ability of a business to bring customers back after their initial purchase.

Higher retention rates indicate stronger customer loyalty, greater long-term revenue potential, and lower dependence on acquiring new customers.

---

## Data Grain

Customer Cohort by Purchase Month

Each row represents a customer cohort and a subsequent purchase month.

---

## KPI

- Cohort Size
- Retained Customers
- Retention Rate

---

## Metric Definitions

### Cohort Size

Number of customers who made their first purchase during a given month.

---

### Retained Customers

Number of customers from a cohort who returned and made another purchase in a later month.

---

### Retention Rate

```text
(Retained Customers / Cohort Size) × 100
```

---

## SQL Approach

- Filter valid purchase events.
- Remove duplicate purchase records using `ROW_NUMBER()`.
- Identify each customer's first purchase month.
- Track monthly purchase activity for every customer.
- Calculate cohort sizes.
- Compute retained customers and retention rate for each month after acquisition.

---

## Output

| Cohort Month | Purchase Month | Month Number | Cohort Size | Retained Customers | Retention Rate |
|--------------|----------------|-------------:|------------:|-------------------:|---------------:|
| 2020-11 | 2020-11 | 0 | 1,113 | 1,113 | 100.00% |
| 2020-11 | 2020-12 | 1 | 1,113 | 77 | 6.92% |
| 2020-11 | 2021-01 | 2 | 1,113 | 10 | 0.90% |
| 2020-12 | 2020-12 | 0 | 1,828 | 1,828 | 100.00% |
| 2020-12 | 2021-01 | 1 | 1,828 | 37 | 2.02% |
| 2021-01 | 2021-01 | 0 | 772 | 772 | 100.00% |

---

## Business Insights

- The **November 2020** cohort retained **6.92%** of customers after one month, with only **0.90%** remaining active after two months.
- The **December 2020** cohort recorded a **2.02%** one-month retention rate, indicating lower repeat purchasing compared to the November cohort.
- Retention declines rapidly after the first purchase, suggesting that most customers do not return for additional purchases.
- The **January 2021** cohort contains only Month 0 because the public dataset ends in January 2021, preventing future retention measurement.

---

## Data Limitation

The Google Analytics 4 public ecommerce dataset spans only **November 2020 to January 2021**.

As a result, later cohorts cannot be observed over longer time periods, limiting long-term retention analysis.

---

## Product Manager Takeaway

Retention is one of the strongest indicators of long-term product success.

The low Month 1 retention rates observed across cohorts suggest that improving post-purchase engagement should be a key business priority. Strategies such as loyalty programs, personalized product recommendations, targeted email campaigns, and promotional offers could encourage customers to return and increase lifetime value.