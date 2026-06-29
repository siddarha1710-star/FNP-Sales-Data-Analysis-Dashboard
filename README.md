# 🎁 FNP Sales Analysis Dashboard

An interactive Excel dashboard analyzing sales performance for **FNP (Ferns N Petals)** — built with PivotTables, PivotCharts, and slicers to track orders, revenue, delivery performance, and customer spending across occasions, categories, cities, and time periods.

<img width="1353" height="634" alt="fnp_dashboard" src="https://github.com/user-attachments/assets/bd5ea866-d81a-4f93-90a8-0f15149bf65b" />


## 📊 Overview

This dashboard provides a 360° view of sales performance, allowing stakeholders to filter and drill down into:

- **Total Orders & Revenue** — high-level KPIs at a glance
- **Revenue by Occasion** — Anniversary, Birthday, Diwali, Holi, Raksha Bandhan, Valentine's Day
- **Revenue by Category** — Cakes, Plants, Mugs, Sweets, Soft Toys, etc.
- **Revenue by Hour (Order Time)** — peak ordering hours
- **Revenue by Month** — seasonal trends across the year
- **Top 5 Products by Revenue**
- **Top 10 Cities by Order Volume**
- **Delivery performance** — average days between order and delivery

All visuals are fully interactive via slicers for **Order Date**, **Delivery Date**, and **Occasion**.

## 🧰 Tools & Techniques Used

- Microsoft Excel
- PivotTables & PivotCharts
- Slicers (date range + categorical filtering)
- Calculated KPI cards
- Data cleaning & structuring from raw order data

## 📈 Key Metrics

| Metric | Value |
|---|---|
| 🧾 Total Orders | 1,000 |
| 💰 Total Revenue | ₹35,20,984.00 |
| 🚚 Avg. Days Between Order & Delivery | 5.53 |
| 👤 Avg. Customer Spending | ₹3,520.98 |

<img width="1141" height="76" alt="fnpkpi" src="https://github.com/user-attachments/assets/7d7ced91-eb8f-471a-9606-d4b520516803" />

## 📊 Data Architecture & Data Model

To power our analytical dashboards and customer segmentation, we constructed a relational data model using a Star Schema design. This setup establishes relationships between our core transaction registry and dimension tables to allow for deep-dive slicing and dicing of metrics.

### Data Model Overview

Below is the entity-relationship diagram (ERD) mapping out how our datasets connect:

<img width="1090" height="785" alt="fnp_mode" src="https://github.com/user-attachments/assets/537e5eb2-4ad8-4392-a4dd-a38a1a3eaf34" />

### Table Breakdown & Schema Structure

The architecture consists of three primary tables linked by one-to-many ($1 \rightarrow *$) relationships:

#### 1. 👥 `customer` (Dimension Table)
Contains master data regarding customer demographics alongside advanced transactional segmentation attributes:
*   **Demographics:** `Name`, `City`, `Contact_Number`, `Email`, `Gender`, `Address`.
*   **RFM Metrics:** `Raw_Recency`, `Raw_Frequency`, `Raw_Monetary`.
*   **Scoring & Segmentation:** `R_Score`, `F_Score`, `M_Score`, `RMF_Cell`, and `Customer_Segment` (used to categorize users into groups like Champions, At-Risk, Loyal Customers, etc.).
*   **Cohort Tracking:** `Cohort_Start_Date` for tracking user retention over time.

#### 2. 🛍️ `orders` (Fact Table)
The central core transactional table that records every individual purchase activity and acts as the bridge between customers and products:
*   **Keys:** `Order_ID`, `Customer_ID`, `Product_ID`.
*   **Time & Delivery Analysis:** Tracks precise ordering patterns (`Order_Date`, `Order_Time`, `Month Name`, `Hour`, `Day`) and delivery fulfillment cycles (`Delivery_Date`, `Delivery_Time`, `Hour(delivery)`).
*   **Financials:** `Quantity`, `products.Price (INR)`, and calculated `total_revenue`.

#### 3. 📦 `products` (Dimension Table)
Stores product catalog metadata and inventory classification data:
*   **Attributes:** `Product_ID`, `Product_Name`, `Category`, `Price (INR)`, `Occasion`, `Description`.
*   **Revenue Performance:** Aggregated calculated fields including `Product_Revenue`, `Running_Total_Revenue`, and `Revenue_Percentage`.
*   **Inventory/Sales Classification:** Features `ABC_Class` categorization to segment high-value products from low-performing inventory.

---

### Key Analysis Enabled by This Model
*   **RFM Customer Segmentation:** Grouping customers by their buying patterns to run targeted marketing campaigns.
*   **Sales & Revenue Trends:** Tracking hourly, daily, and monthly revenue performance.
*   **Product ABC Analysis:** Identifying which specific categories and products drive 80% of the company's total revenue.
*   **Delivery Performance:** Calculating the time difference (`diference`) between ordering and delivery to find operational bottlenecks.



## 💡 Key Insights

- *Anniversary* and *Raksha Bandhan* generate the highest revenue among all occasions.
- *Cakes* and *Soft Toys* are the top-performing product categories.
- Order volume shows a strong seasonal spike, suggesting demand is concentrated around specific festive months.
- Top 10 cities account for a significant share of total orders, with Indore and Kanpur leading.
