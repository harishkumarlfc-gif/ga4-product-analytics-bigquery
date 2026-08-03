# Transaction ID Validation

## Business Question

Do all purchase events contain valid transaction IDs required for accurate order-level analysis?

---

## Business Importance

Transaction IDs uniquely identify completed customer purchases.

Missing or invalid transaction IDs can:

- Overstate completed purchases
- Distort order-level KPIs
- Affect Average Order Value (AOV)
- Impact basket, retention, and customer analytics

Validating transaction IDs ensures that only legitimate customer purchases are included in the Product Master.

---

## Validation Logic

Each purchase event was classified into one of three categories:

- Valid Transaction IDs
- NULL Transaction IDs
- `(not set)` Transaction IDs

Only purchase events with valid transaction IDs are retained for downstream analysis.

---

## SQL Techniques Used

- COUNT()
- COUNTIF()
- Conditional Aggregation

---

## Validation Results

| Metric | Result |
|---------|-------:|
| Total Purchase Events | **5,692** |
| NULL Transaction IDs | **23** |
| `(not set)` Transaction IDs | **883** |
| Valid Transaction IDs | **4,786** |

The validation identified **906 purchase events** containing invalid transaction identifiers (**23 NULL** and **883 `(not set)`**). These events were excluded during Product Master creation to ensure only valid customer purchases were retained.

---

## Business Outcome

After removing purchase events with NULL and `(not set)` transaction IDs, the Product Master contains only valid purchase records suitable for order-level analytics.

This improves the accuracy of:

- Revenue Analysis
- Order Analysis
- Average Order Value (AOV)
- Basket Analytics
- Customer Analytics
- Retention Analysis

---

## Key Takeaway

Transaction ID validation is a critical data quality step in ecommerce analytics. By excluding **906 invalid purchase events**, the Product Master ensures that all downstream analyses are based on legitimate customer transactions, resulting in accurate and trustworthy business insights.



5692 Purchase Events
        │
        ▼
Remove NULL IDs (23)
        │
        ▼
Remove "(not set)" IDs (883)
        │
        ▼
4786 Valid Purchase Events
        │
        ▼
Deduplicate Transaction–Item Pairs
        │
        ▼
13227 Product Master Rows
        │
        ▼
4451 Unique Orders