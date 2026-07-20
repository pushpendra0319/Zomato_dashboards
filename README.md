🍽️ Zomato Sales & Operations Dashboard — Power BI

An end-to-end, interactive Power BI dashboard built on Zomato-style food delivery data, analyzing revenue, restaurant performance, customer behavior, and delivery/service quality across a multi-table relational dataset.

📌 Project Overview

This project transforms raw, multi-table restaurant and delivery data into a fully interactive 4-page Power BI dashboard. It follows a structured BI workflow — data cleaning, data modeling (star schema), calculated columns, visualization design, and interactivity (slicers, cross-filtering, drillthrough) — to answer key business questions about revenue performance, customer growth, restaurant popularity, and delivery service quality.

The dataset consists of 5 relational tables:

Table	Description
zomato_customers	Customer details — city, state, signup date
zomato_restaurants	Restaurant details — cuisine, rating, cost, city
zomato_orders	Order-level transactions — status, payment method, delivery time
zomato_orders_item	Line-item level detail — dish, quantity, price
zomato_delivery	Delivery details — rider, food rating, delivery rating, review comments

🎯 Objectives
Build a clean, relational star-schema data model from raw Excel tables
Track overall business performance through key metrics (revenue, orders, customers)
Identify top-performing restaurants, cuisines, and cities
Analyze customer growth and ordering behavior over time
Evaluate delivery service quality and rider performance
Deliver a fully interactive, drillable dashboard 
🧹 Data Cleaning & Preparation (Power Query)
Verified and corrected column data types (dates as Date, ratings/costs as Decimal/Whole Number)
Removed redundant or duplicate rows
Standardized table and column naming for clarity
Created a calculated column Total Price = quantity * price_rs in zomato_orders_item to represent per-line-item revenue, since raw data only contained quantity and unit price separately
Grouped the continuous delivery_rating column into equal-sized bins (bin size = 1) to support distribution analysis via histogram-style charts

🗂️ Data Modeling
Built a star schema with zomato_orders as the central fact table, related to zomato_customers, zomato_restaurants, zomato_orders_item, and zomato_delivery
Created a dedicated Date Table using:
dax
  DateTable = CALENDAR(MIN(zomato_orders[order_date]), MAX(zomato_orders[order_date]))

with supporting columns (Year, MonthNum, Month, Quarter, Weekday) and marked it as the official Date Table for time-intelligence support

Related DateTable[Date] → zomato_orders[order_date] (one-to-many)
Ensured all dimension tables connect to the fact table via customer_id, restaurant_id, and order_id
📊 Values / Aggregations Used

This project intentionally avoids custom DAX measures, relying instead on calculated columns and implicit aggregation (Sum, Average, Count, Distinct Count) applied directly within visuals — demonstrating a solid grasp of Power BI fundamentals.

Metric	Field	Aggregation
Total Revenue	Total Price	Sum
Total Orders	order_id	Distinct Count
Total Customers	customer_id	Distinct Count
Average Delivery Time	delivery_time_minutes	Average
Average Rating	rating / food_rating / delivery_rating	Average
Delivery Rating Distribution	delivery_rating (bins)	Count

🛠️ Tools & Technologies Used
Power BI Desktop — data modeling, DAX-free calculated columns, report design
Power Query Editor — data cleaning, transformation, custom column creation
Excel — source data format
GitHub — version control and project hosting

⚙️ Power BI Concepts Covered
Data import & transformation (Power Query)
Star schema data modeling & relationships
Calculated columns vs. Measures (New Column vs. New Measure)
Custom Date Table creation & time intelligence readiness
Data binning/grouping for distribution analysis
Implicit aggregation (Sum, Average, Count, Distinct Count)
Visual selection strategy (bar vs. column vs. treemap vs. scatter vs. map)
Slicers & cross-page slicer synchronization
Cross-filtering (native interactivity)
Drillthrough pages for record-level detail
Report page design: KPI cards, Top-N filtering, page backgrounds

📈 Chart Information & Dashboard Summary
Page 1 — Business Overview
Visual	Chart Type	Purpose
KPI Cards	Card	Total Revenue, Total Orders, Avg Delivery Time, Total Customers
Revenue Trend	Line Chart	Month-wise revenue movement
Orders by Status	Donut Chart	Delivered vs. Cancelled vs. Returned split
Payment Method Split	Column Chart	Distribution of payment methods used
Revenue by City	Bar Chart	Top revenue-generating cities

Purpose: A quick, high-level snapshot of overall business health.

Page 2 — Restaurant Performance
Visual	Chart Type	Purpose
Top 10 Restaurants	Bar Chart (Top N)	Highest revenue-generating restaurants
Cuisine Popularity	Treemap	Order volume by cuisine type
Rating vs. Cost	Scatter Chart	Relationship between pricing and customer rating
Online Order Impact	Column Chart	Revenue split by online vs. offline orders
City-wise Restaurant Spread	Map	Geographic distribution of revenue

Purpose: Identifies which restaurants and cuisines drive the most business.

Page 3 — Customer Insights
Visual	Chart Type	Purpose
Customer Signups Over Time	Line/Area Chart	Customer base growth trend
Top Dishes Ordered	Bar Chart (Top N)	Most in-demand dishes
Avg Order Value by State	Column Chart	Regional spending patterns

Purpose: Understands customer growth and ordering preferences.

Page 4 — Delivery & Ratings
Visual	Chart Type	Purpose
Delivery Rating Distribution	Column Chart (Binned)	Spread of delivery ratings (histogram-style)
Avg Delivery Time by Rider	Bar Chart	Rider-wise performance comparison
Food Rating vs. Delivery Rating	Scatter Chart	Correlation between food and delivery satisfaction

Purpose: Evaluates service quality and operational efficiency.

Restaurant Detail Page (Drillthrough)

A dedicated drillthrough page filtered by restaurant_name, showing restaurant-specific KPIs, dish-level order details, monthly revenue trend, and rating distribution — accessible by right-clicking any restaurant in Page 2.

🔗 Interactivity Features

Slicers: Order Date, City, Cuisine, and Order Status — synchronized across all report pages
Cross-Filtering: Clicking any chart element dynamically filters all other visuals on the page
Drillthrough: Right-click any restaurant to navigate to a dedicated detail page with restaurant-specific insights.

💡 Key Insights
Revenue shows a clear month-over-month growth pattern between Q1 and Q2, with fluctuations tied to seasonal demand
A small set of top restaurants and cuisines account for a disproportionate share of total revenue
Higher pricing does not consistently correlate with higher ratings — indicating value-for-money matters more to customers than cost alone
The majority of deliveries fall within the 3–4 star rating range, suggesting solid but improvable service quality
Rider-wise delivery time varies noticeably, highlighting an opportunity for operational optimization

📁 Repository Structure
zomato-sales-dashboard-powerbi/
├── README.md
├── zomato_dashboard.pbix
├── data/
│   └── zomato_project_all_tables.xlsx
└── screenshots/
    ├── page1_business_overview.png
    ├── page2_restaurant_performance.png
    ├── page3_customer_insights.png
    └── page4_delivery_ratings.png
    
