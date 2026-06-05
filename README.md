# Hybrid-ETL-Postgre-data-audit
A production-grade Hybrid ETL pipeline that cleans raw e-commerce logs in Python and mounts them into a PostgreSQL instance. Deploys advanced relational SQL querying, multi-layered groupings, and aggregation audits.
# 📊 Hybrid ETL Pipeline & Enterprise SQL Data Analysis (Project 3)
## 🛠️ Industrial Training Kit Milestone — DecodeLabs

## 📌 Project Overview
Operating on raw transactional data at scale introduces high redundancy. This project implements a modern **Hybrid ETL (Extract, Transform, Load)** framework. 

Instead of manual database cleaning, the dataset was programmatically sanitized and structured using **Python (Pandas)**, and then seamlessly loaded into an enterprise-grade **PostgreSQL** relational database. Once ingested, production-ready **SQL Queries** were deployed to execute behavioral filters, sorting optimizations, and multi-layered operational groupings.

---

## ⚙️ The ETL Architecture (How it Works)

1. **Extract & Transform (Python Layer):** Raw e-commerce logs were ingested via Python. Missing entries were handled, data types standardized, and anomalies resolved to establish a clean data baseline.
2. **Load (Data Engineering Layer):** Using `SQLAlchemy` and `psycopg2`, the cleaned dataset was automatically pushed from Python into a local PostgreSQL instance as a structured table named `orders_table`.
3. **Analyze (SQL Layer):** Advanced relational queries were executed directly inside the PostgreSQL engine to unlock operational business intelligence.

---

## 🏗️ Relational Database Schema Mapping
The structured table `orders_table` maintains 100% downstream data integrity with the following data models:
- `OrderID` (Text/Varchar - Cleaned Unique Index Field)
- `Product` (Text/Varchar - Categorical Variant Category)
- `TotalPrice` (Numeric/Float - Sanitized Transactional Value)
- `OrderStatus` (Text/Varchar - Operational State Vector)

---

## 💻 SQL Query Catalog & Relational Logic
Below are the definitive SQL scripts developed and verified through the PostgreSQL engine as per the DecodeLabs manual:

### 1️⃣ Structural Ingestion Verification (SELECT / FROM)
* **Objective:** Confirms successful database mapping and schema consistency post-Python ingestion.
```sql
SELECT "OrderID" AS order_id, "Product" AS product, "TotalPrice" AS total_price, "OrderStatus" AS order_status 
FROM orders_table 
LIMIT 5;

2️⃣ Conditional Fulfillment Filtering (WHERE Clause)
​Objective: Discards operational transaction noise to target successfully delivered orders.

SELECT "OrderID" AS order_id, "Product" AS product, "TotalPrice" AS total_price, "OrderStatus" AS order_status 
FROM orders_table 
WHERE "OrderStatus" = 'Delivered' 
LIMIT 5;

3️⃣ Premium Revenue Tier Ranking (ORDER BY Clause)
Objective: Instantly filters and ranks high-magnitude revenue orders to identify high-net-worth bulk buyers.
SELECT "OrderID" AS order_id, "Product" AS product, "TotalPrice" AS total_price 
FROM orders_table 
ORDER BY "TotalPrice" DESC 
LIMIT 5;

4️⃣ Inventory Performance Metrics (GROUP BY & Aggregations)
Objective: Collapses 1,200 rows into dynamic product groups to compute total volume (COUNT), total revenue (SUM), and average order value (AVG).
SELECT 
    "Product" AS product, 
    COUNT("OrderID") AS total_orders, 
    SUM("TotalPrice") AS total_revenue, 
    ROUND(AVG("TotalPrice")::numeric, 2) AS avg_order_value
FROM orders_table 
GROUP BY "Product"
ORDER BY total_revenue DESC;

5️⃣ Operational Risk & Supply Chain Audit (Multi-Layered Grouping)
Objective: Audits systemic leakage by analyzing order velocity and monetary exposure against courier pipelines.
SELECT 
    "OrderStatus" AS order_status, 
    COUNT("OrderID") AS order_count,
    SUM("TotalPrice") AS revenue_impact
FROM orders_table 
GROUP BY "OrderStatus"
ORDER BY order_count DESC;

📈 Key Insights & Analytical Verdicts
Pipeline Integrity: The Python-to-PostgreSQL automation successfully processed all 1,200 data rows with zero truncation or datalink degradation.
Revenue Anchor Points: Grouped aggregations confirm that Chairs and Printers dominate the operational landscape, driving the highest aggregate revenue under SUM(TotalPrice).
🚨 Operational Bottleneck: The SQL status breakdown reveals an alarming trend where over 40% of orders sit within Cancelled or Returned cycles, pointing to high friction in fulfillment that requires immediate logistical optimization.

📂 Repository Layout & Deliverables
🐍 Setup_Postgres_Project3.py: Python ETL automated script that cleans data and mounts it directly onto the PostgreSQL local instance.
🐍 SQL_Postgres_Project3.py: Automated query engine executing production-ready SQL scripts via Python.
📄 Project3_SQL_Analysis_Report.docx: Deep-dive executive Word report containing live query results and pgAdmin dashboard snapshots.
📝 README.md: System documentation manual.
