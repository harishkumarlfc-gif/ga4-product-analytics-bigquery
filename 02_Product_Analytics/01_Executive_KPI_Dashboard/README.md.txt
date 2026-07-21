# Executive KPI Dashboard

## Objective

Build an executive-level dashboard that summarizes the overall performance of the ecommerce business using a validated Product Master dataset.

---

## Dataset

Google Merchandise Store (GA4 BigQuery Public Dataset)

---

## Analytical Dataset

Product Master

The Product Master dataset was created after:

- Removing invalid transaction IDs (`(not set)`)
- Removing duplicate transaction-product combinations
- Keeping one unique record per `transaction_id + item_id`

---

## KPIs

| KPI | Description |
|------|