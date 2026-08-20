### Business Performance Analytics — Power BI

**1. Project Overview**
Objective: building an interactive BI solution for monitoring financial and operational business performance at the Business → Product → Store → City level.
Business goals

    - monitor Revenue, Profit and Margin;
    - identify profitability drivers and risks;
    - evaluate Product Portfolio performance;
    - identify underperforming cities and stores;
    - support portfolio and operational decisions.
Source: CSV files
Transformation: Power Query
Semantic Model: Power BI / Star Schema
Analytics: DAX
Reporting period: 2022–2023

**2. Solution Architecture**

CSV Sources → Power Query → Data Cleansing & Transformation → Star Schema → Semantic Model → DAX Measures → Report Layer → Business Insights & Decisions

Design principles

    * separation of Fact / Dimension;
    * single source of truth for KPIs;
    * explicit DAX measures;
    * centralized Date dimension;
    * controlled filter propagation;
    * reusable business logic;
    * minimal calculated columns;
    * report layer separated from data/model layer.

**3. Data Model**
Fact - FactSales
Grain: one row = one sales transaction
Main metrics:
    * Revenue
    * Profit
    * Margin
    * Transactions
Dimensions
DimCalendarDax
    * Date
    * Year
    * Quarters
    * Seasons
    * Month
    * Month Number
    * Weekday
DimProducts
    * Product ID
    * Product Category
    * Product Group
    * Price Segment
    * Product Cost
    * Product Price
DimStores
    * Store ID
    * Store Name
    * Store Location
    * Store Open Date 

Relationships
DimCalendarDax  1 ───── * FactSales
DimProducts  1 ───── * FactSales
DimStores     1 ───── * FactSales
Filter direction: Dimension → Fact.

**4. Data Preparation**
CSV data passes through Power Query.
Transformation layer
    * data type standardization;
    * null / blank handling;
    * duplicate validation;
    * text normalization;
    * key validation;
    * dimension preparation;
    * derived business attributes;
    * date preparation.
Principle: business logic required for reusable analysis is implemented in the semantic model, not duplicated across visuals.

**5. KPI Framework**
KPI	Definition
Revenue	Total sales value
Profit	Total profit
Margin %	Profit / Revenue
Transactions	Number of transactions
Revenue YoY %	Revenue growth vs LY
Revenue MoM %	Revenue growth vs previous month
Profit YoY %	Profit growth vs LY
Profit Contribution %	Share of total Profit
Revenue Contribution %	Share of total Revenue
Current snapshot
KPI	Value	YoY
Revenue	$658,194	+12.3%
Profit	$180,445	+8.4%
Margin	27.42%	-1.0%
Transactions	41,830	+26.9%

**6. Report Architecture**
Dashboard built on the principle progressive analysis: Business performance → Portfolio performance → Inventory performance

**7. Business Performance**
Purpose: executive monitoring of overall business performance.
Analytical focus
    * Revenue trend;
    * Profitability;
    * Margin;
    * Transactions;
    * City performance;
    * Store contribution;
    * Category contribution.
Key visuals
    * KPI cards;
    * Smart Insights: a dynamic bar is implemented at the top of the page, which immediately highlights anomalies;
    * Business Health Index is an integral indicator from 0 to 100 points that assesses the overall health of the business in four areas: Profitability (how profitable the business is), Network Stability (how evenly distributed the business is between stores), Portfolio Quality (what part of the profit is formed by products with a higher margin), Inventory Health (how free the stock is from dead stock);
    * Trend by selected metric (revenue, profit, margin, number of transactions);
    * City Profitability & Risk — the matrix that ranks cities by their profit contribution and risks.;
    * Top / Bottom Stores by selected metric;
    * Selected metric by Product Category;
    * Cities Underperformance vs Median Margin — the histogram of deviations from the median margin that clearly indicates problem locations.
   
Key finding
Revenue demonstrates positive YoY growth, while Margin remains under pressure.
Business implication: Revenue growth should be evaluated together with profitability rather than as an isolated KPI.

<img width="1270" height="709" alt="зображення" src="https://github.com/user-attachments/assets/64426a34-7394-4d4f-af69-7f847209fb87" />

**8. Product Performance**
Purpose: evaluate product portfolio contribution, profitability and momentum.
Analytical dimensions
    * Product Group;
    * Product;
    * Category;
    * Price Segment.
Key visuals
    * Portfolio Quality: A measure of the quality of your product portfolio that helps identify profit concentration;
    * Selected metric by Product Group;
    * Product Portfolio Matrix, that divides products into quadrants to help prioritize marketing budgets;
    * Selected metric by Price Segment;
    * Category Performance Momentum is designed to monitor the growth or decline of each product category. It uses a color-coding system to display the share of products in different states: Declining (red), Growing (green), and Stable (yellow);
       * Product Trend Matrix (Drill-down): the detailed table of the product lifecycle. It uses the Growing, Declining, and Stable states to track margin and revenue dynamics in real time. This allows you to identify which products are losing relevance and which are becoming new growth drivers.
    * Top / Bottom Products by selected metric.

Key findings
    * High-margin products generate 65% of Profit.
    * Top 5 products generate 41% of Profit.
    * Art & Crafts is among the leading portfolio contributors.
    * Revenue is concentrated in Low and Middle price segments.
Business implication
Portfolio decisions should be based on Margin + Profit Contribution + Growth, rather than Revenue alone.

<img width="1276" height="709" alt="зображення" src="https://github.com/user-attachments/assets/4ba13355-85db-435b-9ee1-01247ba4c2f5" />

<img width="1259" height="544" alt="зображення" src="https://github.com/user-attachments/assets/52045e30-cc12-4779-bb49-19fd05d09604" />

**9. Inventory**
Purpose: provide operational visibility into inventory performance and identify potential stock-related risks.
Analytical focus
    * inventory distribution;
    * stock availability;
    * product/category performance;
    * store-level inventory;
    * potential overstock / stockout areas.

Key metrics:
    * Inventory Value: total capital tied up in inventory;
    * Units in Stock: physical number of units in stock;
    * Stockout Rate: the most critical metric that shows that more than half of your inventory is currently unavailable to customers;
    * Revenue at Stockout Risk: the amount of revenue a company loses every day due to out-of-stock items.

Key visuals
    * KPI cards;
    * Smart Insights: a dynamic bar is implemented at the top of the page, which immediately highlights anomalies;
    * Selected metric (Inventory Value, Units in Stock, Stockout Rate, Revenue at Stockout Risk) by Product Group: a histogram shows the cost and percentage of shortages;
    * City Stockout Rate: visualization of priorities for replenishment of stocks.
    * Inventory Efficiency Portfolio divides products into 4 business quadrants:
       Strategic Stock (Top Right): Products with high revenue and sufficient supply. This is the basis of your profit.
       Critical Risk (Bottom Right): Items that generate a lot of money but have critically low inventory. This is the #1 priority for the purchasing department.
       Niche (Bottom Left): Items with low sales and low balances that do not require much attention.
       Overstock (Top Left): Items with high balances that are not selling well (frozen funds)
    * Top Revenue at Stockout Risk: a list of specific driver products that need to be purchased immediately;
    * Store Inventory Performance Detail allows to see the status of each item in a specific store.

<img width="1268" height="713" alt="зображення" src="https://github.com/user-attachments/assets/3eaa3304-bc2d-4ac4-8e99-4ba12ca268de" />

**10. Data Quality & Reconciliation**
Checked before publication:
Source → Model
    * record count;
    * Revenue;
    * Profit;
    * transaction count;
    * unique Product;
    * unique Store;
    * unique City.
Model → Report
    * KPI reconciliation;
    * filter context;
    * totals vs detail;
    * YoY / MoM calculations;
    * Top N / Bottom N;
    * drill-down consistency.
Integrity checks
    * orphan keys;
    * duplicates;
    * missing dimensions;
    * invalid dates;
    * unexpected negative values;
    * incorrect data types.

**11. Performance & Maintainability**
To support productivity:
* Star Schema is used;
* dimension tables are separated from transaction data;
* measures are centralized;
* unnecessary calculated columns are minimized;
* high-cardinality fields are not used unnecessarily;
* complex calculations are not duplicated between visuals.
Maintainability
Business logic is placed in:
Power Query
    → transformation logic

Semantic Model
    → relationships / dimensions

DAX
    → calculations / KPIs

Report
    → visualization / interaction
This allows you to change the calculation logic without rebuilding the entire report layer.

**12. Key Business Insights**
1. Revenue grows faster than Profit, indicating potential pressure on profitability.
2. Business has measurable dependency on a limited number of products.
3. High-margin products 
65% of Profit
Margin protection is strategically important for overall profitability.
4. Portfolio Matrix identifies products requiring: Invest → Protect → Grow → Review

**13. Recommendations**
1. Monitor the gap between Revenue growth and Profit growth.
2. Prioritize products with:
High Margin + High Contribution + Positive Growth
3. Monitor concentration of Revenue and Profit among Top N products.
