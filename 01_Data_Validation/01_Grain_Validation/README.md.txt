# Grain Validation

## Business Question

Does the Product Master maintain the expected analytical grain of **one row per product purchased in one transaction**?

---

## Business Importance

Establishing the correct grain is the foundation of reliable analytics. Every downstream analysis—including Product, Category, Pricing, Basket, Funnel, Retention, and Growth Analytics—assumes that each row represents a unique product purchased within a transaction.

An incorrect grain can lead to:

- Double-counted revenue
- Inflated order counts
- Incorrect product rankings
- Misleading business insights

---

## Expected Grain

**One Row = One Product Purchased in One Transaction**

Example:

| Transaction ID | Item ID | Status |
|---------------|---------|--------|
| T1001 | Hoodie | ✅ Valid |
| T1001 | Bottle | ✅ Valid |
| T1002 | Backpack | ✅ Valid |

Invalid Example:

| Transaction ID | Item ID | Status |
|---------------|---------|--------|
| T1001 | Hoodie | ❌ Duplicate |
| T1001 | Hoodie | ❌ Duplicate |

---

## Validation Logic

The validation compares:

- Total Rows
- Expected Unique Transaction–Product combinations
- Duplicate Rows

The Product Master satisfies the expected grain if:

**Total Rows = Expected Rows**

and

**Duplicate Rows = 0**

---

## SQL Techniques Used

- Common Table Expressions (CTEs)
- `COUNT()`
- `COUNT(DISTINCT)`
- `ROW_NUMBER()`
- `PARTITION BY`

---

## Validation Results

| Metric | Result |
|---------|--------|
| Total Rows | **13,227** |
| Expected Rows | **13,227** |
| Duplicate Rows | **0** |

✅ The validation confirms that every row in the Product Master represents a unique product within a transaction.

---

## Business Outcome

The Product Master successfully maintains the expected analytical grain, providing a reliable foundation for all downstream analyses. Since no duplicate transaction–product combinations exist after cleaning, metrics such as revenue, units sold, Average Order Value (AOV), and product rankings can be calculated with confidence.

---

## Key Takeaway

Validating the analytical grain is one of the first and most important data quality checks in any analytics project. Ensuring one unique product per transaction prevents duplicate counting and guarantees consistent, trustworthy reporting across all business analyses.