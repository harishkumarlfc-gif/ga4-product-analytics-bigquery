# 04 Stage Conversion

## Business Question

What percentage of users successfully progress from one stage of the purchase funnel to the next?

---

## Business Importance

While Funnel Leakage identifies where users abandon the purchase journey, Stage Conversion measures how efficiently users move between funnel stages.

This analysis helps product teams evaluate the effectiveness of each step and prioritize optimization efforts.

---

## Data Grain

Funnel Stage

Each row represents a transition between two consecutive funnel stages.

---

## KPI

- Previous Stage Users
- Current Stage Users
- Stage Conversion Rate

---

## Metric Definition

Stage Conversion Rate

(Current Stage Users / Previous Stage Users) × 100

---

## SQL Approach

- Count distinct users at each funnel stage.
- Use the previous stage as the denominator.
- Calculate stage conversion percentages.

---

## Output

| Stage | Previous Users | Current Users | Conversion % |
|--------|---------------:|--------------:|-------------:|

---

## Business Insights

- Identifies the strongest and weakest funnel transitions.
- Measures how effectively users progress through the purchase journey.
- Highlights opportunities to improve overall conversion.

---

## Product Manager Takeaway

Increasing conversion at the weakest stage can significantly improve completed purchases without increasing website traffic.