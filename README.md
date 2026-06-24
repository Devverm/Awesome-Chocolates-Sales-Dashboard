# 🍫 Awesome Chocolates Sales Dashboard

An interactive Power BI dashboard built to analyze sales, profitability, and shipment performance across products, regions, and sales teams for the fictional "Awesome Chocolates" company.

Originally created as an entry for the **Chandoo.org Power BI Dashboard Contest (2024)**, with an expanded version adding a full multi-page KPI dashboard and drill-through detail pages.

---

## 📌 Problem Statement

Awesome Chocolates' leadership has sales, profit, and shipment data scattered across products, regions, and sales reps but no single view to answer basic operational questions:

- Which **products** and **categories** are actually driving profit, vs. just volume?
- Which **regions** are underperforming, and is that a regional issue or a product mix issue?
- Which **sales reps and teams** are top performers, and how consistent is that month over month?
- Are there **shipments with abnormally low box counts or low/negative profit** worth flagging?
- How is performance **trending** over time, and is growth/decline accelerating or just noisy?

This dashboard consolidates raw shipment-level data into a single decision-support tool that lets a manager filter, drill down, and switch metrics dynamically — without needing a new report built for every question.

---

## 🎯 Objective

Build a Power BI solution that:
1. Cleans and models raw shipment data into a proper star schema
2. Surfaces trend, regional, and category-level performance through interactive visuals
3. Lets users dynamically switch between metrics (Sales / Profit / Boxes) and scenarios (all shipments vs. low-box shipments) without duplicating visuals
4. Highlights top/bottom performers (products, regions, sales reps) at a glance

---

## 🗂️ Project Versions

| File | Description |
|---|---|
| `AC_Sales_Dashboard_joão_s.pbix` | Original contest entry — Read Me page + a single interactive Product Overview page centered on a quadrant/cluster scatter analysis |
| `AC_Sales_Dashboard_wren_p.pbix` | Expanded build — full multi-page KPI dashboard with dedicated regional, category, and leaderboard pages |

---

## 🧱 Data Model

**Fact table**
- `shipments` — Date, Product, Sales, Profit, COGS, Boxes, Profit %, High/Low classification

**Dimension tables**
- `calendar` — Date hierarchy (Year, Month, Week), Year-Month
- `products` — Product, Category
- `locations` — Geo, Region
- `people` — Sales person, Team

**Disconnected / parameter tables** (power the dynamic switching across visuals)
- `tbl_Scenario`, `tbl_Low_Box` — toggle between all shipments and low-box shipments
- `tbl_Quadrant`, `tbl_Clusters` — drive quadrant/cluster highlighting on the performance scatter chart
- `prm_X_Axis`, `prm_Y_Axis`, `prm_Locations`, `prm_Products`, `prm_Timeline`, `prm_Trend` — field parameters that switch the metric, hierarchy level, and trend view shown across visuals, so one visual can answer multiple questions instead of building a duplicate for each metric

**Key DAX measures**
- Total Sales, Total Profit, Profit %, Total Boxes
- MoM Sales / Profit / Boxes Growth %
- PM (prior month) Sales / Profit / Boxes / COGS — used as the comparison baseline for growth measures
- Dynamic axis/title measures that re-label charts based on the active parameter selection

---

## 📊 Report Pages

### `joão_s` — Original Entry
1. **Read Me** — methodology, features, parameters, and measures documentation
2. **Awesome Chocolates Dashboard** — Product Overview page:
   - Trend line with moving average overlay (smooths variance to surface real trend direction)
   - Scatter chart with quadrant/cluster highlighting — the centerpiece visual for grouping products/categories by performance
   - Performance breakdown table
   - Regional bar/column charts
   - Slicers for category, product, location, and timeline

### `wren_p` — Expanded Build
1. **Dashboard** — main KPI view (Total Sales/Profit/Boxes/Profit % cards, MoM growth indicators, trend lines, category/region breakdowns, top-performer tables)
2. **Geo_Sales / Geo_Profit / Geo_Shipment** — regional breakdown, one page per metric
3. **Category_Sales / Category_profit / Category_shipments** — category breakdown, one page per metric
4. **Top 5 Products** — ranked leaderboard table
5. **Top 5 Sales Person** / **Top 5 Sales Person %** — sales rep leaderboards (absolute and % contribution)
6. **Readme** — in-report documentation page

---

## 💡 Key Insights the Dashboard Surfaces

> These are the analytical findings the dashboard is built to reveal — explore the live filters/parameters in the `.pbix` file to see the current numbers, since they update with the underlying data.

- **Performance is not evenly distributed across products or categories.** The quadrant/cluster scatter chart on the Product Overview page exists specifically to separate "high sales, low profit" products from "low sales, high profit" ones — a distinction a simple bar chart hides.
- **Regional performance often reflects product mix, not just regional demand.** The Geo pages are designed to be cross-filtered by category/product to test whether a weak region is underperforming overall or just weak in specific product lines.
- **Month-over-month growth is volatile at the shipment level**, which is why the dashboard pairs raw trend lines with a moving average — to separate genuine momentum from noise.
- **A subset of shipments have unusually low box counts**, which is why a dedicated low-box scenario toggle (`tbl_Low_Box`) exists — these shipments can otherwise skew average profit-per-box calculations.
- **Sales rep performance leaderboards (Top 5 Sales Person / Top 5 Sales Person %)** make it possible to distinguish reps who sell high *volume* from reps who sell high *value* — the two leaderboards intentionally answer different questions.

---

## 🧹 Methodology Notes

- Transactions with zero sales revenue or zero boxes shipped were removed, treated as data entry errors.
- Extreme values were intentionally **kept** rather than filtered out, since high variance is treated as a genuine characteristic of the underlying data rather than noise to suppress.
- The scatter chart + breakdown table is the analytical core of the report — quadrant/cluster highlighting groups products and categories by performance under whichever scenario is currently selected.

---

## 🛠️ Tools & Techniques

- **Power BI Desktop** — data modeling, report design
- **DAX** — calculated measures, dynamic parameter-driven metrics, MoM/PM growth calculations
- **Power Query (M)** — data cleaning, removal of zero-value transactions
- **Field Parameters & Disconnected Tables** — dynamic metric/axis switching without duplicating visuals

---

## 🚀 How to Use

1. Open either `.pbix` file in **Power BI Desktop** (May 2024 or later recommended for full custom-visual compatibility).
2. Use the slicers (Category, Product, Location, Timeline) and field parameters to switch metrics and drill into specific products, regions, or sales reps.
3. On the `wren_p` version, use the action buttons / bookmarks on the **Dashboard** page to navigate between KPI views.

---

## 📁 Repository Structure
```
├── AC_Product_Review.pbix     # Original contest entry
├── AC_Sales.pbix     # Expanded multi-page version
└── README.md
```
