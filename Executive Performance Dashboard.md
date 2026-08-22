## 1. Project Overview

**Objective:** building an interactive BI solution for top management to monitor financial performance, analyze profitability, and identify key factors affecting the company’s financial results, with drill-down from high-level KPIs to transaction-level details.

### Business goals

- monitor key financial KPIs and overall business performance;
- analyze Revenue, Profit, and Margin;
- identify key profitability drivers and financial risks;
- evaluate performance across business dimensions;
- identify underperforming areas and potential improvement opportunities;
- drill down from aggregated results to individual transactions for detailed audit;
- support data-driven financial and operational decisions.

Source: structured transactional data  
Transformation: Power Query  
Semantic Model: Power BI / Star Schema  
Analytics: DAX  
Reporting period: 2014–2017   

## 2. Solution Architecture

Structured transactional data → Power Query → Data Cleansing & Transformation → Star Schema → Semantic Model → DAX Measures → Report Layer → Business Insights & Decisions

### Design principles

- separation of Fact / Dimension;
- single source of truth for KPIs;
- explicit DAX measures;
- centralized Date dimension;
- controlled filter propagation;
- reusable business logic;
- minimal calculated columns;
- report layer separated from data/model layer.    

## 3. Data Model

**Fact - FactSales**  
Grain: one row = one sales transaction  
Main metrics:
- Revenue
- Profit
- Margin
- Transactions

**Dimensions**

**DimCalendarDax**
- Date
- Year
- Quarters
- Month
- Month Name
- Weekday

**DimProduct**
- Product ID
- Category
- Sub-Category
- Product Segment
- Product Name

**DimCustomer**
- Customer ID
- Customer Name
- Segment

**DimAddress**
- City
- Country
- Postal Code
- Region
- State

**Relationships**
- DimCalendarDax 1 ───── * FactSales
- DimProduct 1 ───── * FactSales
- DimCustomer 1 ───── * FactSales
- DimAddress 1 ───── * FactSales

Filter direction: Dimension → Fact.   

## 4. Data Preparation

CSV data passes through Power Query.

**Transformation layer:**
- data type standardization;
- null / blank handling;
- duplicate validation;
- text normalization;
- key validation;
- dimension preparation;
- derived business attributes;
- date preparation.

**Principle:** business logic required for reusable analysis is implemented in the semantic model, not duplicated across visuals.


## 5. The **Executive Summary** page is a central dashboard that provides a strategic overview of the state of the business and allows you to instantly assess KPIs:

**Key visuals:**

1. Key Performance Indicators (KPI) Dashboard and Interactivity. KPI values ​​are shown as of the latest date from the available data set.
The page presents four main metrics:
    - Total Revenue: $2,30M (-29,2%).
    - Gross Profit: $286K (+4,5%).
    - Margin, %: 12,5% (+62,4%).
    - Active Customer Base: 793 (+58,8%).

<img width="1265" height="705" alt="зображення" src="https://github.com/user-attachments/assets/e80574a7-cf44-4536-b1a7-56fb410f721c" />

When you click on any KPI card, all graphs on the page are automatically reorganized, displaying data specifically for the selected metric. Sparklines (mini-graphs) on the cards themselves show dynamics only for the current year.

2. Global Trend Analysis and Drill-down
   * The central visual displays data for all available years, allowing you to track long-term dynamics.
   * Tooltips: when hovering over the trend graph, an extended tooltip appears, showing the distribution of profit by region and segment, as well as a list of the top 3 customers by margin and the category of goods they buy most often.
  
<img width="1284" height="463" alt="зображення" src="https://github.com/user-attachments/assets/f0afc228-08e4-4623-9f5c-2960659a0405" />

   * Drill down to transactions: In the upper right corner of the visual, there is a button that opens the Financial Performance Matrix. In this matrix, you can drill down from year to specific order date and product name.

<img width="1279" height="716" alt="зображення" src="https://github.com/user-attachments/assets/3fdce852-1f5a-4ec2-8a13-8628c3457994" />

3. Regional efficiency and factor analysis
   * Top 5 Cities: the bar chart shows the cities with the largest contribution to the selected metric. The tooltip on this chart shows the dynamics of the metric by day of the week, helping to identify patterns of customer activity.
     
<img width="1248" height="709" alt="зображення" src="https://github.com/user-attachments/assets/4c37153d-c1e8-4fd8-be84-67028fe56d78" />

   * Waterfall Chart (factor analysis): clearly demonstrates which factors influenced the change in profit compared to last year. In particular, a critical insight is visualized: the price decrease led to a loss of 48% of profit.

4. Smart navigation and recommendations
   * Smart Titles: dynamic text is displayed under the main heading that describes all applied filters (Date, Segment, Category, Region). For example, "East Performance in 2015 Category - Office Supplies", which eliminates errors in data interpretation when applying multiple filters at the same time.
   * Strategy block: Clicking on the "information" button (i) opens a window with specific recommendations (for example, focusing on high-profit regions in the West and East or optimizing the assortment in loss-making cities such as Houston or Philadelphia).
     
5. Strategic recommendations. A list of actions to improve performance is available through the "Information" button (i):
    * Focus on regions: concentrate investments in the West and East (California, New York, Washington).
    * Presence Optimization: reduce operations in unprofitable cities (Houston, San Antonio, Philadelphia).
    * Category Development: expand the range of Technology and Office Supplies categories (copiers, phones, accessories).
    * Segmentation: priority on the Consumer segment, which is the most profitable.
    
## 6. The **Margin & Profitability** page is a specialized section of the dashboard designed for in-depth analysis of financial performance and identification of areas of profit loss.

1. KPI Cards
At the top of the page are four main metrics that provide a quick assessment of the current situation:
    - Margin Leakage (Loss): reflects margin losses, with negative dynamics -80.9%.
    - Revenue per Customer: average revenue per customer (2.90K), що зріс на 52.3%.
    - Avg Order Value: average order cost ($458,61).
    - Unprofitable Orders: Number of unprofitable orders (1318), яка зросла на 59.2%.
Unlike the main page, the sparklines on these cards display the trend for all available years.

<img width="1279" height="714" alt="зображення" src="https://github.com/user-attachments/assets/154c4f74-71d7-4baa-9fd1-dea933356da6" />

2. Product Portfolio Matrix. This scatter plot visual analyzes product subcategories along two axes: total revenue and margin.
   * Tooltips: when you hover over a point (subcategory), detailed information is displayed: sales volume in money and units, margin level, and quadrant name (for example, "Volume Builders" for the Storage category).
   * Classification: the system automatically groups products based on their profit contribution and sales volume, helping to identify strategically important items.

<img width="568" height="445" alt="зображення" src="https://github.com/user-attachments/assets/d2a626fa-f235-4ff6-bcb1-185ae560d668" />

3. Analysis of the impact of discounts (Margin by Discount). One of the most important graphs showing the direct dependence of profitability on discount policy:
   * The graph clearly shows how the margin becomes negative as discounts increase. At an 80% discount, losses reach -180%.
   * Regional drill-down: tooltip lets you see how discounts affect margins in specific regions.
  
<img width="725" height="446" alt="зображення" src="https://github.com/user-attachments/assets/bb73520e-a9ac-4e09-8b07-b929ee317898" />

4. Interactive features and Drill-down:
   * Drill-down button (i): Each KPI card has an icon in the top right corner. Clicking it expands a full-screen chart of Trend Unprofitable Orders (or other selected metric), where data can be viewed by quarter, month, and even individual day.

<img width="1075" height="600" alt="зображення" src="https://github.com/user-attachments/assets/62971bbc-7585-4467-8415-4e3be969343e" />

   * Regional analysis: The Margin by Region and Category visual allows you to compare the profitability of different categories across regions.
   * Dynamic headers: As with Summary, a list of all applied filters is displayed under the main page title, ensuring accurate interpretation of results.
