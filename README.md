# PowerBI_readme

# 📊 Project Title: E-Commerce Order Analytics: Data Transformation & Relationship Modeling in Power BI

This project cleans, transforms, and models e-commerce order, product, and sales target data in Power BI to enable accurate profit, sales, and target-performance analysis.

## 📑 Table of Contents
* [Project Overview](#-project-overview)
* [Data Sources & Architecture](#-data-sources--architecture)
* [Data Transformation (ETL)](#-data-transformation-etl)
* [Data Model & DAX](#-data-model--dax)
* [Dashboard Features](#-dashboard-features)
* [Key Insights](#-key-insights)
* [How To Use](#-how-to-use)

---

## 🎯 Project Overview
* **Business Problem:** Order, product, and target data live in three separate, inconsistently formatted files with missing values and no defined relationships, making it hard to analyze profitability against sales targets.
* **Objective:** Build a clean, validated Power BI data model that consolidates order-level, product-level, and target-level data so profit margins, category performance, and target attainment can be analyzed reliably from one model.
* **Target Audience:** Sales Operations, Category Managers, and Business Analysts tracking profitability and progress against monthly category targets.

## 🗃️ Data Sources & Architecture
* **Source Systems:** Three local CSV files — `List of Orders.csv`, `Order Details.csv`, `Sales Target.csv`.
* **Data Volume:** List of Orders restricted to the first 500 rows (per assignment scope); Order Details and Sales Target imported in full.
* **Storage Mode:** Import mode (data loaded into Power BI's in-memory model via Power Query).

## ⚙️ Data Transformation (ETL)
* **Tool Used:** Power Query Editor (Transform Data).
* **Key Cleanups:**
  * Restricted List of Orders to first 500 rows
  * Order Date set to Date type; Amount and Target set to Fixed Decimal Number
  * CustomerName converted to Proper Case
  * Custom column **Location** = `City & ", " & State`
  * Custom column **Profit Margin** = `Profit / Amount` (as %)
  * Conditional column **Profit Status**: Profit < 0 → Loss, Profit = 0 → Break-Even, Profit > 0 → Profit
  * Merged List of Orders + Order Details on Order ID → **Orders Data**
  * Missing values identified and handled per column (replace, remove, or retain with justification)
  * Duplicate rows identified and resolved based on Order ID business logic
  * Orders Data sorted by Order Date (descending); filtered for a specific state (e.g., Tamil Nadu)
  * Order Details duplicated and grouped: Count of Order ID, Average Profit by Category, Total Amount by Sub-Category
  * Sales Target duplicated and grouped: Total Target by Month of Order Date
* **Custom Functions:** Conditional logic for Profit Status implemented via Power Query's Add Conditional Column (M code if/then/else on the Profit field).

## 🧠 Data Model & DAX
* **Model Type:** Relational model centered on a merged fact table, linked to a target reference table.
* **Fact Table:** Orders Data (merged List of Orders + Order Details — Order ID, Order Date, Customer Name, Location, Category, Sub-Category, Quantity, Amount, Profit, Profit Margin, Profit Status).
* **Reference Table:** Sales Target (Category, Month of Order Date, Target).
* **Relationships:**
  * List of Orders ↔ Order Details on **Order ID** (active)
  * Order Details ↔ Sales Target on **Category** (active)
* **Key Measures:**
  ```dax
  Total Profit = SUM('Orders Data'[Profit])
  ```
  ```dax
  Profit Margin % = DIVIDE(SUM('Orders Data'[Profit]), SUM('Orders Data'[Amount]))
  ```
  ```dax
  Total Target = SUM('Sales Target'[Target])
  ```

## 🖥️ Dashboard Features
* **Page 1: Data Model Overview:** Imported tables, row counts, and the Order ID / Category relationships.
* **Page 2: Profitability Deep Dive:** Profit, Profit Margin, and Profit Status by Category/Sub-Category, filterable by state (e.g., Tamil Nadu).
* **Page 3: Target vs Actual Performance:** Total Amount and Average Profit by Category compared against Total Target by Month of Order Date.
* **Design Theme:** Standard, business-friendly Power BI theme (not a graded requirement for this assignment).

## 💡 Key Insights
* **Trend A:** _[Fill in after running the transformations — e.g., which Category/Sub-Category has the highest Profit Margin.]_
* **Trend B:** _[Fill in — e.g., which state or category has the most "Loss" orders by Profit Status.]_
* **Recommendation:** _[Fill in — e.g., action for categories falling short of their monthly Sales Target.]_

## 🚀 How To Use
1. **Prerequisites:** Power BI Desktop (latest version) installed.
2. **File Formats:** Open the `.pbix` file directly, or re-import the three CSVs via Get Data if rebuilding from scratch.
3. **Data Refresh:** Update file paths under **Data Source Settings** in Power Query to point to your local copies of `List of Orders.csv`, `Order Details.csv`, and `Sales Target.csv` before refreshing.
