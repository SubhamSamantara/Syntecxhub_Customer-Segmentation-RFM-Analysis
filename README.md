# Customer Segmentation using RFM Analysis — AdventureWorks

A full RFM (Recency, Frequency, Monetary) customer segmentation built on the AdventureWorks Internet Sales dataset, with a ready-to-use Power BI / Excel dashboard and supporting data files.

## 📊 Overview

This project segments **18,484 customers** into **11 behavioral segments** based on their purchase history, using 60,398 Internet sales order lines spanning **July 2005 – July 2008**. Each customer is scored 1–5 on Recency, Frequency, and Monetary value (by quintile), combined into a 3-digit RFM code, and mapped to a segment using a 128-combination RFM Score → Segment lookup table.

**Reference date for Recency:** 2008-08-01 (one day after the last order in the dataset).

## 🔑 Key Findings

| Segment | % of Customers | % of Revenue |
|---|---|---|
| Champions | 10.3% | **29.9%** |
| At Risk | 15.1% | **28.9%** |
| Loyal | 8.5% | 19.6% |
| Cannot Lose Them | 5.1% | 8.8% |
| Potential Loyalist | 15.5% | 2.4% |
| Hibernating customers | 13.2% | 1.5% |

**Takeaway:** Revenue is split almost evenly between two very different groups — **Champions** (actively buying, high value) and **At Risk** (high historical value, gone quiet). Win-back campaigns for At Risk customers are just as high-priority as loyalty rewards for Champions; nearly 30 cents of every revenue dollar sits with customers who haven't ordered recently.

## 📁 Files in this Repository

| File | Description |
|---|---|
| `AW_RFM_Dashboard.xlsx` | Fully working dashboard — open and use directly in Excel |
| `AW_RFM_Customer_Segments.csv` | Main table: 18,484 customers with Recency, Frequency, Monetary, R/F/M scores, Segment, and demographics (country, income, occupation, gender) |
| `AW_Transactions.csv` | Cleaned FactInternetSales (60,398 order lines) — use for time-series/trend visuals |
| `AW_Segment_Summary_Full.csv` | One row per segment: customer count, avg RFM, revenue share, description, and recommended marketing action |
| `AW_Power_BI_Dashboard_Guide.md` | Step-by-step guide to rebuild this as a Power BI (or Tableau) dashboard |

## 🧮 Methodology

- **Recency** = days since last order (relative to 2008-08-01)
- **Frequency** = distinct `SalesOrderNumber`s per customer
- **Monetary** = total `SalesAmount` per customer
- Each metric scored 1–5 by quintile, combined into a 3-digit RFM code (e.g. `555`, `111`)
- Every code mapped to one of 11 segments via the official RFM lookup table — all 128 combinations matched with zero gaps

## 🗂️ Segments

Champions, Loyal, Potential Loyalist, Promising, New Customers, About To Sleep, Hibernating Customers, Need Attention, At Risk, Cannot Lose Them, Lost Customers — each with a description and a suggested marketing action (see `AW_Segment_Summary_Full.csv`).

## 🛠️ Rebuilding the Dashboard

### Power BI
1. **Get Data → Text/CSV** → import all three CSV files
2. Set `CustomerKey` as Whole Number, "Do not summarize"
3. Relate `AW_Transactions[CustomerKey]` → `AW_RFM_Customer_Segments[CustomerKey]` (many-to-one)
4. Relate `AW_RFM_Customer_Segments[Segment]` → `AW_Segment_Summary_Full[Segment]` (many-to-one)
5. Sort `Segment` by `SegmentOrder` for consistent Champions → Lost ordering

Recommended visuals, DAX measures, and full setup steps are in `AW_Power_BI_Dashboard_Guide.md`.

### Tableau
Import `AW_RFM_Customer_Segments.csv` + `AW_Transactions.csv`, join on `CustomerKey`, and build equivalent worksheets combined into a dashboard with a Segment filter action.

## 🧰 Tech / Data Source

- **Source:** AdventureWorksDW — `FactInternetSales`, `DimCustomer`, `DimGeography`
- **Tools:** Excel, Power BI (or Tableau)
- **Techniques:** RFM analysis, quintile scoring, segment lookup mapping, DAX

## 📌 Suggested Repo Structure

```
├── AW_RFM_Dashboard.xlsx
├── AW_RFM_Customer_Segments.csv
├── AW_Transactions.csv
├── AW_Segment_Summary_Full.csv
├── AW_Power_BI_Dashboard_Guide.md
└── README.md
```

## 📄 License

Add a license of your choice (e.g. MIT) if this repo is public.
