# 03 User Journey

## Business Question

How do users progress through the ecommerce shopping journey from product discovery to completed purchase?

---

## Business Importance

Understanding the customer journey helps product teams identify how users interact with the shopping experience before completing a purchase.

By analyzing user participation across each stage, product managers can identify where users remain engaged, where friction occurs, and which parts of the experience require optimization.

---

## Data Grain

Journey Stage

Each row represents one stage of the ecommerce shopping journey.

---

## KPI

- Unique Users

---

## Metric Definitions

### Unique Users

Number of distinct users who performed each journey event.

Purchase users include only completed purchases where:

- `event_name = 'purchase'`
- `transaction_id IS NOT NULL`
- `transaction_id != '(not set)'`

---

## SQL Approach

- Select key ecommerce journey events.
- Count distinct users at each stage.
- Exclude invalid purchase events.
- Arrange events according to the shopping journey.

---

## Output

| Journey Stage | Users |
|----------------------|------:|
| View Item List | 44 |
| Select Item | 13,180 |
| View Item | 61,252 |
| Add to Cart | 12,545 |
| Begin Checkout | 9,715 |
| Add Shipping Info | 9,714 |
| Add Payment Info | 5,751 |
| Purchase | 3,713 |

---

## Business Insights

- **61,252** users viewed at least one product, representing the largest point of engagement in the shopping journey.
- **12,545** users added products to their cart, indicating that roughly one in five product viewers demonstrated purchase intent.
- Nearly all users who began checkout (**9,715**) also provided shipping information (**9,714**), suggesting minimal friction at this stage.
- The largest decline during checkout occurred between **Add Shipping Info (9,714)** and **Add Payment Info (5,751)**, indicating that payment is a significant point of abandonment.
- **3,713** users successfully completed a purchase, highlighting the opportunity to improve checkout completion.
- The unusually low **View Item List** count is a known limitation of the GA4 public sample dataset and should not be interpreted as representative user behavior.

---

## Product Manager Takeaway

User journey analysis provides an end-to-end view of how customers interact with the ecommerce platform.

The results indicate that the **payment stage** represents the biggest opportunity for checkout optimization. Reducing friction through simplified payment methods, faster checkout, or improved trust signals could increase completed purchases without requiring additional website traffic.