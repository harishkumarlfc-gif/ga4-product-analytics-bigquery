# GA4 E-Commerce Product & Conversion Analytics

> **End-to-end Product Analytics case study using GA4 ecommerce event data in BigQuery — from raw event validation to business recommendations and experiment design.**

[![BigQuery](https://img.shields.io/badge/SQL-BigQuery-4285F4?logo=googlebigquery&logoColor=white)](https://cloud.google.com/bigquery) [![GA4](https://img.shields.io/badge/Analytics-GA4-FF6F00?logo=googleanalytics&logoColor=white)](https://analytics.google.com/) [![Power%20BI](https://img.shields.io/badge/BI-Power%20BI-F2C811?logo=powerbi&logoColor=111111)](https://powerbi.microsoft.com/) [![Product%20Analytics](https://img.shields.io/badge/Focus-Product%20Analytics-168A83)](#-product-sense)

---

## TL;DR

I built this project as a **fresher-level end-to-end analytics workflow**, not just a dashboard exercise.

```text
Raw GA4 events
      ↓
Data quality + grain validation
      ↓
Validated Product Master
      ↓
Commercial KPIs + Product Analytics
      ↓
Funnel + Conversion Diagnostics
      ↓
Customer + Retention Analytics
      ↓
Growth Analytics
      ↓
Power BI Dashboard
      ↓
Product Sense: KPI Tree + RCA + Experiments
```

### What the analysis surfaced

| Area | Observed result |
|---|---:|
| Validated orders | **4,451** |
| Buyers | **3,713** |
| Products | **789** |
| Item revenue | **$306,714** |
| Product Master rows | **13,227** |
| Duplicate transaction-product pairs found | **924** |
| Invalid purchase events | **906** |
| View Item users | **61,252** |
| View → Cart drop-off | **79.52%** |
| Checkout → Purchase drop-off | **61.78%** |
| Checkout → Purchase conversion | **38.2%** |
| Average basket size | **4.38 items/order** |
| Average Selling Price | **$19.52** |
| Apparel revenue share | **47.3%** |
| One-time buyers | **88.15%** |
| Repeat buyers | **11.85%** |
| Mobile conversion | **6.24%** |
| Desktop revenue share | **57.6%** |
| Suggested free-shipping test threshold | **~$85** |

> These figures come from the project's public GA4 sample dataset. They are analytical observations, not claimed production business impact.

---

# 1. Why This Project Is Structured This Way

A lot of analytics projects stop at:

**SQL → charts → dashboard.**

This one explicitly connects:

**data quality → metric reliability → business diagnosis → product hypotheses → measurable experiments**.

The central principle is:

> **Trust the data first. Understand what happened next. Then decide what should be investigated or tested.**

Because the public GA4 dataset does not contain enough information to establish causality, the project separates **observations** from **hypotheses** and presents recommendations as experiments rather than guaranteed outcomes.

---

# 2. Analytical Architecture

```text
                    RAW GA4 EVENTS
                          │
                          ▼
              ┌──────────────────────┐
              │ 01 Data Validation   │
              │ Grain / Duplicates   │
              │ Transaction IDs      │
              │ Business Rules       │
              └──────────┬───────────┘
                         │
                         ▼
              ┌──────────────────────┐
              │   PRODUCT MASTER     │
              │ one product /        │
              │ one valid transaction│
              └──────────┬───────────┘
                         │
       ┌─────────────────┼──────────────────┐
       ▼                 ▼                  ▼
 Product Analytics   Funnel Analytics   User/Growth
       │                 │                  │
       └─────────────────┼──────────────────┘
                         ▼
                 Retention Analytics
                         │
                         ▼
                  Power BI Dashboard
                         │
                         ▼
                  Product Sense Layer
              KPI Tree / RCA / Experiments
```

---

# 3. Folder-by-Folder Guide

## 01 — Data Validation

**Folder:** [`01_Data_Validation`](./01_Data_Validation)

This is the foundation of the project.

### 01.1 Grain Validation

**Business question:**

> Does one row really represent **one product purchased in one transaction**?

The repository defines the expected grain as:

```text
One row = One Product + One Transaction
```

Validation checks compare total rows against distinct transaction-product combinations and duplicate rows.

**Result:**

```text
Total rows       = 13,227
Expected rows    = 13,227
Duplicate rows   = 0
```

### Why a recruiter should care

Getting grain wrong can silently corrupt almost every downstream KPI:

```text
wrong grain
   ↓
wrong revenue
   ↓
wrong units
   ↓
wrong orders / AOV
   ↓
wrong product ranking
   ↓
wrong business decision
```

This demonstrates **data modeling and metric integrity thinking**, not just SQL syntax.

---

### 01.2 Duplicate Validation

**Business question:**

> Are transaction-product combinations repeated in the raw purchase layer?

The repository checks the business key:

```text
transaction_id + item_id
```

**Result:**

```text
Unique transaction-product pairs = 13,227
Duplicate pairs found             = 924
Maximum duplicate count           = 15
```

Duplicates are then handled during Product Master construction using `ROW_NUMBER()`.

**Business relevance:** duplicate purchase records can inflate revenue, units, AOV and product rankings.

---

### 01.3 Transaction ID Validation

**Business question:**

> Which purchase events have usable transaction identifiers?

The repository separates:

```text
Valid IDs
NULL IDs
'(not set)' IDs
```

**Result:**

```text
Purchase events       = 5,692
NULL IDs              = 23
'(not set)' IDs       = 883
Valid IDs             = 4,786
Invalid purchase events = 906
```

The data flow is:

```text
5,692 purchase events
        ↓
23 NULL removed
        ↓
883 '(not set)' removed
        ↓
4,786 valid purchase events
        ↓
transaction-item deduplication
        ↓
13,227 Product Master rows
        ↓
4,451 unique orders
```

**Why this matters:** a purchase event is not automatically a trustworthy order for order-level analytics.

---

### 01.4 Business Rule Validation

The project checks ecommerce logic such as:

```text
price × quantity ≈ item_revenue
quantity > 0
price > 0
```

**Revenue validation result:**

```text
Item Revenue        = 306,714
Price × Quantity    = 306,924
Difference          = 210
```

The repository treats `item_revenue` as the authoritative revenue measure and documents the small difference instead of silently ignoring it.

Quantity and price validation found:

```text
Invalid quantity ≤ 0 = 0
Invalid price ≤ 0    = 0
```

**Business relevance:** this is a practical example of validating that a dataset is not only technically queryable, but logically usable.

---

## Product Master — The Reusable Analytical Layer

**File:** [`01_Data_Validation/productmaster.md.txt`](./01_Data_Validation/productmaster.md.txt)

The Product Master connects the raw event model to the business analysis layer.

It combines:

- transaction ID and purchase date
- user ID
- product ID / name / category / brand
- quantity / price / item revenue
- device
- country
- source / medium / campaign

Core construction logic:

```text
Purchase events
    ↓
Remove invalid transaction IDs
    ↓
UNNEST(e.items)
    ↓
Create transaction-product grain
    ↓
ROW_NUMBER() over transaction_id + item_id
    ↓
Keep rn = 1
    ↓
Validated Product Master
```

This layer is reused by the downstream product, customer, funnel, growth and retention analyses.

---

# 02 — Product Analytics

**Folder:** [`02_Product_Analytics`](./02_Product_Analytics)

Once the analytical layer is trustworthy, the project moves to commercial performance.

## 02.1 Executive KPI Layer

The KPI layer includes:

```text
Revenue
Orders
Units sold
Unique products
AOV
ASP
```

Core formulas:

```text
Orders = COUNT(DISTINCT transaction_id)
AOV    = Revenue / Orders
ASP    = Revenue / Units
```

The key idea is denominator discipline: **row count is not automatically order count**.

---

## 02.2 Top Revenue Products

**Folder:** [`02_Product_Analytics/02_Product_Performance/01_Top_Revenue_Products`](./02_Product_Analytics/02_Product_Performance/01_Top_Revenue_Products)

**Business question:**

> Which products contribute the most revenue?

Selected observations documented in the repository:

- Google Zip Hoodie F/C generated **$10,488** in revenue.
- Google Crewneck Sweatshirt Navy generated **$9,878**.
- Apparel products dominate the high-revenue rankings.
- Bottles and backpacks also appear among strong revenue contributors.

### Business use

These results can inform:

- merchandising visibility
- inventory prioritization
- promotional placement
- seasonal campaigns
- complementary-product recommendations

A key analytical distinction is:

```text
Revenue ≠ Units
```

A premium product can generate more revenue without being the volume leader.

---

# 03 — Funnel Analytics

**Folder:** [`03_Funnel_Analytics`](./03_Funnel_Analytics)

This module asks:

> How do users move through the ecommerce purchase journey, and where does the journey leak?

The core funnel is:

```text
View Item
   ↓
Add to Cart
   ↓
Begin Checkout
   ↓
Purchase
```

The folder contains analysis for:

- Event Funnel
- Product Funnel
- Funnel Leakage
- Stage Conversion
- Conversion by Device
- Conversion by Traffic Source

---

## 03.1 Event Funnel

Observed user populations:

```text
View Item        61,252
Add to Cart      12,545
Begin Checkout    9,715
Purchase          3,713
```

The analysis uses unique users at each stage, preventing repeat event activity from being interpreted as additional people.

---

## 03.2 Funnel Leakage

**Folder:** [`03_Funnel_Analytics/03_Funnel_Leakage`](./03_Funnel_Analytics/03_Funnel_Leakage)

The analysis uses `LAG()` to pull the previous stage and calculate users lost.

Formula:

```text
Users Lost  = Previous Users - Current Users
Drop-off %  = Users Lost / Previous Users × 100
```

### Results

| Transition | Users lost | Drop-off |
|---|---:|---:|
| View → Cart | 48,707 | **79.52%** |
| Cart → Checkout | 2,830 | **22.56%** |
| Checkout → Purchase | 6,002 | **61.78%** |

### Product insight

The largest percentage leakage occurs at **View → Cart**.

However, **Checkout → Purchase** is a particularly useful product investigation because users at this stage have already progressed further into the purchase journey.

This produces a more nuanced question than simply:

> "Which stage has the biggest percentage?"

The better product question is:

> "Which leakage represents the most valuable addressable opportunity, given intent, scale and feasibility?"

The current dataset cannot establish the cause.

---

## 03.3 Conversion by Device

Observed:

```text
Mobile conversion   = 6.24%
Desktop revenue     = 57.6% of revenue
```

The correct next step is not to label a device as "bad". It is to identify **which funnel stage creates the device difference**.

Useful follow-up cuts:

- device × funnel stage
- device × source
- device × AOV
- device × product mix

---

## 03.4 Conversion by Traffic Source

The analysis evaluates traffic quality through:

```text
Users
Orders
Conversion
Revenue
AOV
```

The key business idea:

> **Traffic volume alone does not tell you whether acquisition is valuable.**

---

# 04 — User Analytics

**Folder:** [`04_User_Analytics`](./04_User_Analytics)

This module changes the analytical grain.

Earlier:

```text
One row = product in transaction
```

User analysis often needs:

```text
One row = customer
```

That means the Product Master must first be aggregated by user.

Typical user-level metrics include:

- order count
- revenue
- first purchase date
- last purchase date
- repeat / one-time status
- purchase frequency

### Core customer signal

The project found:

```text
One-time buyers = 88.15%
Repeat buyers   = 11.85%
```

This surfaces a **retention opportunity**. It does not, by itself, prove why customers fail to return.

---

# 05 — Growth Analytics

**Folder:** [`05_Growth_Analytics`](./05_Growth_Analytics)

Growth analysis connects acquisition dimensions to downstream behavior and commercial outcomes.

The project uses dimensions such as:

- source
- medium
- campaign
- device
- country
- time

A strong growth-analysis question is not only:

> "Where did users come from?"

but:

> "Which acquisition sources and segments produce meaningful downstream behavior?"

Useful metrics include:

```text
Users
Orders
Conversion
Revenue
AOV
```

This helps distinguish **traffic generation** from **valuable acquisition**.

---

# 06 — Retention Analytics

**Folder:** [`06_Retention_Analytics`](./06_Retention_Analytics)

The repository's cohort framework is based on monthly purchase retention.

Core pipeline:

```text
First purchase
      ↓
Cohort month
      ↓
Distinct customer purchase months
      ↓
Join cohort to purchase months
      ↓
Month number
      ↓
Retained customers
      ↓
Retention rate
```

### Why distinct purchase months?

If one customer buys multiple products in a month, that customer should count as:

```text
1 active customer
```

not:

```text
5 retained customers
```

### Core formula

```text
Retention Rate
=
Retained Customers / Original Cohort Size
```

---

## D1 / D3 / D7 — Transferable Retention Thinking

The repository's main retention analysis is monthly, but the same reasoning extends to daily retention.

```text
First activity / purchase
        ↓
Cohort date
        ↓
Join later events
        ↓
DATE_DIFF
        ↓
D1 / D3 / D7 flags
        ↓
Collapse to one row per user
        ↓
Retention rate
```

For example:

```text
D1 = days since start = 1
D3 = days since start = 3
D7 = days since start = 7
```

The important lesson is:

> **Retention starts with a clear cohort definition and denominator; the percentage comes later.**

---

# 07 — Product Sense

**Folder:** [`07_Product_Sense`](./07_Product_Sense)

This is the bridge from descriptive analytics to decision support.

The module includes:

- KPI Tree
- Root Cause Analysis
- Experiment Ideas
- Product Case Studies
- Executive Recommendations

The common framework is:

```text
Observation
     ↓
Business Impact
     ↓
Hypothesis
     ↓
Experiment
     ↓
Primary Metric
     ↓
Guardrail Metric
```

---

## 07.1 KPI Tree

**File:** [`01_KPI_Tree.md.txt`](./07_Product_Sense/01_KPI_Tree.md.txt)

The project's revenue tree decomposes:

```text
Revenue
│
├── Orders
│   ├── Traffic
│   └── Conversion Rate
│       ├── View → Cart
│       ├── Cart → Checkout
│       └── Checkout → Purchase
│
└── AOV
    ├── Products per Order
    └── ASP
```

This converts a vague question such as:

> "How do we increase revenue?"

into measurable drivers.

---

## 07.2 Root Cause Analysis

**File:** [`02_Root_Cause_Analysis.md.txt`](./07_Product_Sense/02_Root_Cause_Analysis.md.txt)

The project explicitly separates evidence from assumptions.

### Case 1 — Checkout Abandonment

Observed:

```text
Checkout → Purchase conversion = 38.2%
Checkout abandonment           = 61.8%
```

Possible hypotheses:

- checkout UX friction
- payment failures
- limited payment methods
- delivery concerns
- unexpected shipping costs
- technical issues

Additional data requested in the project includes payment outcomes, checkout-step events, errors, shipping options, exit behavior, device performance and session-level diagnostics.

### Case 2 — Low Repeat Purchase

Observed:

```text
One-time buyers = 88.15%
Repeat buyers   = 11.85%
```

Potential hypotheses include competing alternatives, weak engagement, incentives, satisfaction and delivery experience.

The point is not to claim a cause from limited behavioral data; it is to define what should be investigated next.

---

## 07.3 Experiment Design

The project proposes experiments with:

```text
Hypothesis
Control
Treatment
Primary metric
Guardrails
```

### Example — Checkout

**Hypothesis:** simplifying checkout can increase completed purchases.

**Primary metric:**

```text
Checkout → Purchase conversion
```

**Guardrails:**

```text
AOV
Revenue per Visitor
```

### Example — Retention

A proposed test uses personalized post-purchase communication for first-time buyers.

**Primary metric:** Repeat Purchase Rate

**Guardrails:** AOV and incentive cost

---

## 07.4 Executive Recommendations

**File:** [`06_Executive_Recommendations.md.txt`](./07_Product_Sense/06_Executive_Recommendations.md.txt)

The project translates the analysis into five proposed opportunities:

| Opportunity | Primary metric | Guardrail / support |
|---|---|---|
| Reduce checkout abandonment | Checkout → Purchase conversion | AOV, Revenue / Visitor |
| Improve customer retention | Repeat Purchase Rate | AOV, incentive cost |
| Cross-sell accessories with Apparel | AOV | Checkout conversion |
| Test free-shipping threshold | AOV | Purchase conversion, Contribution Margin |
| Personalize product recommendations | CTR | Checkout conversion, Revenue / Visitor |

These are intentionally framed as **testable recommendations**, not guaranteed outcomes.

---

# 4. Selected Business Insights

## Insight 1 — Data quality can change the decision

The project identified **906 invalid purchase events** and **924 duplicate transaction-product pairs** before downstream analysis.

That means the first product question was not:

> "What is the conversion rate?"

It was:

> "Can I trust the data used to calculate it?"

---

## Insight 2 — The biggest funnel drop is not automatically the only priority

```text
View → Cart               79.52% drop-off
Checkout → Purchase       61.78% drop-off
```

The project treats late-stage abandonment as particularly worth investigating because those users have moved further toward purchase intent.

This demonstrates the difference between **ranking a metric** and **interpreting a business opportunity**.

---

## Insight 3 — Revenue can hide a retention problem

The project found:

```text
88.15% one-time buyers
11.85% repeat buyers
```

This suggests a meaningful retention opportunity even when top-line revenue is the headline KPI.

The next step would be to investigate why customers do not return and test targeted retention initiatives.

---

## Insight 4 — Product mix matters

**Apparel contributes 47.3% of observed revenue**, and top revenue rankings contain multiple apparel products.

This supports questions around:

- merchandising
- inventory
- cross-sell
- premium product placement

---

## Insight 5 — Basket size is a growth lever

Average basket size is:

```text
4.38 items/order
```

That makes the following hypotheses relevant:

```text
bundles
cross-sell
recommendations
frequently-bought-together
```

---

## Insight 6 — Price and volume answer different questions

Observed ASP:

```text
$19.52
```

The repository also analyzes price tiers, allowing the analyst to ask whether revenue is being driven by:

```text
volume
price
mix
```

rather than treating revenue as one undifferentiated number.

---

# 5. Dashboard

**Folder:** [`DASHBOARD`](./DASHBOARD)

The Power BI deliverable contains five analytical views covering:

1. Executive Overview
2. Customer & Funnel
3. Growth & Retention
4. Product Performance
5. Product Performance — additional product analysis

The dashboard is the **decision-facing layer** over the validated analytical dataset.

The intended reading path is:

```text
Headline KPI
   ↓
Diagnostic breakdown
   ↓
Behavior / segment
   ↓
Business opportunity
   ↓
Recommended investigation
```

---

# 6. Technical Skills Demonstrated

### BigQuery / SQL

`CTEs` · `UNNEST` · `COUNT(DISTINCT)` · `CASE WHEN` · `GROUP BY` · `ROW_NUMBER()` · `PARTITION BY` · `LAG()` · `DATE_TRUNC` · `DATE_DIFF` · `SAFE_DIVIDE` · `PARSE_DATE` · deduplication · data validation · cohort analysis

### Analytics

Product Analytics · Funnel Analysis · Conversion Analysis · Customer Analytics · Retention / Cohort Analysis · Growth Analytics · Revenue Analytics · Product Performance · KPI Design · Root Cause Analysis · Experiment Design

### BI

Power BI · KPI Dashboards · Data Visualization · Business Storytelling

---

# 7. How to Read This Repository

| Looking for | Start here |
|---|---|
| Data quality / analytical grain | [`01_Data_Validation`](./01_Data_Validation) |
| Product / revenue KPIs | [`02_Product_Analytics`](./02_Product_Analytics) |
| Funnel / CRO | [`03_Funnel_Analytics`](./03_Funnel_Analytics) |
| Customer behavior | [`04_User_Analytics`](./04_User_Analytics) |
| Acquisition / growth | [`05_Growth_Analytics`](./05_Growth_Analytics) |
| Retention / cohorts | [`06_Retention_Analytics`](./06_Retention_Analytics) |
| Product thinking / experiments | [`07_Product_Sense`](./07_Product_Sense) |
| Dashboard | [`DASHBOARD`](./DASHBOARD) |

---

# 8. What I Would Add in a Production Environment

This project uses a public GA4 sample dataset, so some causal questions cannot be answered from the available fields alone.

A production analytics environment could additionally connect:

- payment success / failure data
- checkout-step instrumentation
- customer feedback / NPS
- returns and refunds
- inventory
- contribution margin
- customer support
- controlled experiment results

This distinction is intentional: **the project demonstrates how to move from evidence to hypotheses without presenting hypotheses as facts.**

---

# 9. The Analytical Mindset Behind the Project

```text
What happened?
      ↓
Is the data trustworthy?
      ↓
Where is the biggest measurable opportunity?
      ↓
Who / what segment is affected?
      ↓
What could explain it?
      ↓
What additional data would validate the explanation?
      ↓
What should be tested?
      ↓
What is the primary metric?
      ↓
What are the guardrails?
```

That is the main thing this repository is intended to demonstrate.

---

# Final Takeaway

> **This project is not just a collection of SQL queries. It is a structured Product / Data Analytics workflow built as a fresher: validate the data, model it at the right grain, quantify business performance, diagnose customer behavior, and translate findings into measurable product hypotheses.**

**BigQuery SQL · GA4 · Power BI · Product Analytics · Funnel Analytics · Cohort Retention · Customer Analytics · Growth Analytics · Root Cause Analysis · Experiment Design**