<div align="center">

# 🛒 E-Commerce Business Process Optimization

<br/>

[![Status](https://img.shields.io/badge/Status-Complete-44BBA4?style=for-the-badge)](.)
[![Excel](https://img.shields.io/badge/Excel-Advanced-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](.)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](.)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](.)
[![draw.io](https://img.shields.io/badge/draw.io-BPMN%20%7C%20UML-FF6633?style=for-the-badge)](.)

<br/>

> **Analysed 110,817 real e-commerce orders to identify process inefficiencies, segment customers, and deliver a formally documented system enhancement proposal — using the full BA toolkit.**

<br/>

| 📦 Orders Analysed | 💰 Total Revenue | ⭐ Avg Review Score | 🚚 Avg Delivery |
|:---:|:---:|:---:|:---:|
| **110,817** | **R$ 16,008,872** | **4.09 / 5.0** | **~12 days** |

</div>

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Project Structure](#-project-structure)
- [Phase 2 — Excel](#-phase-2--excel-analysis)
- [Phase 3 — Python](#-phase-3--python-analysis)
- [Phase 4 — Power BI](#-phase-4--power-bi-dashboard)
- [Key Findings](#-key-findings)
- [Skills Demonstrated](#-skills-demonstrated)
- [How to Run](#-how-to-run)
- [Dataset](#-dataset)

---

## 🎯 Project Overview

This project is a complete Analyst portfolio built on the **Olist Brazilian E-Commerce dataset** — 110,817 real orders from Brazil's largest marketplace, adapted to a **Sri Lankan retail context**.

It delivers every artefact a BA role requires:

```
✅ Data Cleaning & ETL          ✅ Customer Segmentation (RFM)
✅ Cohort & Funnel Analysis     ✅ Interactive Dashboards
```

---

## 🔍 Business Problem

Analysis of the existing order management process identified **4 critical operational gaps**:

| # | Pain Point | Data Evidence |
|---|---|---|
| ⚠️ 1 | No automated customer communication at any stage | 0 automated notifications  |
| ⚠️ 2 | No seller SLA monitoring — delays go untracked | Average delivery time exceeds benchmark |
| ⚠️ 3 | 8.8% review gap — no post-delivery prompting | 96,470 delivered vs 88,000 reviewed orders |
| ⚠️ 4 | Manual status updates causing information lag | Status delay visible in Power BI dashboard |

---

## 🗂️ Project Structure

```
BA_Ecommerce_Project/
│
├── 📁 01_Raw_Data/                   ← 9 original Olist CSV files (never modified)
│
├── 📁 02_Excel/
│   └── BA_Project_Main.xlsm          ← Power Query + Data Model + Dashboard + VBA
│
├── 📁 03_Python/
│   ├── BA_Ecommerce_Analysis.ipynb   ← Full analysis notebook
│   ├── rfm_results.csv               ← RFM segmentation output
│   ├── cohort_results.csv            ← Cohort retention matrix
│   ├── funnel_results.csv            ← Funnel analysis output
│   └── *.png                         ← 4 exported chart images
│
├── 📁 04_PowerBI/
│   └── BA_Ecommerce_Dashboard.pbix   ← 4-page interactive dashboard
│
└── README.md
```

---

## 📊 Phase 2 — Excel Analysis

### Power Query ETL Pipeline
8 queries with **non-destructive transformation** — raw CSVs untouched throughout.

- Locale-aware date parsing (Portuguese Brazil format fix)
- Left Outer Joins to attach English category names
- Null removal from critical delivery and approval columns
- Column pruning, data type enforcement, text standardisation

### Data Model — Star Schema

```
         Customers
             │
Reviews ── Orders ── OrderItems ── ProductsEnglish
             │
          Payments
```

**Orders** = central fact table &nbsp;|&nbsp; All others = dimension tables

### Dashboard Features

| Feature | Detail |
|---|---|
| **KPI Cards** | Total Revenue · Total Orders · Avg Order Value · Avg Review Score · Avg Delivery Days |
| **Charts** | Monthly revenue line · Top 10 categories bar · Payment method donut |
| **Interactivity** | Slicers with cross-filtering across all visuals |
| **Advanced Formulas** | XLOOKUP · INDEX MATCH · SUMIFS · SORT · UNIQUE · TAKE · SORTBY |
| **Conditional Formatting** | Heatmaps · Data bars · Traffic light icon sets · Exception highlighting |
| **VBA Macros** | `RefreshDashboard()` · `ExportDashboardPDF()` with date-stamped filename |

---

## 🐍 Phase 3 — Python Analysis

> All analysis in `03_Python/BA_Ecommerce_Analysis.ipynb`

### Libraries Used
```python
pandas           # Data loading, cleaning, transformation
numpy            # Numerical operations
matplotlib       # Chart generation
seaborn          # Chart styling
```

### Analysis 1 — RFM Customer Segmentation

Customers scored **1–5** on three dimensions using quintile scoring (`pd.qcut`):

| Score | Recency | Frequency | Monetary |
|:---:|---|---|---|
| **5** | Bought very recently | Buys very often | Spends most |
| **3** | Moderate recency | Average frequency | Average spend |
| **1** | Has not bought in a long time | Rarely buys | Spends least |

**Segments identified:**

| Segment | Definition | Strategy |
|---|---|---|
| 🏆 Champions | High R + High F + High M | Reward · Request referrals |
| 💛 Loyal Customers | Consistently good scores | Loyalty programme |
| 🆕 New Customers | High R, Low F | Nurture with onboarding |
| ⚠️ At Risk | Low R, was frequent | Re-engagement campaign now |
| ❌ Lost Customers | Low all three | Low-cost win-back only |
| 💎 High Spenders | High M, Low F | Targeted premium offers |
| 🌱 Potential Loyalists | Middle scores | Incentivise next purchase |

### Analysis 2 — Cohort Retention Analysis

Month-on-month retention tracked for every customer cohort from first purchase month.
Results exported as a heatmap matrix — Month 0 = 100%, subsequent months show return rate.

**Key finding:** Sharp drop after Month 0 → heavy reliance on new customer acquisition. Retention programme needed.

### Analysis 3 — Order Funnel Analysis

| Stage | Orders | Conversion |
|---|---:|---:|
| Orders Placed | ~100,000 | 100.0% |
| Orders Approved | ~99,441 | 99.4% |
| Orders Shipped | ~97,600 | 97.6% |
| Orders Delivered | ~96,470 | 96.5% |
| Orders Reviewed | ~88,000 | **88.0%** |

> 🔴 **Biggest gap: Delivered → Reviewed (8.8% loss)** — addressed in FR-004

---

## 📊 Phase 4 — Power BI Dashboard

### 4-Page Dashboard

| Page | Purpose | Key Visuals |
|---|---|---|
| **Sales Overview** | Executive summary | 5 KPI cards · Revenue trend · Top 10 categories · Payment donut · Year slicer |
| **Customer Segmentation** | Customer strategy | RFM donut · Revenue by segment · Scatter plot (Recency × Monetary × Frequency) |
| **Cohort & Funnel** | Retention + efficiency | Retention heatmap matrix · Order funnel chart |
| **Operations** | Performance monitoring | Delivery histogram · State map · Review score by category |

### DAX Measures

```dax
Total Revenue     = SUM(Payments[payment_value])
Total Orders      = DISTINCTCOUNT(Orders[order_id])
Avg Order Value   = DIVIDE([Total Revenue], [Total Orders], 0)
Avg Review Score  = AVERAGE(OrderItems[review_score])
Avg Delivery Days = AVERAGE(Orders[delivery_days])

On Time Rate =
    DIVIDE(
        COUNTROWS(FILTER(Orders,
            Orders[order_delivered_customer_date] <=
            Orders[order_estimated_delivery_date])),
        [Total Orders], 0) * 100
```

> **Python → Power BI:** RFM and cohort results calculated in Python, exported as CSV, imported into Power BI. Each tool doing what it does best.

---

## 📋 Phase 5 — BA Documents

**Requirements:**

| ID | Title | Priority |
|---|---|:---:|
| FR-001 | Automated Order Confirmation Notification | 🔴 High |
| FR-002 | Real-Time Order Status Notifications | 🔴 High |
| FR-003 | Seller SLA Monitoring and Alert System | 🔴 High |
| FR-004 | Automated Post-Delivery Review Request | 🟡 Medium |
| FR-005 | Seller Performance Dashboard | 🟡 Medium |
| FR-006 | Customer Self-Service Order Tracking Portal | 🔴 High |
| FR-007 | Automated Payment Failure Notification | 🔴 High |
| FR-008 | Delivery Failure Automated Handling | 🟡 Medium |
| FR-009 | Customer Notification Preference Management | 🟢 Low |
| FR-010 | Automated Monthly Performance Report | 🟢 Low |

### UAT Test Cases

8 test cases — each with: 

| TC | FR | Title | Priority |
|---|---|---|:---:|
| TC-001 | FR-001 | Automated Order Confirmation | 🔴 High |
| TC-002 | FR-002 | Real-Time Status Notifications | 🔴 High |
| TC-003 | FR-003 | Seller SLA Alert — 48 Hours | 🔴 High |
| TC-004 | FR-006 | Customer Order Tracking Portal | 🔴 High |
| TC-005 | FR-004 | Automated Review Request | 🟡 Medium |
| TC-006 | FR-007 | Payment Failure Notification | 🔴 High |
| TC-007 | FR-005 | Seller Performance Dashboard | 🟡 Medium |
| TC-008 | FR-009 | Notification Preference Management | 🟢 Low |

---

## 📈 Key Findings

| Area | Metric | Value |
|---|---|---|
| Revenue | Total revenue | R$ 16,008,872 |
| Revenue | Average order value | R$ 154.10 |
| Revenue | Top performing category | Health & Beauty |
| Revenue | Top payment method | Credit Card |
| Operations | Average delivery time | ~12 days |
| Operations | Review submission rate | 91.2% (8.8% gap) |
| Customers | Average review score | 4.09 / 5.0 |
| Customers | Unique customers | ~99,000 |

---

## 💼 Skills Demonstrated

<details>
<summary><b>📊 Data Engineering & Excel</b></summary>
<br/>

- ETL pipeline design using Power Query (M language)
- Star schema data modelling with 5 table relationships
- Non-destructive data transformation — raw data never touched
- Cross-table Left Outer Joins and data denormalisation
- Locale-aware date parsing for international datasets
- XLOOKUP, INDEX MATCH, SUMIFS, dynamic arrays (SORT, UNIQUE, TAKE)
- VBA macro automation with user feedback and error handling

</details>

<details>
<summary><b>🐍 Python & Data Analysis</b></summary>
<br/>

- RFM customer segmentation using quintile scoring
- Cohort retention analysis with month-over-month tracking
- Funnel analysis with step-by-step conversion rates
- Time series revenue trend analysis
- Multi-condition aggregation with `groupby().agg()`
- DataFrame merging, boolean filtering, and feature engineering
- Chart generation with matplotlib and seaborn

</details>

<details>
<summary><b>📊 Power BI & Visualisation</b></summary>
<br/>

- DAX measures including conditional `FILTER` calculations
- Cross-filtering and interactive slicers
- Conditional formatting heatmap via Matrix visual
- Python → Power BI integration via CSV export
- 4-page professional dashboard layout and design

</details>


---

## 🚀 How to Run

### Prerequisites

```
Python 3.x with Anaconda
Microsoft Excel Office 365
Power BI Desktop (free)
VS Code + Python + Jupyter extensions
```

### 1 — Get the Dataset
```
1. Visit: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
2. Download and unzip all 9 CSV files
3. Place them inside: 01_Raw_Data/
```

### 2 — Run Python Analysis
```python
# Open VS Code
# Open file: 03_Python/BA_Ecommerce_Analysis.ipynb
# Select kernel: Anaconda base (Python 3.x)
# Update data_path to your local 01_Raw_Data folder path
# Run → Run All Cells

# Output files generated automatically:
# rfm_results.csv  cohort_results.csv  funnel_results.csv
# monthly_revenue.png  rfm_segmentation.png
# cohort_analysis.png  funnel_analysis.png
```

### 3 — Open Excel Workbook
```
1. Open:  02_Excel/BA_Project_Main.xlsm
2. Click: Enable Content (macros must be enabled)
3. Go to: Dashboard sheet
4. Click: Refresh Dashboard button
```

### 4 — Open Power BI Dashboard
```
1. Open:  04_PowerBI/BA_Ecommerce_Dashboard.pbix
2. Click: Refresh if prompted to update data source paths
3. Use page tabs at bottom to navigate between pages
```


---

## 📁 Dataset

**Source:** [Olist Brazilian E-Commerce — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
**License:** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)  
**Period:** October 2016 – October 2018

| File | Rows | Description |
|---|---:|---|
| olist_orders_dataset.csv | ~100,000 | Order master — status and timestamps |
| olist_order_items_dataset.csv | ~113,000 | Line items per order |
| olist_customers_dataset.csv | ~99,000 | Customer location data |
| olist_order_payments_dataset.csv | ~103,000 | Payment method and value |
| olist_products_dataset.csv | ~32,000 | Product catalogue |
| olist_order_reviews_dataset.csv | ~99,000 | Customer review scores |
| product_category_name_translation.csv | 71 | Portuguese → English names |

---

<div align="center">

**Built as a Business Analyst portfolio project · Sri Lanka · 2026**

*If this project was useful, feel free to ⭐ star the repository*

</div>
