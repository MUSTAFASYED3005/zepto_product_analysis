# zepto_product_analysis
An end-to-end data analytics project evaluating pricing strategies, discount mechanisms, inventory valuation, and stock availability across 3,700+ quick-commerce products using PostgreSQL and Power BI.
# 🛒 Zepto Data Analysis Project

## 📌 About the Project

This project is a **data analysis and business intelligence project based on Zepto product data**.

The main idea was to take a raw product dataset, clean and explore it using **SQL**, and then use **Power BI** to turn the data into meaningful visual insights.

While working on the project, I focused on questions such as:

* Which products have the highest discounts?
* Which products have a high MRP but are currently out of stock?
* Which categories have higher estimated revenue?
* Which categories offer better average discounts?
* How much does a product cost per gram?
* How is the inventory distributed based on product weight?

The project gave me practical experience in working with raw data, cleaning it, writing SQL queries, and presenting the results through a dashboard.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Understand and explore the Zepto product dataset.
* Check the dataset for missing and incorrect values.
* Clean the data before performing analysis.
* Analyze product pricing and discount percentages.
* Study stock and out-of-stock products.
* Calculate estimated revenue at the category level.
* Compare product value using price per gram.
* Analyze inventory weight across different categories.
* Create a Power BI dashboard to present the analysis visually.

---

## 🗂️ Dataset

The dataset contains information about Zepto products, including:

| Column                   | Description                               |
| ------------------------ | ----------------------------------------- |
| `sku_id`                 | Unique identifier for each product SKU    |
| `category`               | Product category                          |
| `name`                   | Product name                              |
| `mrp`                    | Maximum Retail Price                      |
| `discountPercent`        | Discount percentage                       |
| `availableQuantity`      | Available quantity                        |
| `discountedSellingPrice` | Selling price after discount              |
| `weightInGms`            | Product weight in grams                   |
| `outOfStock`             | Shows whether the product is out of stock |
| `quantity`               | Product quantity                          |

The SQL table used in the project is named `zepto`. The original SQL structure defines `sku_id` as the primary key and includes the product, pricing, inventory and stock-related fields.

---

## 🛠️ Tools & Technologies

* **SQL / PostgreSQL** – Data exploration, cleaning and analysis
* **Power BI** – Dashboard and data visualization
* **CSV** – Source dataset
* **GitHub** – Project documentation and version control

---

## 🔍 Project Workflow

The project follows a simple data analysis workflow:

```text
Raw Dataset
     ↓
Data Exploration
     ↓
Data Quality Checking
     ↓
Data Cleaning
     ↓
SQL Analysis
     ↓
Business Insights
     ↓
Power BI Dashboard
```

---

## 🧹 Data Cleaning

Before analyzing the data, I performed some basic data quality checks.

### Missing Values

The dataset was checked for NULL values in important fields such as:

* Product name
* Category
* MRP
* Discount
* Selling price
* Weight
* Available quantity
* Stock status
* Quantity

This helped identify potential issues before moving forward with the analysis.

### Zero-Price Products

Products having an MRP of `0` were identified and removed from the dataset.

```sql
DELETE FROM zepto
WHERE mrp = 0;
```

### Price Conversion

The price values were converted from **paise to rupees** by dividing them by 100.

```sql
UPDATE zepto
SET mrp = mrp / 100.0,
    discountedSellingPrice = discountedSellingPrice / 100.0;
```

These cleaning steps were included in the original SQL analysis script.

---

## 📊 SQL Analysis

After cleaning the data, I used SQL to answer several business-oriented questions.

### 1. Top Discounted Products

I identified the top 10 products based on their discount percentage.

This helps understand which products are being offered with the highest discounts.

### 2. High-MRP Products That Are Out of Stock

Products with an MRP greater than ₹300 and currently marked as out of stock were identified.

This can help highlight products that have relatively high listed prices but are unavailable.

### 3. Estimated Revenue by Category

Estimated revenue was calculated using:

```text
Discounted Selling Price × Available Quantity
```

The calculation was then grouped by category.

```sql
SUM(discountedSellingPrice * availableQuantity)
```

The SQL analysis uses this calculation to compare estimated revenue across product categories.

### 4. High-MRP Products With Low Discounts

Products with:

```text
MRP > ₹500
Discount < 10%
```

were identified to understand products that have a relatively high price but limited discounting.

### 5. Categories With Higher Average Discounts

The average discount percentage was calculated for each category, and the five categories with the highest average discount were identified.

### 6. Price Per Gram

For products weighing at least 100 grams, I calculated:

```text
Price Per Gram = Discounted Selling Price / Weight
```

This provides a simple way to compare product prices relative to their weight.

### 7. Product Weight Classification

Products were divided into three groups based on their weight:

| Weight                  | Category |
| ----------------------- | -------- |
| Less than 1000g         | Low      |
| 1000g – less than 5000g | Medium   |
| 5000g or more           | Bulk     |

This classification was created using a SQL `CASE` statement.

### 8. Total Inventory Weight

The total inventory weight was calculated for each category using:

```text
Weight × Available Quantity
```

This gives a category-level view of the amount of physical inventory represented by the available products.

---

## 📈 Power BI Dashboard

After the SQL analysis, the data was used to build a **Power BI dashboard**.

The dashboard provides a visual way to explore areas such as:

* Product categories
* Pricing
* Discounts
* Stock availability
* Inventory
* Category-level metrics

The purpose of the dashboard is to make the analysis easier to understand without having to read individual SQL queries.

> 📌 The repository includes the Power BI `.pbix` file used for the project.

---

## 💡 Key Takeaways

Working on this project helped me understand how raw data can be converted into useful information through a combination of SQL and visualization.

Some of the main analytical areas covered were:

* Discount analysis can help identify products with stronger promotional pricing.
* Stock analysis can highlight products that are currently unavailable.
* Category-level estimated revenue helps compare the potential value represented by available inventory.
* Price-per-gram provides a normalized way to compare products with different weights.
* Weight classification makes inventory analysis easier.
* Total inventory weight provides another perspective for understanding category-level stock.

These metrics are intended for **analytical purposes** and should not be treated as actual sales or profit figures unless transaction-level business data is available.

---

## 📁 Project Structure

```text
Zepto-Data-Analysis/
│
├── zepto_v2.csv
│
├── zepto_projectsql.sql
│
├── zepto project dasboard.pbix
│
└── README.md
```

### Files

**`zepto_v2.csv`**
Contains the product dataset used for the analysis.

**`zepto_projectsql.sql`**
Contains SQL queries for:

* Data exploration
* Data quality checking
* Data cleaning
* Product analysis
* Discount analysis
* Inventory analysis
* Category-level analysis

**`zepto project dasboard.pbix`**
Power BI dashboard containing the visual analysis.

**`README.md`**
Project documentation.

---

## 🚀 How to Use This Project

### Step 1 – Get the Dataset

Download or clone this repository and locate:

```text
zepto_v2.csv
```

### Step 2 – Load the Data

Import the CSV data into PostgreSQL and create the `zepto` table using the SQL script.

### Step 3 – Run the SQL Queries

Open:

```text
zepto_projectsql.sql
```

Run the queries step by step to explore, clean and analyze the data.

### Step 4 – Open the Power BI Dashboard

Open:

```text
zepto project dasboard.pbix
```

in Power BI Desktop to explore the dashboard.

---

## 📚 What I Learned

This project helped me improve my practical understanding of:

* SQL queries
* Data cleaning
* Exploratory Data Analysis
* Aggregation and grouping
* Conditional logic using `CASE`
* Business-oriented data analysis
* Inventory analysis
* Data visualization
* Power BI dashboards
* Presenting data in a simple and understandable way

---

## 🔮 Future Improvements

There are several ways this project could be extended in the future:

* Add actual sales/order data.
* Analyze sales trends over time.
* Track inventory changes over different dates.
* Identify frequently out-of-stock products.
* Add customer-level analysis if customer data is available.
* Add interactive filters and drill-downs in Power BI.
* Automate the process of updating the dashboard with new data.

---

## 👨‍💻 Author

**Syedmustafa Haider**

This project was created as a practical data analysis project to explore how **SQL and Power BI** can be used together to understand product and inventory data.

---

## ⭐ If You Found This Project Useful

If you find this project helpful or interesting, feel free to **star ⭐ the repository** and explore the SQL queries and Power BI dashboard.

