# DAX Measures Documentation

This document outlines all DAX measures used in the Marketing Analytics Investigation project.

The measures are grouped based on their purpose to ensure clarity and usability.

---

# 1. GA4 PERFORMANCE METRICS

These metrics represent actual on-site performance (treated as the source of truth).

### Total Sessions

```
Total Sessions =
SUM(tbl_ga4[Sessions])
```

### Total Users

```
Total Users =
SUM(tbl_ga4[Users])
```

### Total Conversions

```
Total Conversions =
SUM(tbl_ga4[Conversions])
```

### GA4 Conversions

```
GA4 Conversions =
[Total Conversions]
```

### Total Revenue

```
Total Revenue =
SUM(tbl_ga4[Revenue])
```

### Total Engaged Sessions

```
Total Engaged Sessions =
SUM(tbl_ga4[Engaged Sessions])
```

---

# 2. ENGAGEMENT & QUALITY METRICS

These metrics evaluate user behaviour and traffic quality.

### Engagement Rate

```
Engagement Rate =
DIVIDE([Total Engaged Sessions], [Total Sessions])
```

### Engagement Per User

```
Engagement Per User =
DIVIDE([Total Engaged Sessions], [Total Users])
```

### Conversions Per User

```
Conversions Per User =
DIVIDE([Total Conversions], [Total Users])
```

### Conversion Rate

```
Conversion Rate =
DIVIDE([Total Conversions], [Total Sessions])
```

### Revenue Per Session

```
Revenue Per Session =
DIVIDE([Total Revenue], [Total Sessions])
```

---

# 3. AD PLATFORM METRICS

These represent platform-reported performance.

### Google Conversions

```
Google Conversions =
SUM(tbl_google[Conversions])
```

### Meta Conversions

```
Meta Conversions =
SUM(tbl_meta[Conversions])
```

### Total Ads Conversions

```
Total Ads Conversions =
[Google Conversions] + [Meta Conversions]
```

### Google Ads Cost

```
Google Ads Cost =
SUM(tbl_google[Cost])
```

### Meta Ads Cost

```
Meta Ads Cost =
SUM(tbl_meta[Cost])
```

### Total Cost

```
Total Cost =
[Google Ads Cost] + [Meta Ads Cost]
```

---

# 4. EFFICIENCY & VALUE METRICS

These help evaluate profitability and performance efficiency.

### ROAS

```
ROAS =
DIVIDE([Total Revenue], [Total Cost])
```

### Cost Per Conversion

```
Cost Per Conversion =
DIVIDE([Total Cost], [Total Conversions])
```

### AOV (Average Order Value)

```
AOV =
DIVIDE([Total Revenue], [Total Conversions])
```

### Paid Revenue

```
Paid Revenue =
[Total Revenue]   // (Assumed from paid channels if filtered)
```

---

# 5. INVESTIGATION METRICS (CORE OF PROJECT)

These are the most important metrics for identifying discrepancies.

### Conversion Gap

```
Conversion Gap =
[Total Ads Conversions] - [Total Conversions]
```

### Gap %

```
Gap % =
DIVIDE([Conversion Gap], [Total Ads Conversions])
```

### Conversion Share %

```
Conversion Share % =
DIVIDE([Total Conversions], [Total Ads Conversions])
```

---

# 6. CONTRIBUTION METRICS

Used to understand distribution and importance.

### Revenue Share %

```
Revenue Share % =
DIVIDE([Total Revenue], CALCULATE([Total Revenue], ALL(dim_campaign)))
```

---

# 7. FLAGS & ANALYTICAL LOGIC

These measures help identify anomalies and performance issues.

### Low Conversion Flag

```
Low Conversion Flag =
IF([Conversion Rate] < 0.02, "Low", "OK")
```

### High Engagement Low Conversion Flag

```
High Engagement Low Conversion =
IF(
    [Engagement Rate] > 0.6 && [Conversion Rate] < 0.02,
    "Mismatch",
    "Normal"
)
```

---

# HOW TO READ THIS MODEL

* GA4 metrics represent actual performance
* Ads metrics represent platform-reported performance
* Gap metrics highlight discrepancies
* Flags help identify anomalies

---

# KEY TAKEAWAY

This model is designed not just for reporting, but for **investigation and decision-making**.

---
