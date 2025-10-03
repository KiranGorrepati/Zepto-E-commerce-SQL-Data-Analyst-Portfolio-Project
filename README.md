📦 Zepto E-commerce SQL Data Analyst Portfolio Project

A real-world SQL data analytics portfolio project based on inventory data scraped from Zepto – one of India’s fastest-growing quick-commerce startups. This project simulates a real analyst's workflow, from raw data import to business-focused SQL analysis.

📌 Project Overview

This project mirrors how data analysts work in the e-commerce and retail industry by using SQL to:

🗃️ Set up and clean a real-world e-commerce inventory database

🔍 Perform exploratory data analysis (EDA) on product listings

📉 Identify inconsistencies in pricing and availability

📊 Generate business insights using SQL queries

The end goal? To uncover insights that can support product, pricing, and inventory decisions.

📁 Dataset Overview

The dataset was originally scraped from Zepto's official product listings and shared on Kaggle. It mimics real inventory catalog data with messy entries, duplicates, and varied formats.

Each row represents a Stock Keeping Unit (SKU), where the same product may appear in different sizes, packaging, or discount offers.

🧾 Columns Description:
Column Name	Description
sku_id	Unique identifier for each product entry (Primary Key)
name	Product name
category	Product category (e.g., Fruits, Snacks, Beverages)
mrp	Maximum Retail Price (originally in paise, converted to ₹)
discountPercent	Discount percentage on MRP
discountedSellingPrice	Final selling price after applying discount
availableQuantity	Number of units available in inventory
weightInGms	Weight of product in grams
outOfStock	Boolean flag (TRUE/FALSE) indicating stock availability
quantity	Units per package (mixed with grams for loose produce)
🔧 Project Workflow
1️⃣ Database Setup

We first created the zepto table with appropriate data types:

CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);

2️⃣ Data Import

Import the dataset via pgAdmin or PostgreSQL CLI:

\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv' WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');


Note: If you face encoding issues, re-save the CSV file using UTF-8 CSV format.

🔍 Exploratory Data Analysis (EDA)

Performed data profiling using SQL queries:

Counted total records

Checked for missing/null values

Identified unique product categories

Compared in-stock vs out-of-stock items

Detected duplicate products with varying SKUs

🧹 Data Cleaning

Performed cleaning operations to improve data quality:

Removed rows with MRP or discountedSellingPrice = 0

Converted prices from paise to rupees

Removed invalid or inconsistent data entries

📊 Business Insights (SQL Analysis)

Key insights extracted using SQL:

✅ Top 10 Best Value Products (based on highest discount %)
✅ Out-of-stock High MRP Products – potential revenue loss
✅ Estimated Potential Revenue by product category
✅ High-MRP, Low-Discount Products – identify overpriced items
✅ Top Categories by Avg Discount %
✅ Price per Gram Analysis – identify value-for-money items
✅ Weight-based Product Segmentation: Low, Medium, Bulk
✅ Total Inventory Weight per category

🚀 Getting Started
Clone the Repository
git clone https://github.com/amlanmohanty/zepto-SQL-data-analysis-project.git
cd zepto-SQL-data-analysis-project

Run SQL Analysis

Open zepto_SQL_data_analysis.sql in your SQL editor (e.g., pgAdmin, DBeaver)

Create a new database and run the SQL file to set up schema and queries

Import the CSV dataset (UTF-8 format recommended)
