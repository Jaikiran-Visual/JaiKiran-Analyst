# 🔍 Bike Buyers SQL Analysis — Demographics & Purchase Behaviour

**Tools:** SQL, SQLite
**Dataset:** 1,000+ customer records
**Date:** June 2026

---

## 📌 Project Overview

Designed a relational database and wrote 7 business-focused SQL queries to identify the highest-value buyer segments in a bike sales dataset. Focused on translating demographic data into actionable marketing recommendations.

---

## 🎯 Business Problem

> *Which customer demographics drive the highest conversion rates, and how should marketing teams prioritize their outreach?*

---

## 🗃️ Database Schema

```sql
CREATE TABLE bike_buyers (
    ID INTEGER PRIMARY KEY,
    Marital_Status TEXT,
    Gender TEXT,
    Income REAL,
    Children INTEGER,
    Education TEXT,
    Occupation TEXT,
    Home_Owner TEXT,
    Cars INTEGER,
    Commute_Distance TEXT,
    Region TEXT,
    Age INTEGER,
    Purchased_Bike TEXT
);
```

---

## 🔎 SQL Queries & Business Questions

### Query 1 — Purchase Rate by Age Group
```sql
SELECT
  CASE
    WHEN Age < 31 THEN 'Young (< 31)'
    WHEN Age BETWEEN 31 AND 54 THEN 'Middle-Aged (31-54)'
    ELSE 'Senior (55+)'
  END AS Age_Group,
  COUNT(*) AS Total_Customers,
  SUM(CASE WHEN Purchased_Bike = 'Yes' THEN 1 ELSE 0 END) AS Buyers,
  ROUND(100.0 * SUM(CASE WHEN Purchased_Bike = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 1) AS Conversion_Rate
FROM bike_buyers
GROUP BY Age_Group
ORDER BY Conversion_Rate DESC;
```

### Query 2 — Conversion by Commute Distance
```sql
SELECT
  Commute_Distance,
  COUNT(*) AS Total,
  SUM(CASE WHEN Purchased_Bike = 'Yes' THEN 1 ELSE 0 END) AS Buyers,
  ROUND(100.0 * SUM(CASE WHEN Purchased_Bike = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 1) AS Conversion_Rate
FROM bike_buyers
GROUP BY Commute_Distance
ORDER BY Conversion_Rate DESC;
```

### Query 3 — Income vs Purchase Behaviour (Window Function)
```sql
SELECT
  Gender,
  ROUND(AVG(Income), 0) AS Avg_Income,
  ROUND(AVG(CASE WHEN Purchased_Bike = 'Yes' THEN Income END), 0) AS Avg_Income_Buyers,
  RANK() OVER (ORDER BY AVG(CASE WHEN Purchased_Bike = 'Yes' THEN Income END) DESC) AS Income_Rank
FROM bike_buyers
GROUP BY Gender;
```

> *(+ 4 more queries in the .sql file)*

---

## 📊 Key Findings

| Variable | Finding |
|---|---|
| **Commute Distance** | 0–1 mile commuters had **40%+ higher conversion** than long-distance commuters |
| **Age Group** | Middle-aged (31–54) had the highest absolute buyer count |
| **Income** | Buyers averaged significantly higher income than non-buyers across all genders |
| **Occupation** | Professionals and skilled manual workers had the strongest conversion rates |

---

## 💼 Business Impact

- ✅ Short-commute segment has **40%+ higher conversion** → prioritize geo-targeted ads in dense urban/suburban areas
- ✅ SQL segmentation model can help increase **marketing ROI by 20–25%** through smarter budget allocation
- ✅ Delivered 3 actionable recommendations for campaign targeting and customer segmentation

---

## 💡 Business Recommendations

1. **Target short-commute urban customers** with "last-mile commute" messaging in city-centre ad placements
2. **Focus budget on middle-aged professionals** — highest volume + strong income profile
3. **Upsell to existing car owners** with 1–2 cars — data shows they buy bikes as a commute supplement

---

## 📁 Files in This Repo

```
├── bike_buyers_analysis.sql    # All 7 SQL queries
├── bike_buyers.db              # SQLite database
├── README.md                   # This file
└── results/
    └── query_outputs.png       # Screenshot of key query results
```

---

## 🔗 Connect

[LinkedIn](https://linkedin.com/in/jaikiran-analyst) | [Email](mailto:jaikivisual@gmail.com)
