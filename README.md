# Retail Inventory Availability & Stockout Risk Analysis Dashboard

## Project Overview

This project focuses on analysing retail inventory availability, identifying recurring stockout patterns, monitoring inventory risks and evaluating potential revenue exposure across multiple warehouses. Developed using **Microsoft Excel, Power Query and Power Pivot**, the solution transforms raw inventory, sales, product, warehouse, supplier and purchase order data into an interactive inventory management dashboard to support data-driven replenishment decisions and improve inventory availability.

## Business Objective

To ensure continuous product availability by identifying inventory shortages, monitoring stockout risks and preventing potential revenue losses across warehouses. The project aims to provide actionable insights into inventory coverage, product demand, supplier lead times and replenishment requirements, enabling businesses to make informed inventory management decisions.

## Business Problems Addressed

The analysis addresses the following key inventory management challenges:

1. How much inventory is actually available across different warehouses?
2. Which products are currently out of stock?
3. Which products are approaching critical stockout conditions?
4. How many days will the available inventory last based on historical demand?
5. Which product categories and warehouses experience the highest inventory risks?
6. Which products are likely to run out before their suppliers can deliver replenishment orders?
7. How much potential revenue is exposed to insufficient inventory?
8. Which products and warehouses require immediate replenishment attention?

## Tools & Technologies

- **Microsoft Excel:** Dashboard development, PivotTables, PivotCharts, KPI calculations, slicers and interactive reporting.
- **Power Query:** Data cleaning, transformation, validation, custom column creation and merging multiple datasets.
- **Power Pivot:** Data modelling, table relationships and analytical calculations across multiple datasets.
- **Excel Data Model:** Integrated analysis of inventory, product, warehouse, supplier, sales and purchase order information.

## Dataset Description

The project uses six interconnected datasets in CSV format:

| Dataset | Description |
|---|---|
| Product Master | Product details, categories, pricing, suppliers, MOQ and replenishment parameters. |
| Warehouse Master | Warehouse information, geographical locations, capacity and operational status. |
| Supplier Master | Supplier information, average delivery lead time, reliability, MOQ and payment terms. |
| Inventory Snapshot | Periodic inventory positions, stock movements, available stock, safety stock and reorder points. |
| Sales Transactions | Day-to-day product sales, quantities sold, selling prices, discounts and net sales. |
| Purchase Orders | Procurement records, ordered quantities, received quantities, expected delivery dates and actual delivery dates. |

The cleaned workbook contains:
- 360 product records.
- 6 warehouse records.
- 35 supplier records.
- 38,880 inventory snapshot records.
- 64,540 sales transaction records.
- 9,126 purchase order records.

## Data Cleaning & Transformation

Raw datasets contained multiple data quality issues. These were identified, documented and resolved using Power Query before performing the analysis.

Major data cleaning and transformation techniques included:

- Standardizing inconsistent text formats using Trim, Clean and Capitalize transformations.
- Converting product, warehouse, supplier, transaction and purchase order identifiers into consistent uppercase formats.
- Identifying and removing duplicate records and duplicate primary key entries.
- Handling missing text values by replacing blanks with "Unknown" in non-key columns.
- Standardizing inconsistent supplier reliability percentage formats.
- Replacing null stock adjustment quantities with zero.
- Identifying duplicate inventory snapshot combinations using Snapshot Date, Product ID and Warehouse ID.
- Validating inventory stock movement calculations:

  `Closing Stock = Opening Stock + Stock Received - Units Sold + Stock Adjustment`

- Calculating available inventory:

  `Available Stock = Closing Stock - Reserved Stock - Damaged Stock`

- Calculating Days of Cover based on available inventory and average daily sales.
- Merging product and supplier information into the inventory snapshot dataset to obtain supplier lead times and product selling prices.
- Creating custom columns for stock risk classification and estimated revenue at risk.
- Preserving legitimate null actual delivery dates for open or not-yet-received purchase orders.

A separate **Data Quality Log** was prepared to document the identified data quality issues, affected columns or records, and the corresponding Power Query resolution techniques.

## Data Modelling

A relational data model was developed using Power Pivot to integrate the six datasets and enable cross-table analysis.

The major relationships include:

- Product Master → Inventory Snapshot
- Warehouse Master → Inventory Snapshot
- Product Master → Sales Transactions
- Warehouse Master → Sales Transactions
- Product Master → Purchase Orders
- Warehouse Master → Purchase Orders
- Supplier Master → Purchase Orders

This model enables integrated inventory, sales, warehouse and procurement analysis without unnecessarily duplicating information across tables.

## Inventory Risk Classification & Analytical Calculations

Several calculated fields were developed in Power Query to evaluate inventory health and potential stockout exposure.

**1. Days of Cover (DOC)**

Measures how long the currently available inventory can support demand based on average daily sales.

`Days of Cover = Available Stock / Average Daily Sales`

Where:

`Average Daily Sales = Units Sold / 30`

Records with zero units sold are excluded from Days of Cover calculations.

**2. Stock Risk Classification**

Products are categorized into four inventory risk levels:

- **Out of Stock:** Available stock is below zero.
- **High Risk:** Days of Cover are below supplier delivery lead time, or available stock is below the reorder point.
- **Moderate Risk:** Days of Cover equals supplier delivery lead time, or available stock equals the reorder point.
- **Low Risk:** Products that do not fall into the above conditions.

**3. Estimated Revenue at Risk**

Estimates potential revenue exposure when inventory coverage is insufficient to support demand during the supplier replenishment lead time.

`Revenue at Risk = MAX(0, Lead Time - Days of Cover) × Average Daily Sales × Selling Price`

These calculations help prioritize products based on inventory availability, replenishment urgency and potential revenue exposure.

## Dashboard KPIs

The interactive dashboard includes six key performance indicators:

1. **Total Available Stock:** Total quantity of inventory available across selected warehouses and product categories.
2. **Out-of-Stock Products:** Distinct count of products classified as out of stock.
3. **High-Risk Products:** Distinct count of products requiring urgent inventory attention.
4. **Average Days of Cover:** Average inventory coverage period based on available stock and daily demand.
5. **Average Supplier Delivery Days:** Average supplier lead time across the selected inventory records.
6. **Estimated Revenue at Risk:** Total estimated revenue exposure associated with insufficient inventory coverage.

## Dashboard Visualizations

The dashboard incorporates eight analytical visualizations to provide a comprehensive view of inventory performance:

1. **Monthly Stockout Trend:** Tracks changes in stockout occurrences over time to identify recurring inventory shortages.
2. **Stock Risk Distribution:** Shows the percentage distribution of products across different inventory risk levels.
3. **Product Category-wise Average Days of Cover:** Identifies categories with relatively lower inventory coverage.
4. **Warehouse-wise Inventory Demand vs Stock Availability:** Compares available inventory against product demand across warehouses.
5. **Top 10 Products by Stockout Occurrences:** Identifies products experiencing the highest frequency of stockouts.
6. **Top 10 Products by High-Risk Frequency:** Highlights products repeatedly approaching critical stockout conditions.
7. **Inventory Demand vs Stock Received Trend:** Compares monthly product demand against stock receipts to evaluate replenishment adequacy.
8. **Estimated Revenue at Risk by Product Category:** Identifies categories contributing the highest potential revenue exposure.

## Interactive Filters

The dashboard includes interactive slicers to support multidimensional analysis:

- Year
- Month
- Product Category
- Warehouse

These filters allow users to investigate inventory performance across different time periods, product categories and warehouse locations.

## Business Insights & Recommendations

The analysis identifies several important inventory management patterns and provides warehouse-specific, category-specific and product-specific recommendations.

Some of the key findings include:

1. **Warehouse Inventory Risk:** Mumbai West DC recorded the highest recent estimated revenue at risk of ₹45.96 lakh, with 55 high-risk products and the lowest average Days of Cover of 88.2 days. Delhi NCR Fulfillment Hub followed with ₹44.40 lakh in estimated revenue at risk.

2. **Recurring Warehouse Stockouts:** Kolkata Central DC recorded 766 historical stockout observations, the highest among all six warehouses. It also had the highest recent number of out-of-stock products (51).

3. **Category-wise Stockout Exposure:** Accessories consistently recorded the highest historical warehouse-wide stockout observations. In October 2026, the category also recorded 35 out-of-stock products and 53 high-risk products.

4. **Revenue Exposure by Category:** Mobile Phones recorded the highest historical warehouse-wide estimated revenue at risk of ₹12.65 crore, followed by Laptops at ₹7.34 crore.

5. **Critical Inventory Coverage:** Storage, Accessories and Mobile Phones historically recorded relatively lower average Days of Cover. Storage products recently showed critically low inventory coverage across all warehouses except Nagpur Transit Warehouse.

6. **Repeated Product Stockouts:** Products such as Vistara Webcam 169, Novatech Android Smartphone 088, Orbis LED Monitor 343, Intra Headphones 295 and Aster Earbuds 316 experienced repeated stockout occurrences across the historical period.

7. **High-Value Product Exposure:** Orbis Gaming Laptop 026 at Mumbai West DC recorded ₹8.36 lakh in estimated revenue at risk, while Intra Android Smartphone 052 at the same warehouse recorded ₹7.49 lakh.

8. **Inconsistent Stockout Improvement:** Although stockout observations declined to 148 in August 2025, they increased to 274 in both March and April 2026. October 2026 also recorded 236 observations, a 34% increase compared with September 2026.

9. **Procurement Optimisation Opportunity:** May 2025 recorded insufficient stock receipts relative to demand, whereas June and July 2025 recorded excess stock receipts, indicating opportunities to improve procurement planning.

10. **Warehouse-specific Risk:** Chennai Service Warehouse showed recurring high-risk Networking products despite having a relatively comfortable overall inventory position.

### Key Business Recommendations

- Prioritize replenishment at Mumbai West DC and Delhi NCR Fulfillment Hub based on their higher estimated revenue exposure.
- Introduce warehouse-specific reorder points and safety stock levels at Kolkata Central DC.
- Review Accessories demand patterns, supplier lead times and replenishment parameters.
- Prioritize Mobile Phone replenishment at Delhi NCR, Mumbai and Kolkata.
- Investigate repeatedly unavailable products and establish corrective replenishment plans.
- Monitor recurring late purchase orders and evaluate supplier reliability.
- Identify excess and slow-moving inventory at Chennai and evaluate suitable stock transfers to warehouses experiencing shortages.
- Align procurement quantities with historical demand, stock receipts and stockout patterns.
- Introduce monthly management reviews covering stockout frequency, inventory coverage, high-risk products and supplier delivery performance.

A separate **Insights and Recommendations** document contains the detailed findings and corresponding business recommendations.

## Project Deliverables

The project includes the following deliverables:

- Interactive Excel Inventory Availability and Stockout Risk Dashboard.
- Cleaned datasets for all six source tables.
- Power Query data cleaning and transformation workflow.
- Power Pivot relational data model.
- KPI calculations and analytical PivotTables.
- Dashboard visualizations and interactive slicers.
- Data Quality Log documenting identified issues and resolution techniques.
- Detailed Insights and Recommendations document.

## Business Value

This project demonstrates how raw operational data can be transformed into meaningful business intelligence for inventory and supply chain management. By identifying recurring stockout patterns, evaluating inventory coverage, highlighting high-risk products and estimating potential revenue exposure, the solution helps inventory and procurement teams prioritize replenishment activities, improve warehouse-level inventory planning and make more informed operational decisions.

## Skills Demonstrated

**Excel | Advanced Excel | Power Query | Power Pivot | Data Cleaning | Data Transformation | Data Modelling | Data Analysis | Inventory Analytics | Supply Chain Analytics | KPI Development | Dashboard Development | Business Intelligence | Data-Driven Decision Making**
