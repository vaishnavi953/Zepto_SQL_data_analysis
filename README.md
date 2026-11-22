# Zepto E-commerce Inventory Analysis | SQL Project

**Author:** Vaishnavi Bondre

## Project Overview

This project analyzes a Zepto e-commerce inventory dataset using PostgreSQL. The objective is to explore product and inventory data, clean inconsistent pricing records, and answer business questions related to discounts, product availability, estimated inventory value, and inventory weight.

## Objectives

- Explore the structure and quality of the inventory dataset.
- Identify missing values, zero-priced records, product categories, and repeated product names.
- Convert MRP and discounted selling prices from paise to Indian rupees.
- Analyze discounts, out-of-stock products, category-level inventory value, and product value by weight.
- Translate SQL query results into practical business observations.

## Tools and Technologies

- **Database:** PostgreSQL
- **SQL Client:** pgAdmin (or another PostgreSQL client)
- **Dataset:** `zepto_v2.csv`
- **Analysis:** SQL aggregation, filtering, grouping, sorting, CASE expressions, and data cleaning

## Dataset

The supplied CSV contains **3,732 rows** and **9 columns**. Each row represents a product SKU entry. A product name may occur more than once because catalog entries can be listed under different categories or package details.

| Column | Description |
|---|---|
| `Category` | Product category |
| `name` | Product name |
| `mrp` | Maximum Retail Price, stored in paise |
| `discountPercent` | Discount percentage |
| `availableQuantity` | Available inventory quantity |
| `discountedSellingPrice` | Selling price after discount, stored in paise |
| `weightInGms` | Product weight in grams |
| `outOfStock` | Stock availability flag |
| `quantity` | Package quantity or produce quantity |

The SQL table adds `sku_id` as a generated primary key.

## Project Workflow

### 1. Database and Table Creation

Create a PostgreSQL table to store the inventory records. The SQL script defines `sku_id` as a `SERIAL PRIMARY KEY` and uses appropriate numeric, text, integer, and Boolean data types.

### 2. Data Import

Import `zepto_v2.csv` into the `zepto` table using pgAdmin's Import/Export feature or PostgreSQL's `\copy` command. Map the CSV columns to the table columns in this order:

`category, name, mrp, discountPercent, availableQuantity, discountedSellingPrice, weightInGms, outOfStock, quantity`

The generated `sku_id` is not imported from the CSV.

### 3. Data Exploration

The SQL analysis checks:

- Total number of records.
- Sample product records.
- Null values across the dataset.
- Distinct product categories.
- In-stock and out-of-stock SKU counts.
- Product names appearing against multiple SKU entries.

### 4. Data Cleaning

- Identify rows where MRP or discounted selling price is zero.
- Remove rows with zero MRP, as implemented in the supplied SQL script.
- Convert MRP and discounted selling price from paise to rupees by dividing by `100.0`.

**Cleaning note:** The supplied SQL script checks for either zero MRP or zero discounted selling price, but its `DELETE` statement removes rows only when `mrp = 0`. The supplied dataset contains 1 row with zero MRP and 1 row with zero discounted selling price; these are the same row.

### 5. SQL Business Analysis

The SQL script answers these business questions:

1. Which 10 products have the highest discount percentages?
2. Which products have an MRP above ₹300 and are out of stock?
3. What is the estimated inventory value for each category?
4. Which products have an MRP above ₹500 and a discount below 10%?
5. Which five categories have the highest average discount percentages?
6. What is the price per gram for products weighing at least 100 grams?
7. How can products be grouped into Low, Medium, and Bulk weight bands?
8. What is the total inventory weight for each category?

## Key Dataset Findings

The following figures are calculated from the supplied CSV. Price values are converted from paise to rupees, and the one zero-MRP row is excluded for the cleaned analysis.

- **Raw records:** 3,732
- **Product categories:** 14
- **Distinct product names:** 1,681
- **Repeated product names:** 1,214 names appear in more than one row.
- **In-stock SKU rows:** 3,279 (87.86%)
- **Out-of-stock SKU rows:** 453 (12.14%)
- **Estimated inventory value:** ₹2,243,080.60

The estimated inventory value is calculated as `discountedSellingPrice × availableQuantity`. It is an inventory-value estimate, not realized sales revenue.

## How to Run the Project

1. Install PostgreSQL and open pgAdmin or another PostgreSQL client.
2. Create a database for the project.
3. Create the `zepto` table using the table definition in `Zepto_SQL_data_analysis.sql`.
4. Import `zepto_v2.csv` into the table, mapping the nine CSV columns and allowing PostgreSQL to generate `sku_id`.
5. Execute the SQL script in sections: exploration, cleaning, and business analysis.
6. Review the query outputs and compare them with the accompanying Business Insights PDF.

## Project Files

- `README.md` — Project documentation.
- `Zepto_SQL_data_analysis.sql` — Table creation, exploration, cleaning, and business analysis queries.
- `zepto_v2.csv` — Inventory dataset.
- `Business_Insights_Zepto.pdf` — Business findings and recommendations.

## Author

**Vaishnavi Bondre**
