# Duplicate Validation

## Business Question

Does the raw GA4 purchase data contain duplicate product records within the same transaction?

---

## Business Importance

Duplicate transaction-product records can significantly inflate business metrics such as revenue, units sold, Average Order Value (AOV), and product rankings.

Identifying and removing duplicate records is essential to ensure accurate and trustworthy analytical reporting.

---

## Validation Logic

Each unique combination of:

- Transaction ID
- Item ID

should appear only once.

The validation groups the raw purchase data by Transaction ID and Item ID, then counts how many times each combination appears.

Any combination with a count greater than one is classified as a duplicate.

---

## SQL Techniques Used

- Common Table Expressions (CTEs)
- GROUP BY
- COUNT()
- CASE WHEN
- Aggregate Functions

---

## Validation Results

| Metric | Result |
|---------|--------|
| Unique Transaction–Product Pairs | **13,227** |
| Duplicate Transaction–Product Pairs | **924** |
| Maximum Duplicate Count | **15** |

The validation identified **924 duplicate transaction-product combinations** in the raw purchase data, with the highest duplicate occurring **15 times** within the same transaction.

These duplicates were removed in the Product Master using the `ROW_NUMBER()` window function, retaining only the first occurrence of each Transaction ID–Item ID combination.

---

## Business Outcome

Removing duplicate transaction-product records prevents inflated revenue, incorrect unit sales, and misleading product rankings.

This validation ensures that every purchased product is represented only once within each transaction, creating a reliable dataset for downstream Product, Category, Pricing, Basket, Funnel, Retention, and Growth Analytics.

---

## Key Takeaway

Duplicate validation is a critical data quality step in ecommerce analytics. By identifying **924 duplicate transaction-product combinations** and removing them during Product Master creation, the dataset accurately reflects actual customer purchases and provides a trustworthy foundation for business reporting.