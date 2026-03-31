<div align="center">

# 🛒 E-Commerce Business Process Optimization
### End-to-End Business Analyst Portfolio Project — Sri Lankan Retail Context

<br/>

[![Status](https://img.shields.io/badge/Status-Complete-44BBA4?style=for-the-badge)](.)
[![Excel](https://img.shields.io/badge/Excel-Advanced-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](.)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](.)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](.)
[![draw.io](https://img.shields.io/badge/draw.io-BPMN%20%7C%20UML-FF6633?style=for-the-badge)](.)
[![Word](https://img.shields.io/badge/Word-FRS%20%7C%20UAT-2B579A?style=for-the-badge&logo=microsoft-word&logoColor=white)](.)

<br/>

> **Analysed 110,817 real e-commerce orders to identify process inefficiencies, segment customers, and deliver a formally documented system enhancement proposal — covering the complete BA toolkit from raw data to signed UAT test cases.**

<br/>

| 📦 Orders Analysed | 💰 Total Revenue | ⭐ Avg Review Score | 🚚 Avg Delivery | 🔍 Review Gap |
|:---:|:---:|:---:|:---:|:---:|
| **110,817** | **R$ 16,008,872** | **4.09 / 5.0** | **~12 days** | **8.8%** |

</div>

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Project Structure](#-project-structure)
- [Phase 2 — Excel](#-phase-2--excel-analysis)
- [Phase 3 — Python](#-phase-3--python-analysis)
- [Phase 4 — Power BI](#-phase-4--power-bi-dashboard)
- [Phase 5 — BA Documents](#-phase-5--ba-documents)
- [Key Findings](#-key-findings)
- [Skills Demonstrated](#-skills-demonstrated)
- [How to Run](#-how-to-run)
- [Dataset](#-dataset)

---

## 🎯 Project Overview

This is a complete, end-to-end **Business Analyst portfolio project** built on the **Olist Brazilian E-Commerce dataset** — 110,817 real orders from Brazil's largest marketplace, framed in a **Sri Lankan retail context** relevant to companies like Daraz, Keells, Cargills, PAYable, and Sysco.

Every deliverable mirrors what a BA produces on a real job:

```
✅ ETL Pipeline & Data Cleaning        ✅ RFM Customer Segmentation
✅ Star Schema Data Model               ✅ Cohort Retention Analysis
✅ Interactive Excel Dashboard          ✅ Order Funnel Analysis
✅ 4-Page Power BI Dashboard            ✅ BPMN AS-IS / TO-BE Diagrams
✅ Functional Requirements Spec (FRS)  ✅ UAT Test Cases with Sign-Off Sheet
✅ Use Case Diagram                     ✅ Advanced Excel (XLOOKUP, VBA, Arrays)
```

---

## 🔍 Business Problem

Quantitative analysis of 110,817 orders identified **4 critical operational gaps**:

| # | Pain Point | Data Evidence |
|---|---|---|
| ⚠️ 1 | No automated customer communication at any order stage | 0 automated notifications in AS-IS process |
| ⚠️ 2 | No seller SLA monitoring — delays go untracked | Average delivery time exceeds industry benchmark |
| ⚠️ 3 | 8.8% order review gap — no post-delivery prompting | 96,470 delivered vs 88,000 reviewed orders |
| ⚠️ 4 | Manual status updates cause customer information lag | Status delay confirmed in Power BI dashboard |

---

## 🗂️ Project Structure

```
BA_Ecommerce_Project/
│
├── 📁 01_Raw_Data/                        ← 9 original Olist CSV files (never modified)
│
├── 📁 02_Excel/
│   └── BA_Project_Main.xlsm               ← Power Query ETL + Star Schema + Dashboard + VBA
│
├── 📁 03_Python/
│   ├── BA_Ecommerce_Analysis.ipynb        ← Full analysis notebook (RFM, Cohort, Funnel)
│   ├── rfm_results.csv                    ← RFM segmentation export → imported into Power BI
│   ├── cohort_results.csv                 ← Cohort retention matrix export
│   ├── funnel_results.csv                 ← Funnel analysis export
│   └── *.png                              ← 4 exported chart images
│
├── 📁 04_PowerBI/
│   └── BA_Ecommerce_Dashboard.pbix        ← 4-page interactive Power BI dashboard
│
├── 📁 05_BA_Documents/
│   ├── FRS_OrderManagement.docx           ← Functional Requirements Spec (10 FRs, 7 NFRs)
│   └── UAT_TestCases_OrderManagement.docx ← 8 UAT test cases + formal sign-off sheet
│
├── 📁 06_Diagrams/
│   ├── BPMN_ASIS_Order_Management.drawio  ← Current process with annotated pain points
│   ├── BPMN_TOBE_Order_Management.drawio  ← Proposed enhanced automated process
│   └── UseCase_OrderManagement.drawio     ← 21 use cases, 5 actors, include/extend relations
│
└── README.md
```

---

## 📊 Phase 2 — Excel Analysis

### Power Query ETL Pipeline
8 connected queries built with **non-destructive transformation** — raw source files untouched throughout.

- Locale-aware date parsing fixing Brazilian Portuguese date format errors
- Left Outer Joins merging English category names onto product data
- Null removal from critical delivery and approval date columns
- Column pruning, data type enforcement, and text standardisation

### Data Model — Star Schema

```
              Customers
                  │
Reviews ── Orders ──── OrderItems ──── ProductsEnglish
                  │
              Payments
```

**Orders** = central fact table · All others = dimension tables · 5 relationships defined

### Dashboard Features

| Feature | Detail |
|---|---|
| **KPI Cards** | Total Revenue · Total Orders · Avg Order Value · Avg Review Score · Avg Delivery Days |
| **Charts** | Monthly revenue line · Top 10 categories bar · Payment method donut |
| **Interactivity** | Slicers with cross-filtering — all visuals update simultaneously |
| **Advanced Formulas** | XLOOKUP · INDEX MATCH · SUMIFS · Dynamic Arrays (SORT, UNIQUE, TAKE, SORTBY) |
| **Conditional Formatting** | Heatmaps · Data bars · Traffic light icon sets · Exception threshold highlighting |
| **VBA Macros** | `RefreshDashboard()` with status bar feedback · `ExportDashboardPDF()` with date-stamped filename |

---

## 🐍 Phase 3 — Python Analysis

> Full notebook: `03_Python/BA_Ecommerce_Analysis.ipynb`

### Libraries
```python
pandas     # Data loading, cleaning, transformation, aggregation
numpy      # Numerical operations
matplotlib # Chart generation and styling
seaborn    # Statistical visualisation (cohort heatmap)
```

### Analysis 1 — RFM Customer Segmentation

Each customer scored **1–5** on three dimensions using quintile scoring (`pd.qcut`):

| Dimension | Score 5 | Score 1 |
|---|---|---|
| **Recency** | Bought very recently | Has not bought in a long time |
| **Frequency** | Buys very often | Rarely buys |
| **Monetary** | Highest total spend | Lowest total spend |

**7 segments identified with targeted business strategies:**

| Segment | Definition | Recommended Action |
|---|---|---|
| 🏆 Champions | High R + High F + High M | Reward · Request referrals |
| 💛 Loyal Customers | Consistently strong scores | Loyalty programme |
| 🆕 New Customers | High R, Low F | Onboarding · Second-purchase incentive |
| ⚠️ At Risk | Low R, previously frequent | Immediate re-engagement campaign |
| ❌ Lost Customers | Low on all three | Low-cost win-back only |
| 💎 High Spenders | High M, Low F | Targeted premium offers |
| 🌱 Potential Loyalists | Middle scores | Next-purchase discount |

### Analysis 2 — Cohort Retention Analysis

Tracked month-on-month retention for every customer cohort from first purchase month. Visualised as a heatmap — Month 0 = 100%, subsequent months show return rate.

**Key finding:** Sharp drop after Month 0 → heavy reliance on new customer acquisition. Retention programme recommended.

### Analysis 3 — Order Funnel Analysis

| Stage | Orders | vs Start |
|---|---:|---:|
| Orders Placed | ~100,000 | 100.0% |
| Orders Approved | ~99,441 | 99.4% |
| Orders Shipped | ~97,600 | 97.6% |
| Orders Delivered | ~96,470 | 96.5% |
| Orders Reviewed | ~88,000 | **88.0%** |

> 🔴 **Biggest drop: Delivered → Reviewed (8.8%)** — addressed by FR-004 in the FRS

---

## 📊 Phase 4 — Power BI Dashboard

### 4-Page Interactive Dashboard

| Page | Business Purpose | Key Visuals |
|---|---|---|
| **Sales Overview** | Executive performance summary | 5 KPI cards · Revenue trend · Top 10 categories · Payment donut · Year slicer |
| **Customer Segmentation** | Customer targeting strategy | RFM segment donut · Revenue by segment · Scatter plot (R × M, sized by F) |
| **Cohort & Funnel** | Retention and process efficiency | Retention heatmap matrix · Order funnel with drop-off chart |
| **Operations** | Delivery and quality monitoring | Delivery histogram · State map · Review score by category |

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

> **Python → Power BI workflow:** RFM and cohort results calculated in Python, exported as CSV, imported into Power BI. Each tool doing what it does best.

---

## 📋 Phase 5 — BA Documents

### BPMN Process Maps (draw.io)

**AS-IS** — 4 swim lanes with 5 data-evidenced pain point annotations.
**TO-BE** — Same structure with proposed automated enhancements (teal):

```
✅ FR-001 · Auto confirmation SMS + email within 5 minutes
✅ FR-002 · Real-time status notifications at every order stage
✅ FR-003 · SLA timer — 24hr warning + 48hr breach escalation
✅ FR-004 · Automated review request 24hrs post-delivery
```

### Use Case Diagram
5 actors · 21 use cases · 6 × «include» · 4 × «extend» relationships

### Functional Requirements Specification

| ID | Requirement | Priority |
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
| Revenue | Total gross revenue | R$ 16,008,872 |
| Revenue | Average order value | R$ 154.10 |
| Revenue | Top performing category | Health & Beauty |
| Revenue | Top payment method | Credit Card |
| Operations | Average delivery time | ~12 days |
| Operations | Review submission rate | 91.2% — 8.8% gap |
| Customers | Average review score | 4.09 / 5.0 |
| Customers | Unique customers | ~99,000 |
| Process | Biggest funnel drop | Delivered → Reviewed (8.8%) |

---

## 💼 Skills Demonstrated

<details>
<summary><b>📊 Data Engineering & Excel</b></summary>
<br/>

- ETL pipeline using Power Query (M language) — non-destructive, connection-only queries
- Star schema data modelling with 5 table relationships in Excel Data Model
- Locale-aware date parsing (Portuguese Brazil format)
- Left Outer Joins and data denormalisation
- XLOOKUP, INDEX MATCH, SUMIFS with structured table references
- Dynamic arrays: SORT, UNIQUE, TAKE, SORTBY
- Conditional formatting: heatmaps, data bars, traffic lights, exception highlighting
- VBA macros: RefreshDashboard() and ExportDashboardPDF()

</details>

<details>
<summary><b>🐍 Python & Data Analysis</b></summary>
<br/>

- RFM segmentation using pd.qcut quintile scoring
- Cohort retention: cohort assignment, months_since_first, pivot_table matrix
- Funnel analysis with shift(1) for conversion rates
- Time series analysis with groupby and period conversion
- groupby().agg() with named aggregation
- DataFrame merging, boolean filtering, feature engineering
- matplotlib subplots, fill_between, seaborn heatmap

</details>

<details>
<summary><b>📊 Power BI & DAX</b></summary>
<br/>

- DAX: SUM, DISTINCTCOUNT, DIVIDE, AVERAGE, COUNTROWS(FILTER)
- Cross-filtering slicers with automatic bidirectional updates
- Conditional formatting heatmap via Matrix visual
- Python → Power BI integration via CSV export
- 4-page professional dashboard design

</details>

<details>
<summary><b>📋 Business Analysis</b></summary>
<br/>

- AS-IS / TO-BE BPMN process mapping with data-evidenced pain point annotations
- Use Case diagram with include/extend notation
- Functional requirements with MoSCoW prioritisation and acceptance criteria
- 7 non-functional requirements categories
- Scope definition with explicit exclusions
- UAT test cases with formal sign-off sheet
- Stakeholder register and assumption/dependency analysis

</details>

---

## 🚀 How to Run

### Prerequisites
```
Python 3.x (Anaconda)  ·  Excel Office 365  ·  Power BI Desktop (free)
VS Code + Jupyter extension  ·  draw.io at app.diagrams.net (free)
```

### 1 — Get the Dataset
```
Visit: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
Download and unzip all 9 CSV files → place in 01_Raw_Data/
```

### 2 — Python Analysis
```python
# Open 03_Python/BA_Ecommerce_Analysis.ipynb in VS Code
# Select Anaconda base kernel
# Update data_path to your local 01_Raw_Data path
# Run → Run All Cells
```

### 3 — Excel Dashboard
```
Open 02_Excel/BA_Project_Main.xlsm → Enable Content → Dashboard sheet → Refresh
```

### 4 — Power BI Dashboard
```
Open 04_PowerBI/BA_Ecommerce_Dashboard.pbix → Refresh → navigate 4 pages
```

### 5 — Diagrams
```
app.diagrams.net → File → Open from Device → select .drawio file from 06_Diagrams/
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
