# 🛡️ Shield Insurance Analytics Dashboard

A comprehensive Power BI analytics solution designed to track Insurance Performance, Revenue Performance, and Geographical Performance. The main focus of this dashboard was to design three important pages covering Executive View, Sales Mode Analysis, and Age Group Analysis.

---

## 📌 Project Overview

The Shield Insurance Dashboard is a data-driven Power BI project built to analyse insurance business performance across three core dimensions:

- **Insurance Performance** — policy sales, settlement risk, and customer segments
- **Revenue Performance** — monthly trends, sales mode contribution, and growth patterns  
- **Geographical Performance** — city revenue ranking and regional penetration gaps

---

## 🔍 Analysis Questions Covered

### Part 1 — Primary Analysis (10 Questions)
1. Monthly Revenue Trend — what is the MoM growth rate?
2. Top 5 Cities by Revenue — how concentrated is geographic revenue?
3. Age Group Revenue Split — which age group contributes highest revenue?
4. Customer Split by Sales Mode — which channel brings most customers?
5. Revenue Split by Sales Mode — which channel generates most revenue?
6. Daily Customer Growth Trend — which month peaked highest?
7. Age Group vs Expected Settlement — which group carries highest risk?
8. Customer Distribution by Age Group — where is the customer base concentrated?
9. Age Group vs Policy Preference — what policy type does each age group prefer?
10. Month-over-Month Customer Change % — are we consistently growing?

### Part 2 — Secondary Analysis (3 Questions)
11. Revenue per Customer by Sales Mode (ARPC) — which channel has highest value?
12. Settlement Risk vs Revenue Imbalance — which age group is most exposed?
13. Geographic Revenue vs Customer Penetration Gap — which regions underperform?

---

## 🗂️ Data Model

**Tables:**
- `fact_premiums` — customer_code, date, final_premium_amt(INR), policy_id, sales_mode
- `fact_settlements` — age, settlement %
- `dim_Customer` — age, Age_Group, city, customer_code, dob
- `dim_policies` — base_coverage_amt, base_premium_amt, policy_id
- `dim_date` — date, day_type, mmm_yy, Month_Number, week_no

---

## 🧮 DAX Measures
Here, I included only the most important DAX measures. I created more than 30+ measures to track overall performance.

```dax
-- Total Premium
Total Premium = 
SUM(fact_premiums[final_premium_amt(INR)])

-- Expected Settlement
Expected Settlement = 
SUMX(
    fact_premiums,
    VAR CustomerAge = RELATED(dim_Customer[age])
    VAR SettlePct = 
        LOOKUPVALUE(
            fact_settlements[settlement %],
            fact_settlements[age], CustomerAge
        )
    RETURN
        fact_premiums[final_premium_amt(INR)] * SettlePct
)

-- Annual Expected Settlements
Annual Expected Settlements = 
[Expected Settlement]

-- Month-over-Month Growth
MoM Growth % = 
DIVIDE(
    [Total Premium] - CALCULATE([Total Premium], PREVIOUSMONTH(dim_date[date])),
    CALCULATE([Total Premium], PREVIOUSMONTH(dim_date[date]))
)
```
## 📊 Key Metrics

- Total Policies Sold - 27,000 
- Total Premium Paid - ₹989.25M 
- Top Age Group - 31–40 (₹356.03M Revenue) 
- Top Sales Channel - Offline Agent (55%) 
- Analysis Period - Nov 2022 — Apr 2023 

---
## 💡 Key Insights

**Revenue**
- Revenue peaked at ₹263.84M in March 2023 — a 100% increase from Mar 2023
- April 2023 softened to ₹153.75M — seasonal correction or churn signal

**Customer & Sales Mode**
- Offline Agent dominates with 55% of all customers
- Broker channel delivers the highest ARPC at ₹37,420 — 38% above Online average

**Age Group**
- 31–40 is the #1 revenue engine at ₹356.03M
- 18–24 is the highest long-term growth opportunity
- 65+ carries ₹184.89M in settlements with only 19% revenue contribution

**Risk**
- 65+ shows the most critical risk-to-revenue imbalance
- Actuarial reserve review urgently recommended for 51–65 and 65+ bands

**Geography**
- Top 5 cities drive majority of revenue — classic 80/20 concentration
- 
---
## 🎬 Video Presentation
> Click the thumbnail above to watch the full Shield Insurance 
> Dashboard presentation and data story walkthrough.

[![Shield Insurance Dashboard Walkthrough](https://www.youtube.com/watch?v=6IxeA9Ky8Wk&t=12s)]([https://www.youtube.com/watch?v=6IxeA9Ky8Wk&t=12s](https://www.youtube.com/watch?v=6IxeA9Ky8Wk&t=12s))

## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| Power BI Desktop | Dashboard design and visualisation |
| Power BI Service | Used to publish, share, and access reports online |
| DAX | Calculated measures and KPIs |
| Power Query | Data transformation and modelling |
| Excel / CSV | Raw data source |

---

## 📁 Project Structure
Shield-Insurance-Dashboard/

├── 📊 ShieldInsurance.pbix        # Power BI file


├── 📂 img/

│   ├── home_page.png

│   ├── executive_view.png

│   ├── sales_mode_analysis.png

│   └── age_group_analysis.png

│   └── data model.png

└── 📄 README.md

---

## 📸 Dashboard Preview

### Executives Analysis
High-level KPI summary for leadership — total revenue, customer count, top performing age group, and monthly growth trend at a glance.
![Age Group Dashboard](https://raw.githubusercontent.com/Revathi-jaisankar/Shield-Insurance-Analysis/main/img/Executive_page.png)

### Age Group Analysis
Customer and revenue breakdown by age — 31 to 40 is the top revenue engine, 65+ carries the highest settlement risk, and 18 to 24 is the biggest long-term growth opportunity.
![Age Group Dashboard]([Screenshots/age_group_analysis.png](https://github.com/Revathi-jaisankar/Shield-Insurance-Analysis/blob/main/img/Age_group_Analysis_Page.png))

### Sales Mode Analysis
Deep dive into how customers are buying — Offline Agent leads at 55% of customers and dominates revenue, while Online channels are growing in volume.
![Sales Mode Dashboard]([Screenshots/sales_mode_analysis.png](https://github.com/Revathi-jaisankar/Shield-Insurance-Analysis/blob/main/img/Sales_Mode_Analysis_Page.png))

---

# Revathi Ganesan  
### Data Analyst Intern | Power BI | SQL | Excel  

📊 I specialize in creating insightful dashboards and data-driven solutions  
🌍 Based in UAE  
🎯 Focused on business intelligence and analytics  

🔗 [LinkedIn](https://www.linkedin.com/in/revathi-ganesan-576a37121/) · [GitHub](https://github.com/Revathi-jaisankar)

## 📄 License

This project is for educational and portfolio purposes.
