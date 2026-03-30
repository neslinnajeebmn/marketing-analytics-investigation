# 📊 Marketing Analytics Investigation: GA4 vs Platform Attribution (E-commerce)

## Overview

This project investigates discrepancies between platform-reported conversions (Meta Ads & Google Ads) and GA4 data in an e-commerce environment.

The goal is to understand whether platform-reported performance can be trusted for decision-making.

---

## Problem Statement

Marketing teams often optimise campaigns based on platform dashboards.

However, these platforms use different attribution models, which can lead to inflated performance reporting.

 Key Question:

**Are platform-reported conversions aligned with actual website performance?**

---

## Dashboard Preview

<img width="938" height="737" alt="image" src="https://github.com/user-attachments/assets/d1edb019-e3d2-49ec-8f97-66a88e4eb790" />

<img width="940" height="731" alt="image" src="https://github.com/user-attachments/assets/593c75d5-7a35-49d9-98aa-08a6d39ff521" />


---

## Key Findings

* 42.5% of platform-reported conversions were not reflected in GA4
* Meta Prospecting campaigns showed the highest discrepancy (~61%)
* Retargeting campaigns appeared strong but were over-attributed
* Brand campaigns showed the closest alignment with GA4

---

## Root Cause Analysis

The discrepancy is driven by:

* Attribution window differences (7-day click, 1-day view)
* View-through conversions (especially in Meta)
* Cross-platform duplication
* Tracking limitations (cookies, cross-device behaviour)

---

## Solution Approach

To address this, a validation-first framework was implemented:

* Use GA4 as a proxy for actual performance
* Compare platform data against GA4
* Identify conversion gaps
* Evaluate campaign reliability before scaling

---

## Dataset

A simulated 90-day dataset (Jan–Mar 2026) representing an e-commerce business:

* GA4 Data → Sessions, Users, Conversions, Revenue
* Google Ads → Cost, Conversions
* Meta Ads → Cost, Conversions

---

## Data Model

### Dimension Tables:

* dim_date
* dim_campaign
* dim_channel
* dim_device
* dim_medium

### Fact Tables:

* tbl_ga4
* tbl_google
* tbl_meta

---

## Key Metrics (DAX)

```DAX
Total Ads Conversions =
[Google Conversions] + [Meta Conversions]

Conversion Gap =
[Total Ads Conversions] - [Total GA4 Conversions]

Gap % =
DIVIDE([Conversion Gap], [Total Ads Conversions])
```

---

## Dashboard Structure

### 1. Performance Overview

* Revenue, Conversions, Cost, ROAS
* Campaign-level performance
* Traffic & engagement insights

### 2. Attribution & Validation

* GA4 vs Ads comparison
* Conversion Gap %
* Campaign-level discrepancy analysis

---

## Key Insight

Platform-reported performance can significantly overstate actual results.

 Marketing decisions should always be validated using GA4 or backend systems before scaling campaigns.

---

## Tools Used

* Power BI (Data Modelling & Visualisation)
* DAX (Measures & Calculations)
* Excel (Data Preparation)

---

## Repository Contents

* `/data` → Raw datasets
* `/pbix` → Power BI dashboard
* `/dax` → DAX measures
* `/images` → Dashboard visuals
* `/docs` → Methodology

---

## 👩‍💻 Author

**Neslin Najeeb**
Digital Marketing & Data Analytics

---

