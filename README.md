# Shopify Sales Analysis Project

🛍️ This project provides a comprehensive analysis of Shopify sales data, focusing on customer behavior, product performance, revenue patterns, and regional distribution. By leveraging both **SQL for data extraction** and **Power BI for visualization**, this project uncovers actionable insights to optimize e-commerce strategies. The analysis covers a representative dataset, offering a snapshot of real-world sales, order trends, and payment adoption.

---

## Background

E-commerce businesses thrive on **data-driven decision-making**. Understanding customer behavior, product performance, and revenue streams is essential for growth and profitability. This project was designed to:  

- Identify **top-performing products** and revenue-generating categories  
- Examine **customer spending patterns** and order frequency  
- Measure **average order value and basket size**  
- Investigate **geographic sales distribution** to identify key markets  
- Track **payment gateway adoption** to understand customer preferences  
- Assess **tax collection and high-value transactions** for financial insights  

By combining SQL-based data analysis with **Power BI dashboards**, the project provides **visual storytelling** of Shopify’s business operations, helping stakeholders make informed marketing, inventory, and sales decisions.  

The goal is not just to analyze raw numbers but to **transform data into strategic insights**, enabling targeted business growth and operational optimization.  

---

## Tools Used

This project leverages a combination of data management, analysis, and visualization tools to ensure **accuracy, efficiency, and professionalism**:  

- **SQL (PostgreSQL / MySQL):**  
  - Extracted, filtered, and aggregated Shopify sales data  
  - Enabled complex queries for revenue, orders, top customers, product categories, and regional analysis  

- **Power BI:**  
  - Created **interactive dashboards** for high-level and granular insights  
  - Developed **DAX measures** to calculate KPIs like total sales, average order value, revenue by product, and customers by state  
  - Enabled **dynamic visualizations** for filtering by product type, city, and payment gateway  

- **Visual Studio Code / SQL Editor:**  
  - Used as the query editor and project management environment  
  - Ensured clear, well-documented scripts for reproducibility  

- **Git & GitHub:**  
  - Version control for SQL scripts, Power BI documentation, and project artifacts  
  - Facilitated collaboration, project tracking, and easy sharing  

- **Excel / CSV:**  
  - Initial data exploration and cleaning before importing into Power BI  

---

This combination of tools ensures **robust data analysis**, **interactive visualization**, and **actionable insights**, making this project **professional-grade and business-ready**.


## ❓ SQL Questions Analyzed  
The following SQL queries were written and executed to answer key business questions:  

1. **What is the total sales revenue?**  
2. **Who are the top 5 customers by total spending?**  
3. **What are the sales by product category?**  
4. **What is the sales performance by city?**  
5. **How many orders has each customer placed?**  
6. **What is the average quantity of items per order?**  
7. **What is the breakdown of sales by payment gateway?**  
8. **What is the total amount of tax collected?**  
9. **What are the top 5 largest orders by total price?**  
10. **What is the customer distribution by state?**  

---
🔍 SQL queries? Check them out here: [project sql folder](/Sql/)

---

## 📊 The Analysis  
 

Each SQL query was designed to extract meaningful insights from Shopify sales data.  

---

### 1. Total Sales Revenue  

```sql
SELECT SUM("Total Price Usd") AS Total_Revenue
FROM shopify_sales;
```

Provides the overall revenue generated from all sales.
Insight: The store generated $2.74M, which gives a clear high-level picture of business performance.

### 2. Top 5 Customers by Total Spending

```sql
Copy code
SELECT "Customer Id", SUM("Total Price Usd") AS Total_Spent
FROM shopify_sales
GROUP BY "Customer Id"
ORDER BY Total_Spent DESC
LIMIT 5;
```

Identifies the most valuable customers in terms of revenue contribution.
Insight: The top customer spent over $9.2K, making them highly valuable for loyalty and retention strategies.

### 3. Sales by Product Category

```sql
Copy code
SELECT "Product Type", SUM("Total Price Usd") AS Total_Revenue
FROM shopify_sales
GROUP BY "Product Type"
ORDER BY Total_Revenue DESC;
```

Shows revenue breakdown by product type.
Insight: Tennis Shoes and Running Shoes are the top-selling categories.

### 4. Sales Performance by City

```sql
Copy code
SELECT "CITY", SUM("Total Price Usd") AS Revenue
FROM shopify_sales
GROUP BY "CITY"
ORDER BY Revenue DESC
LIMIT 3;
```

Ranks cities by revenue performance.
Insight: Houston, New York, and Miami are the leading cities in sales.

### 5. Orders per Customer

```sql
Copy code
SELECT "Customer Id", COUNT("Order Number") AS Number_of_Orders
FROM shopify_sales
GROUP BY "Customer Id"
ORDER BY Number_of_Orders DESC;
```

Tracks how many orders each customer has placed.
Insight: Most customers placed only one order, suggesting low repeat purchase rates. 

---

# 📈 Power BI Analysis (DAX Measures)

This section summarizes the **Power BI measures** used in the Shopify project, along with their **DAX formulas** and purpose.

---

## Sales & Revenue Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Total Sales** | `Total Sales = SUM(shopify_sales[Total Price Usd])` | Calculates total revenue from all sales. |
| **Total Orders** | `Total Orders = DISTINCTCOUNT(shopify_sales[Order Number])` | Counts the number of unique orders. |
| **Total Customers** | `Total Customers = DISTINCTCOUNT(shopify_sales[Customer Id])` | Counts the number of unique customers. |
| **Average Order Value (AOV)** | `Average Order Value = DIVIDE([Total Sales], [Total Orders])` | Shows the average value of an order. |
| **Average Quantity Per Order** | `Average Quantity Per Order = AVERAGE(shopify_sales[Quantity])` | Displays the average number of items purchased per order. |
| **Total Tax Collected** | `Total Tax Collected = SUM(shopify_sales[Total Tax])` | Shows total tax amount collected across all sales. |

---

## Customer & Product Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Customer Total Spend** | `Customer Total Spend = SUM(shopify_sales[Total Price Usd])` | Tracks total spending by each customer. |
| **Revenue by Product Type** | `Revenue by Product Type = SUM(shopify_sales[Total Price Usd])` | Calculates total revenue per product category. |
| **Customers by State** | `Customers by State = DISTINCTCOUNT(shopify_sales[Customer Id])` | Measures unique customers across different states. |

---

## Payment & Gateway Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Revenue by Gateway** | `Revenue by Gateway = SUM(shopify_sales[Total Price Usd])` | Shows total revenue generated via each payment method. |
| **Revenue by Gateway %** | `Revenue by Gateway % = DIVIDE([Revenue by Gateway], CALCULATE([Revenue by Gateway], ALL(shopify_sales[Gateway])))` | Calculates the percentage share of each payment gateway in total sales. |

---

## Dashboard Screenshot

![Shopify Sales Dashboard](Powerbi/Shopify.png)
![Shopify Sales Dashboard](Powerbi/Report.png)

---

## Key Performance Indicators (KPIs)

The dashboard highlights the most important top-level metrics from the sales data:

| KPI | Value | Description |
|-----|-------|-------------|
| **Total Revenue** | $2.75 M | Total revenue generated from all sales. |
| **Total Tax** | $249.7 K | Total amount of tax collected from all orders. |
| **Total Quantity Sold** | 6,403 | Total number of individual items sold. |
| **Total Orders** | 2,403 | Total number of unique orders placed. |

---

## Visualizations and Insights

### 1. Daily Revenue Trend
- **Type:** Line chart  
- **Description:** Shows total revenue generated each day.  
- **Insight:** All sales activity in this dataset occurred in **March 2025**. Helps identify peak sales days.

### 2. Top 5 Products by Revenue
- **Type:** Bar chart  
- **Description:** Displays the top 5 products contributing the most revenue.  
- **Insight:** **Tennis Shoes ($575K)** and **Running Shoes ($570K)** are the strongest revenue drivers.

### 3. Top 5 Cities by Revenue
- **Type:** Bar chart  
- **Description:** Ranks cities based on total sales revenue.  
- **Insight:** **Houston ($177K)**, **New York ($104K)**, and **Miami ($92K)** are the top three revenue-generating cities.

### 4. Orders by Payment Method
- **Type:** Donut chart  
- **Description:** Shows proportion of orders processed by each payment gateway.  
- **Insight:** Payment methods are nearly evenly split, with **Shopify Payments (50.75%)** slightly ahead of **Manual (49.25%)**.

### 5. Orders by State
- **Type:** Map visualization  
- **Description:** Color-coded map showing concentration of orders across US states.  
- **Insight:** Highest customer concentration is in **California, Texas, and Florida**.



# What I Learned

Throughout this project, I've leveled up my SQL and Power BI skills while diving deep into real e-commerce data:

- **🧩 Advanced SQL Analysis:** Mastered complex SQL queries, including `GROUP BY`, `SUM()`, `AVG()`, `COUNT()`, and `DISTINCT`, to extract meaningful insights on revenue, orders, top customers, and product performance.
- **📊 Data Aggregation & Insights:** Learned to transform raw sales data into actionable insights—like total revenue, average order value, product category performance, and regional sales distribution.
- **💡 Analytical Problem-Solving:** Developed skills to translate business questions into SQL queries and Power BI visualizations for clear, data-driven decision-making.
- **🛍️ Customer & Product Insights:** Understood customer behavior, order patterns, and product popularity through top spenders, frequent buyers, and high-revenue products.
- **📈 Power BI & DAX Mastery:** Created dynamic measures to analyze sales and performance:
  - `Total Sales` → Total revenue across all orders  
  - `Average Order Value (AOV)` → Average spending per order  
  - `Total Orders` & `Total Customers` → Track transaction and customer counts  
  - `Revenue by Product Type` & `Revenue by Gateway` → Product and payment insights  
  - `Customers by State` → Regional customer distribution  
  These measures made dashboards interactive and easy to interpret.
- **⚡ Storytelling with Data:** Learned to narrate an end-to-end story from raw sales data to revenue trends, top products, customer behavior, and regional insights—providing actionable business recommendations for e-commerce strategy.


## Closing Thoughts

This project significantly strengthened my SQL and Power BI skills while offering a hands-on understanding of real-world e-commerce data. The insights gained from analyzing Shopify sales data not only demonstrate technical proficiency but also highlight how data-driven decisions can optimize revenue, product strategy, and customer engagement.  

For aspiring data analysts, this project underscores the value of mastering both **data querying (SQL)** and **data visualization (Power BI/DAX)** to extract actionable insights. It emphasizes the importance of continuous learning, adapting to new tools, and building a strong analytical mindset to stay competitive in the ever-evolving field of data analytics.



## 🏁 Conclusion & Takeaways

This analysis of Shopify sales data provides a clear view of the business’s performance and customer behavior. Key takeaways include:  

- **Revenue Drivers:** Tennis Shoes and Running Shoes are the top-grossing products, driving most of the revenue.  
- **Customer Insights:** Top spenders contribute disproportionately to revenue; most customers place only a single order, indicating opportunities for retention programs.  
- **Regional Performance:** Houston, New York, and Miami generate the highest revenue, with California, Texas, and Florida having the largest customer bases.  
- **Payment Patterns:** Shopify Payments slightly outperforms manual methods, highlighting the adoption of digital payments.  
- **Operational Insights:** Average order size and quantity per order provide insights for inventory and marketing strategies.  

Focusing on **high-value customers, top-performing products, regional marketing, and payment optimization** can significantly boost profitability and business efficiency.
