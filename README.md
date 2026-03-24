# 🛒 E-Commerce Business Process Optimization
### Business Analyst Portfolio Project — Sri Lankan Retail Context

![Excel](https://img.shields.io/badge/Excel-Power%20Query%20%7C%20VBA%20%7C%20Dashboard-217346?style=flat&logo=microsoft-excel&logoColor=white)
![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20Seaborn%20%7C%20Matplotlib-3776AB?style=flat&logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-DAX%20%7C%20Star%20Schema%20%7C%20Dashboard-F2C811?style=flat&logo=powerbi&logoColor=black)
![draw.io](https://img.shields.io/badge/draw.io-BPMN%20%7C%20Use%20Case-F08705?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-44BBA4?style=flat)

---

## 📌 Project Overview

This end-to-end Business Analyst portfolio project simulates a real-world e-commerce process improvement engagement relevant to Sri Lankan retail businesses such as **Daraz**, **Keells Online**, and **Cargills Food City**. Using a real 100,000+ order dataset, the project delivers the full suite of BA deliverables — from raw data cleaning through to formal requirements documentation.

The project was built to directly match the skill requirements of BA and data analyst roles at companies including **Sysco Lanka**, **PAYable**, **Vision Tech**, and **Glitz Park**.

---

## 🎯 Business Problem Statement

Analysis of 110,817 e-commerce orders (2016–2018) identified four critical operational gaps:

| # | Pain Point | Evidence |
|---|---|---|
| 1 | No automated customer communication at any order stage | Zero automated notifications found in AS-IS process |
| 2 | No seller SLA monitoring — sellers can delay indefinitely | Delivery time variance identified in data analysis |
| 3 | 8.8% of delivered orders receive no customer review | Funnel: 96,470 delivered vs 88,000 reviewed |
| 4 | Manual order status updates causing information lag | Status update gap visible in Power BI dashboard |

---

## 📁 Repository Structure

```
BA_Ecommerce_Project/
│
├── 01_Raw_Data/
│   ├── olist_orders_dataset.csv
│   ├── olist_order_items_dataset.csv
│   ├── olist_customers_dataset.csv
│   ├── olist_order_payments_dataset.csv
│   ├── olist_products_dataset.csv
│   ├── olist_sellers_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_geolocation_dataset.csv
│   └── product_category_name_translation.csv
│
├── 02_Excel/
│   └── BA_Project_Main.xlsm            ← Power Query + Dashboard + VBA
│
├── 03_Python/
│   ├── BA_Ecommerce_Analysis.ipynb     ← Full analysis notebook
│   ├── rfm_results.csv                 ← RFM segmentation output
│   ├── cohort_results.csv              ← Cohort retention matrix output
│   ├── funnel_results.csv              ← Funnel analysis output
│   ├── monthly_revenue.png
│   ├── rfm_segmentation.png
│   ├── cohort_analysis.png
│   └── funnel_analysis.png
│
├── 04_PowerBI/
│   └── BA_Ecommerce_Dashboard.pbix     ← 4-page interactive dashboard
│
├── 05_BA_Documents/
│   ├── FRS_OrderManagement.docx        ← Functional Requirements Spec
│   └── UAT_TestCases_OrderManagement.docx
│
├── 06_Diagrams/
│   ├── BPMN_ASIS_Order_Management.drawio
│   ├── BPMN_TOBE_Order_Management.drawio
│   └── UseCase_OrderManagement.drawio
│
└── README.md
```

---

## 🗂️ Dataset

**Source:** [Olist Brazilian E-Commerce Dataset — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

| File | Rows | Description |
|---|---|---|
| olist_orders_dataset.csv | 99,441 | Main order ledger with status and timestamps |
| olist_order_items_dataset.csv | 112,650 | Line items — products, prices, freight |
| olist_customers_dataset.csv | 99,441 | Customer location data |
| olist_order_payments_dataset.csv | 103,886 | Payment method and values |
| olist_products_dataset.csv | 32,951 | Product catalogue (Portuguese) |
| olist_order_reviews_dataset.csv | 99,224 | Customer review scores (1–5) |
| product_category_name_translation.csv | 71 | Portuguese to English category names |

> **Master DataFrame after cleaning and joining:** 110,817 rows × 24 columns

---

## 🔧 Phase 2 — Excel Analysis

### Tools Used
- **Power Query** — ETL pipeline (non-destructive data transformation)
- **Data Model** — Star schema with 5 table relationships
- **Pivot Tables** — Business analysis across 5 dimensions
- **Excel Dashboard** — Interactive KPI dashboard with slicers
- **Advanced Formulas** — XLOOKUP, INDEX MATCH, SUMIFS, Dynamic Arrays
- **Conditional Formatting** — Heatmaps, data bars, traffic light icon sets
- **VBA Macros** — Automated dashboard refresh, PDF export

### Data Model — Star Schema

```
Customers ──── Orders ──── OrderItems ──── ProductsEnglish
                  │
               Payments
                  │
               Reviews
```

`Orders` is the central **fact table**. All others are **dimension tables**.

### Key Cleaning Steps

| Step | Action | Reason |
|---|---|---|
| Date conversion | Using Locale → Portuguese (Brazil) | Brazilian date format DD-MM-YY conflicts with default parsing |
| Order filter | Status = delivered only | Exclude cancelled and incomplete orders |
| Null removal | Drop null delivery and approval dates | Incomplete records corrupt time-based calculations |
| State standardisation | UPPERCASE on customer_state | SP vs sp treated as different values without standardisation |
| Column pruning | Reviews: keep order_id and review_score only | Remove data bloat from unused columns |
| Left Outer Join | Products merged with CategoryTranslation | Attach English category names to Portuguese product codes |

### Excel Dashboard KPIs

| KPI | Value |
|---|---|
| Total Revenue | R$ 16,008,872 |
| Total Orders | 96,470 |
| Avg Order Value | R$ 165.93 |
| Avg Review Score | 4.09 / 5.0 |
| Avg Delivery Days | Calculated via Power Query custom column |

---

## 🐍 Phase 3 — Python Analysis

### Setup

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Notebook Structure

| Section | Analysis | Output |
|---|---|---|
| 1 | Setup & Data Loading | Master DataFrame: 110,817 rows |
| 2 | Exploratory Data Analysis | Revenue trends, delivery and review stats |
| 3 | RFM Customer Segmentation | 7 labelled customer segments |
| 4 | Cohort Analysis | Monthly retention heatmap |
| 5 | Funnel Analysis | Stage-by-stage drop-off chart |

### RFM Segmentation

Customers scored 1–5 on Recency, Frequency, and Monetary using quintile scoring (`pd.qcut`):

| Segment | Definition | Business Action |
|---|---|---|
| Champions | High R + High F + High M | Reward — ask for referrals |
| Loyal Customers | Good scores across all 3 dimensions | Loyalty programme |
| New Customers | High R, Low F | Nurture with onboarding campaigns |
| At Risk | Low R, previously frequent | Re-engagement campaign immediately |
| Lost Customers | Low across all 3 dimensions | Low-cost win-back only |
| High Spenders | High M, Low F | Premium targeted offers |
| Potential Loyalists | Mid-range scores | Incentivise next purchase |

### Cohort Retention Analysis

Tracks the percentage of customers from each monthly cohort who return in subsequent months. Month 0 is always 100% (first purchase). Month 1 onwards reveals true retention behaviour. Low month-1 retention signals heavy reliance on new customer acquisition — a costly and unsustainable growth model.

### Funnel Analysis

```
Stage 1 — Orders Placed      : 99,441  (100.0%)
Stage 2 — Orders Approved    : 99,441  ( 99.4%)
Stage 3 — Orders Shipped     : 97,600  ( 98.1%)
Stage 4 — Orders Delivered   : 96,470  ( 98.8%)
Stage 5 — Orders Reviewed    : 88,000  ( 91.2%)
                                          ↑
                               Biggest drop-off — addressed by FR-004
```

---

## 📊 Phase 4 — Power BI Dashboard

### 4-Page Interactive Dashboard

| Page | Key Visuals | Business Question |
|---|---|---|
| Sales Overview | 5 KPI cards, monthly revenue line chart, top 10 categories, payment type donut, year slicer | How is the business performing overall? |
| Customer Segmentation | RFM segment donut, revenue by segment bar, RFM scatter plot (R vs M, sized by F) | Who are our customers and what are they worth? |
| Cohort and Funnel | Retention heatmap matrix, order processing funnel | Are we keeping customers? Where do we lose them? |
| Operations | Delivery time histogram, state map, review scores by category, on-time delivery rate | How efficient are our operations? |

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

### Power BI vs Tableau

Power BI was selected over Tableau because it is part of the Microsoft ecosystem. Sri Lankan enterprises predominantly use Microsoft infrastructure. Power BI integrates directly with Excel, SharePoint, and Teams — making it significantly more relevant to the local job market.

---

## 📐 Phase 5 — BA Documents

### BPMN AS-IS Diagram

Maps the current broken order management process across 4 swim lanes: Customer, Olist Platform, Seller, and Carrier. Five pain point annotations are linked directly to the problem steps using BPMN notation.

### BPMN TO-BE Diagram

Proposes the enhanced process with all new automated steps shown in teal, improvement annotations in green, and an SLA escalation path clearly marked. Every new task is referenced to its corresponding FRS requirement.

### Use Case Diagram

21 use cases inside a system boundary rectangle. 5 actors outside: Customer, Seller, Platform Admin, Notification System (system actor), and Payment Gateway (external actor). Include and extend relationships shown with correct UML notation.

### FRS — Functional Requirements Specification

10 Functional Requirements with MoSCoW prioritisation:

| ID | Requirement | Priority |
|---|---|---|
| FR-001 | Automated order confirmation — SMS and email within 5 minutes | High |
| FR-002 | Real-time status notifications at each lifecycle stage | High |
| FR-003 | Seller SLA monitoring — 24hr warning and 48hr escalation | High |
| FR-004 | Post-delivery automated review request — 24hrs after delivery | Medium |
| FR-005 | Seller performance dashboard — real-time, admin access only | Medium |
| FR-006 | Customer self-service order tracking portal — no login required | High |
| FR-007 | Payment failure notification with plain-language reason and retry link | High |
| FR-008 | Delivery failure automated redelivery scheduling | Medium |
| FR-009 | Customer notification preference management | Low |
| FR-010 | Automated monthly performance report generation | Low |

7 Non-Functional Requirements covering: Performance, Availability (99.9% uptime), Scalability, Security (TLS + AES-256 + RBAC), Usability, Reliability, and Auditability.

### UAT Test Cases

8 test cases — each with objective, pre-conditions, numbered steps, expected result, blank actual result field, Pass/Fail/Blocked status, and a formal 5-signatory sign-off sheet.

---

## 💡 Key Concepts Demonstrated

| Concept | Where Applied |
|---|---|
| ETL (Extract Transform Load) | Power Query non-destructive cleaning pipeline |
| Star Schema and Data Modelling | Excel Data Model and Power BI Model View |
| Primary Key and Foreign Key | 5 table relationships across the data model |
| RFM Segmentation | Python — quantile scoring with pandas |
| Cohort Analysis | Python — retention matrix using pivot_table |
| Funnel Analysis | Python — stage-by-stage conversion with shift(1) |
| DAX Measures | Power BI — context-aware dynamic calculations |
| Cross-Filtering | Power BI — automatic bidirectional visual filtering |
| BPMN Process Mapping | draw.io — AS-IS pain points and TO-BE improvements |
| Requirements Engineering | FRS — MoSCoW prioritisation with acceptance criteria |
| UAT Design | Test cases directly mapped to FRS requirements |
| VBA Automation | Excel — refresh dashboard and PDF export macros |
| Dynamic Array Formulas | Excel — SORT, UNIQUE, TAKE, SORTBY |
| Denormalisation | Merging review_score and category_english into OrderItems |

---

## 🛠️ Tools and Technologies

| Tool | Purpose |
|---|---|
| Microsoft Excel 365 | Power Query ETL, Star Schema Data Model, Dashboard, VBA Macros |
| Python 3.x | Data cleaning, RFM segmentation, cohort and funnel analysis |
| pandas | DataFrame manipulation, groupby, merge, pivot_table |
| matplotlib and seaborn | Charts — line, bar, heatmap, funnel, scatter |
| VS Code + Jupyter | Python development environment |
| Power BI Desktop | 4-page interactive dashboard with DAX measures |
| draw.io | BPMN AS-IS, BPMN TO-BE, Use Case diagram |
| Microsoft Word 365 | FRS and UAT documentation |

---

## 🚀 How to Run

### Excel
1. Open `02_Excel/BA_Project_Main.xlsm`
2. Click **Enable Content** when prompted (required for VBA macros)
3. Go to **Data → Refresh All** to reload all Power Query connections
4. Navigate to the **Dashboard** sheet to view the interactive report

### Python

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn jupyter

# Open the notebook in Jupyter or VS Code
jupyter notebook 03_Python/BA_Ecommerce_Analysis.ipynb

# Update the data_path in Cell 3 to your local raw data folder
data_path = r"C:\your\path\to\01_Raw_Data"

# Run: Kernel → Restart and Run All Cells
```

### Power BI
1. Open `04_PowerBI/BA_Ecommerce_Dashboard.pbix`
2. Go to **Home → Transform Data → Close and Apply** to refresh
3. If prompted, update the data source path: **File → Options → Data Source Settings**

### draw.io Diagrams
1. Go to [app.diagrams.net](https://app.diagrams.net)
2. **File → Open from → Device**
3. Select any `.drawio` file from `06_Diagrams/`

---

## 📈 Key Findings

```
VOLUME
  Total orders analysed       :  110,817
  Successfully delivered      :   96,470  (87.0%)
  Date range                  :  Oct 2016 — Aug 2018

REVENUE
  Total revenue               :  R$ 16,008,872
  Average order value         :  R$ 165.93
  Top performing category     :  Health and Beauty

CUSTOMERS
  Unique customers            :  ~99,000
  Champions segment           :  Top revenue contributors
  At Risk segment             :  Priority re-engagement target

OPERATIONS
  Review submission gap       :  8.8% of delivered orders not reviewed
  Biggest funnel drop-off     :  Delivered to Reviewed stage
  Cohort retention            :  Low month-1 return rate
  Implication                 :  Over-reliance on new customer acquisition

PROPOSED IMPROVEMENTS
  10 functional requirements  :  Target all identified operational gaps
  Review rate target          :  91.2% → 96%
  SLA enforcement             :  Eliminate indefinite seller processing delays
  Customer comms              :  Zero manual steps in notification workflow
```

---

## 📄 Dataset License

The Olist Brazilian E-Commerce Dataset is available on Kaggle under CC BY-NC-SA 4.0.
All analysis, documentation, diagrams, and code in this repository are original work.

---

## 👤 About This Project

Built as a comprehensive Business Analyst portfolio project targeting entry-level and junior BA and data analyst roles in the Sri Lankan job market.

**Target roles:** Business Analyst · Data Analyst · Junior BI Analyst · Process Analyst

**Relevant employers:** Sysco Lanka · PAYable · Vision Tech · Glitz Park · Commercial Bank · Dialog · Hemas

---

> *Built from scratch with zero prior experience. Every concept, tool, and technique was learned and applied from the ground up — which is exactly what this project is designed to prove.*
