# Data Validation

## Overview

Before building any KPI, dashboard, or business insight, it is essential to validate the underlying data.

This module documents the validation framework applied to the Google Analytics 4 (GA4) Google Merchandise Store dataset available in BigQuery.

The objective is to ensure that downstream product analytics are built on accurate and reliable data.

---

## Validation Framework

This repository validates the dataset in the following order:

- Grain Validation
- Duplicate Validation
- NULL Validation
- Business Rule Validation
- Aggregate Validation
- Freshness Validation

---

## Why Data Validation?

Incorrect data can lead to inaccurate KPIs, misleading dashboards, and poor business decisions.

Each validation includes:

- Business Question
- Expected Result
- SQL Query
- Output Screenshot
- Observation
- Business Impact