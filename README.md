# Superstore-PowerBI-Analysis
# End-to-End Superstore Sales & Profitability Analysis

- An end-to-end Data Analysis project analyzing sales performance, customer purchasing patterns, shipping operational metrics, and profitability drivers to deliver actionable business intelligence.
---

## 1. Idea & Objectives
The primary goal is to audit Superstore's retail performance across regions, customer demographics, and product categories to detect the core operational issues pulling overall margins down, specifically evaluating aggressive discounting strategies and unprofitable product lines.

---

## 2. Dataset Overview
- **Dataset:** Sample - Superstore Clean Dataset
- **Records:** ~9,994 retail transactions
- **Timeframe:** 2014 – 2017
- **Key Dimensions:** Order Date, Ship Date, Ship Mode, Customer Segment, Geographic Hierarchy (Region, State, City), Product Hierarchy (Category, Sub-Category, Product Name).
- **Key Metrics:** Sales, Quantity, Discount, Profit, Calculated Margin.
---

## 3. Business Questions Addressed
1. Which year and month generated the highest sales, and what is the overall sales trend over time?
2. Which state generated the highest sales, and which state generated the highest profit?
3. What is the top-selling city within the highest-performing state?
4. Which Category and Sub-Category generate the highest sales and highest profit?
5. What is the top-selling product by revenue (Sales), and what is the most demanded product by volume (Quantity)?
6. Who are the top 5 customers contributing the most revenue to the store?
7. What is the most popular and frequently used shipping mode (Ship Mode)?
8. Which geographic region generates the highest sales?
9. Which products or categories have the highest profit margins (Profit Margin = Profit / Sales)?
10. Which customer segment (Consumer, Corporate, Home Office) contributes the most to total sales and profit?
11. How do discounts impact profitability, and does offering higher discounts increase profits or lead to net losses?
12. Which products or sub-categories generate net negative profit (losses) and require pricing/strategy reviews?
13. What is the average shipping duration (Order Date to Ship Date) across different ship modes?
---

## 4. Data Exploration (EDA)
- Evaluated statistical distributions, quartiles, and variances of `Sales`, `Quantity`, and `Discount`.
- Assessed correlation between `Discount` brackets and `Profit` margins.
- Verified cardinality and frequency counts across categorical dimensions (`Region`, `Segment`, `Category`).
---

## 5. Data Cleaning & Preprocessing
- **Type Casting:** Converted `Order Date` and `Ship Date` into datetime formats.
- **Integrity Validation:** Checked for null values, trailing spaces, and duplicate records across `Order ID` and `Row ID`.
- **Calculated Columns:** Derived shipping duration via `DATEDIFF(Order Date, Ship Date, DAY)` and engineered binned `Discount Bracket` tiers (`0%`, `1%-10%`, `11%-20%`, `21%-30%`, `31%-50%`, `>50%`).
---

## 6. Data Analysis & Core DAX Measures
Custom DAX measures engineered for the dynamic data model:
- `Total Sales = SUM('Sample - Superstore clean NTI'[Sales])`
- `Total Profit = SUM('Sample - Superstore clean NTI'[Profit])`
- `Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)`
- `Total Customers = DISTINCTCOUNT('Sample - Superstore clean NTI'[Customer ID])`
- `Avg Shipping Days = AVERAGEX('Sample - Superstore clean NTI', DATEDIFF('Sample - Superstore clean NTI'[Order Date], 'Sample - Superstore clean NTI'[Ship Date], DAY))`
- `Avg Discount = AVERAGE('Sample - Superstore clean NTI'[Discount])`
---

## 7. Data Visualization (Power BI Dashboard)
The dashboard is structured into an executive 3-page interactive layout with unified custom color palettes, conditional formatting, and synchronized slicers:
1. **Executive Overview:** High-level KPI cards, sales by category, segment breakdown, state distribution map, top California cities, and shipping duration metrics.
2. **Customer & Regional Analysis:** Multi-year line trends, dual-axis state performance benchmarks, regional sales breakdown, and top-tier customer rankings.
3. **Pricing & Profitability Analysis:** Sub-category profit and loss highlighting, discount bracket vs. profit erosion curves, and product-level scatter profitability matrices.
---

## 8. Key Insights & Strategic Conclusions
- **The Discount Trap:** Profitability remains solid up to **20% discount**. Any discount bracket exceeding **20%** triggers severe negative profitability, with discounts over **50%** resulting in heavy net capital erosion.
- **Loss-Making Lines:** Three sub-categories generate structural net losses: **Tables (-$8.6K)**, **Bookcases (-$4.7K)**, and **Machines (-$1.6K)**, largely due to unmanaged high-discount promotions.
- **Geographic Disparities:** While **California** and **New York** drive the vast majority of company profits, major markets like **Texas** (-$10.8K) and **Ohio** (-$2.5K) show substantial net losses despite strong top-line sales.
- **Customer Concentration:** The **Consumer** segment represents **53.4%** of gross sales, while **Corporate** accounts provide the most resilient margins.
- **Actionable Recommendation:** Implement strict discount caps at 20% across Furniture and Office Machine lines, renegotiate supplier pricing for Tables, and audit shipping pricing tiers in Central and Southern states.
