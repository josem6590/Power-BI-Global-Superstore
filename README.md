# 📊 Global Superstore Analysis

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](#)


> **Live Interactive Report:** [Link to embedded Power BI publish-to-web link or demo]  

---

## 📌 Background and Overview
Global Supertore is an online retailer that distributes products across the globe. Specialising - from what I can see in the dataset - office furniture, supplies and technology. With data available from 2011 - 2014 we will endeavour to answer the following questions using Power BI:

* Analysing Sales by Revenue and Orders, and how we are tracking over the years?
* Looking at sales by month and year, do we see a seasonality pattern?  
* Which products are top sellers and which are our worst sellers? Do we need to remove/replace items from our inventory?   
* What products have the lowest and highest profit margin?  
* What is the distribution of customers by country?  
* Are we at risk of being too heavily weighted in one country/product?

<!--• Analysing Sales by Revenue and Orders, and how we are tracking over the years?-->


**KPI:**
Sales, Revenue, Profit Margin.  
**Objective:** Build a Power BI report to track KPIs and answer the above questions.  
**Target Audience:** Regional Sales Managers and Senior VP of Sales.  

---

## 🛠️ ETL
For a brief outline of the flow of data and ETL, see the [DataArch](DataArch.md).

## 📐 Data Modeling (Star Schema)
See data model here [Schema](Schema.png).

* **Model Type:** Star Schema (1 Fact Table, 4 Dimension Tables)
* **Key Dimensions:** `Dim_Customer`, `Dim_Product`, `Dim_Date`, `Dim_Geography`
  * Dim_Date was created using DAX and marked as the date table.
  * Location data categories were used for the Dim_geography table and hierarchies created.
  * Unnecessary columns where hiden from view for report viewers. 
* **Fact Table:** `Fact_Sales`
* **Relationships:** Enforced `1-to-Many` single-direction relationships to optimise DAX performance and prevent circular dependencies.


## 📐 Key DAX Measures & Analytics
For a breakdown of key DAX measures used in this report, see the [DAX Code Documentation](DAX_DOCUMENTATION.md).

* **Parameters:** Created to hold the following measures; Total Revenue, Total Profit and Total Orders. This enabled report users have more control, especially on the overview report page so they would be able to see the page by each parameter.

* **Top 3 Metrics:** 
Revenue
Orders
Profit
  
---

# 📊 Global Superstore - Power BI Analytics Project

## 🔍 Executive Summary
* **Performance Overview (2011–2014):** Global Superstore achieved **$12.6M** in Total Revenue across **25K** orders. 
* **Category Breakdown:** Revenue is evenly distributed across Furniture, Office Supplies, and Technology (ranging from 30% to 38% each). However, Office Supplies drives the highest volume, accounting for **53%** of all orders. 
* **Revenue Forecasting:** Projected revenue for 2015 is **$5M**, representing a **16% YoY growth**. While positive, this indicates a deceleration compared to the 26% YoY growth achieved in 2014.
* **Profitability Gap:** Despite generating 30% of total revenue, the **Furniture** category accounts for only **18% of total profit**—yielding less than half the profit of both Office Supplies and Technology.

---

## 🔍 Exploratory Data Analysis (EDA)

![Dashboard](Dashboard.png)

* **YoY Growth:** Revenue, order volume, and profit all closed the year strong, trending **24%–26% up** compared to the previous year.
* **Seasonality Trends:** Sales consistently build throughout the year, peaking in **June, September, and November**, with recurring historical dips in July and October.
* **Top Markets:** The **United States** remains our primary market with a 20% share, followed closely by **Australia**, which recently overtook Mexico for the second spot.


### The Negative Profit Deep-Dive
Initial analysis of the product matrix revealed that **Table sales are consistently operating at a loss**, failing to break even. 

To investigate further, I plotted order profitability on the Product Analysis page, which revealed a significant volume of transactions yielding negative margins. Notably, this trend of loss-making orders is present across *all* product categories, not just Furniture. 

To isolate and action this issue, I developed a dedicated **Profit & Loss Report** page featuring: 
* A KPI tracking the count of countries experiencing negative profit. 
* A geographic map visualizing the ratio of positive vs. negative profit orders by region. 
* A breakdown of negative order volume grouped by country. 
* A granular, exportable matrix detailing negative margins by Product and Order ID, designed to assist the commercial team in reassessing pricing strategies.

### Country-Specific Analysis Page (Drill-Through)
To allow stakeholders to perform targeted regional analysis, I implemented dynamic **Drill-Through navigation** from the main dashboard to a dedicated Country Deep-Dive page. Selecting any country filters the page to display localized operational and financial trends:
* **Geographic Distribution Map:** Visualizes Revenue by State/Region, making it easy to spot top-performing sales territories within a single country.
* **Profit Trend & Anomaly Detection:** A daily Profit line chart equipped with Power BI’s native **Anomaly Detection** algorithm to automatically highlight and explain unexpected margin spikes or drops over time.
* **Time-Based Operational Matrix:** A granular breakdown indexed by Month and Day of Month, featuring key calculated metrics:
  * **Order Metrics:** Total Orders, Total Items Ordered, and Average Items per Order (Basket Size).
  * **Financial Metrics:** Total Revenue, Revenue YoY Growth (%), Total Profit, and Profit Margin (%).

### AI Revenue Drivers & Customer Analytics

![Logistics & Customer Insights](KeyIN.jpg)

To identify underlying revenue drivers and customer behaviors, I utilized Power BI's native **Key Influencers** and **Top Segments** AI visuals to run automated cluster and regression analysis across transactions:

* **AI Revenue Influencers (Positive vs. Negative Drivers):**
  * **Top Revenue Boosters:** Transactions involving **Copiers** increase average revenue by **+$8.67K** above baseline, followed by **Bookcases** (+$5.76K) and **Chairs** (+$4.26K).
  * **Top Revenue Drag:** Placing orders in **Office Supplies** reduces average order value by **-$3.33K**. Sub-categories like **Labels** (-$3.09K), **Paper** (-$3.02K), and **Fasteners** (-$2.77K) pull average order sizes significantly below the global baseline.
* **Customer Segment Clustering:**
  * **High-Value Clusters:** Identified **3 premium segments** averaging **$6.6K–$7.4K** per order, with the top segment generating an average of **$7.43K** across 308 orders.
  * **Low-Value Clusters:** Identified **5 volume-heavy, low-yield segments** averaging under **$1.4K**, with the lowest segment averaging just **$621.60** per order (393 transactions).
* **Fulfillment & Market Segmentation:**
  * **Ship Mode:** **Standard Class** dominates revenue volume at **59.95% ($7.6M)**, while express options (**First Class** at 14.48% and **Same Day** at 5.28%) remain underutilized.
  * **Customer Base:** **Consumer** accounts for **51.48% ($6.5M)** of total revenue, while **Corporate ($3.8M / 30.25%)** and **Home Office ($2.3M / 18.27%)** highlight strong potential for targeted B2B growth.

---

## 🔍 Strategic Summary & Next Steps

While top-line metrics show strong YoY growth, the underlying volume of negative-margin orders means this growth is not a true reflection of business health. Addressing these loss-making transactions is critical. While correcting pricing or increasing shipping fees could improve margins, we must also model how those price hikes might impact overall sales volume.

### Outstanding Questions for Further Investigation
1. **Fulfillment Logistics:** Order IDs often begin with two-letter country codes that do not match the final shipping destination. If these prefixes represent distribution centers, is there a correlation between the distance from the fulfillment center to the customer and the resulting profit loss?
2. **Shipping Structures:** While initial checks showed no clear relationship between *Ship Mode* (e.g., Standard vs. Express) and profit loss, a deeper dive into the actual freight costs versus what the customer is being charged is necessary.
