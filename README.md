# Chocolate Sales Analysis — Power BI Report

An interactive Power BI dashboard analyzing chocolate sales across customers, products, brands, and geography. Built on a star-schema data model with a custom Calendar dimension, DAX measures for sales and trend analysis, and five report pages covering demographics, sales trends, product/brand performance, and city/region-level insights.

## 🖼️ Screenshots

**Dashboard**
![Dashboard](screenshots/Dashboard.png)

**Customer Demographics Analysis**
![Customer Demographics Analysis](screenshots/Customer_Demographics_Analysis.png)

**Sales Trend Analysis**
![Sales Trend Analysis](screenshots/Sales_Trend_Analysis.png)

**Brand & Product Analysis**
![Brand and Product Analysis](screenshots/Brand_and_Product_Analysis.png)

**Geospatial Analysis**
![Geospatial Analysis](screenshots/Geospatial_Analysis.png)

## 📊 Report Overview

The report is organized into 5 visible pages plus 1 hidden tooltip page:

| Page | Contents |
|---|---|
| **Dashboard** | KPI cards (Total Sales, Total Quantity Sold), Top Brand & Top City cards, Sales by Gender (donut), Sales by Month (area chart), Sales by Chocolate Type & by Brand (column charts), city-level map, Brand/City slicers |
| **Customer Demographics** | Loyalty status funnel, Gender donut, Age Segment breakdown, Top 5 customers by festival-season sales, Top 5 customers by total sales |
| **Sales_Trends** | Monthly sales trend by Brand, monthly sales trend by Loyalty Status, sales by Quarter, sales by Weekday |
| **Product & Brand Analysis** | Sales by Chocolate Type, sales by Brand, Cost Segment donut, Top 5 chocolates treemap, month-over-month % change in sales |
| **Geospatial Analysis** | Sales by City and by Origin Region, shown on maps |
| **Tooltip_ Brand** *(hidden)* | Custom tooltip table (Brand + Total Sales) shown on hover in other visuals |

## 🗂️ Data Model

Built as a star schema for clean relationships and efficient DAX evaluation:

- **Fact table:** `chocolate_sales_fact_table`
- **Dimension tables:**
  - `Calendar_Dimension` — Date, Day, Day Number, Month, Month Number, Quarter, Year
  - `customer_dimension` — Customer_Name, Age, Age_segment, Gender, Loyalty_Status, Location
  - `product_dimension` — Chocolate_Name, Chocolate_Type, Brand, Cost_segment
  - `location_dimension` — City, Origin_Region

`Calendar_Dimension` is generated via `CALENDAR()` spanning the full range of transaction dates, with a numeric `Month Number` column set as the **sort-by-column** for `Month`, ensuring charts render in true chronological (Jan → Dec) order rather than alphabetical order.

## 📐 Key Measures

| Measure | Purpose |
|---|---|
| `Total Sales` | Core revenue measure used across all pages |
| `Quantity_Sold` | Units sold |
| `Change_in_sales` | Period-over-period % change in sales |
| `Festival_season_sales` | Sales isolated to festival-season periods |

## ✅ Notes on Data Quality / Fixes Applied

- **Month sort order:** Line and area charts were originally sorting by measure value (or alphabetically) instead of calendar order. This was fixed by setting `Month`'s Sort-by-Column to `Month Number` at the model level and explicitly re-applying the axis sort on affected visuals.
- **Category coloring:** The Gender donut chart initially rendered a color gradient/shading instead of two flat colors. Fixed by switching the relevant color format style from **Rules**/**Gradient** to **Categorical** and assigning solid colors per Male/Female series.

## 🛠️ Built With

- **Power BI Desktop**
- **DAX** for calculated columns and measures
- **Power Query (M)** for data shaping and the Calendar dimension

## 📁 Files

- `Chocolate_Analysis_Report.pbix` — the full Power BI report
- `screenshots/` — page-by-page preview images used in this README

## 🚀 Getting Started

1. Clone this repository.
2. Open `Chocolate_Analysis_Report.pbix` in **Power BI Desktop** (2023 or later recommended).
3. If prompted, refresh data sources under **Home → Refresh**.
4. Use the Brand/City slicers on the Dashboard page to filter the report interactively.

## 📌 Possible Future Enhancements

- Add a Year/Quarter slicer synced across all pages for consistent time filtering
- Add row-level security (RLS) if this report is shared across regional teams
- Build a forecast visual on the Sales_Trends page using the built-in analytics pane
