# 02 Cohort Analysis

## Business Question

How well do customers from each acquisition month return to make future purchases?

---

## Business Importance

Cohort analysis groups customers based on the month of their first purchase and tracks their purchasing activity over subsequent months.

Unlike overall retention metrics, cohort analysis helps identify whether newer customer groups are becoming more or less engaged over time.

---

## Data Grain

Customer Cohort by Purchase Month

Each row represents a customer cohort and the month in which purchases occurred.

---

## KPI

- Cohort Month
- Purchase Month
- Month Number
- Returning Customers

---

## Metric Definitions

### Cohort Month

The month in which a customer made their first valid purchase.

---

### Purchase Month

The month in which the customer made a purchase.

---

### Month Number

Number of months since the customer's first purchase.

```text
Purchase Month - Cohort Month
```

---

### Returning Customers

Number of unique customers from a cohort who made a purchase during a given month.

---

## SQL Approach

- Filter valid purchase events.
- Remove duplicate purchase records using `ROW_NUMBER()`.
- Identify each customer's first purchase month.
- Track every customer's purchase activity by month.
- Join purchase history with cohort information.
- Calculate the number of returning customers for each cohort over time.

---

## Output

| Cohort Month | Purchase Month | Month Number | Customers |
|--------------|----------------|-------------:|----------:|
| 2020-11 | 2020-11 | 0 | 1,113 |
| 2020-11 | 2020-12 | 1 | 77 |
| 2020-11 | 2021-01 | 2 | 10 |
| 2020-12 | 2020-12 | 0 | 1,828 |
| 2020-12 | 2021-01 | 1 | 37 |
| 2021-01 | 2021-01 | 0 | 772 |

---

## Business Insights

- The **November 2020** cohort started with **1,113** customers, of which **77** returned the following month and **10** were still purchasing two months later.
- The **December 2020** cohort consisted of **1,828** customers, with **37** returning in January 2021.
- The **January 2021** cohort contains only first-month purchases because the public dataset ends in January 2021, leaving no future months available for retention analysis.
- Across all cohorts, customer activity declines noticeably after the first purchase, highlighting the importance of improving long-term customer retention.

---

## Data Limitation

The Google Analytics 4 public ecommerce dataset spans only a few months (November 2020 to January 2021).

As a result, later cohorts have fewer observable months, limiting long-term retention analysis.

---

## Product Manager Takeaway

Cohort analysis provides a clearer picture of customer retention than overall repeat purchase metrics by tracking each customer group independently over time.

The results show that customer activity drops significantly after the initial purchase, suggesting opportunities to improve retention through loyalty programs, personalized recommendations, post-purchase engagement, and lifecycle marketing.