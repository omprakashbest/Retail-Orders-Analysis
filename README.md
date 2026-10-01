# 📊 Retail Orders Analysis — ETL & SQL Analytics

An end-to-end **Retail Orders Data Analysis** project that demonstrates the complete data analytics workflow — from automated data extraction and cleaning with Python to database integration and business analysis using advanced SQL.

The project uses a retail orders dataset to analyze **sales performance, product rankings, regional performance, year-over-year growth, category trends, and sub-category growth**.

---

## 🎯 Project Objective

The objective of this project is to transform raw retail order data into a structured dataset and use SQL-based analysis to answer important business questions such as:

- Which products generate the highest sales?
- Which products perform best within each region?
- How did monthly sales change between 2022 and 2023?
- Which month generated the highest sales for each category?
- Which sub-category experienced the highest sales growth from 2022 to 2023?

---

## 🔄 Project Workflow

```text
Kaggle Dataset
      ↓
Kaggle API
      ↓
Data Extraction
      ↓
Python + Pandas
      ↓
Data Cleaning & Transformation
      ↓
Feature Engineering
      ↓
MySQL Database
      ↓
Advanced SQL Analysis
      ↓
Business Insights
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **Python** | ETL and data processing |
| **Pandas** | Data cleaning and transformation |
| **MySQL** | Data storage and analysis |
| **SQLAlchemy** | Database connectivity |
| **PyODBC** | MySQL/database connection |
| **Kaggle API** | Automated dataset extraction |
| **Jupyter Notebook** | ETL workflow and analysis |
| **Git & GitHub** | Version control and project management |

The GitHub repository documents the same ETL stack, including Python, Pandas, MySQL, SQLAlchemy/PyODBC, Kaggle API, and Jupyter Notebook.

---

## 📂 Dataset

The project uses a **Retail Orders Dataset from Kaggle**.

The dataset contains order-level information covering:

- Order ID
- Order Date
- Ship Mode
- Customer Segment
- Country
- City
- State
- Postal Code
- Region
- Category
- Sub-Category
- Product ID
- Quantity
- Discount
- Sale Price
- Profit

The SQL database table is structured around these order, geographic, product, quantity, discount, sales, and profit fields.

---

## ⚙️ ETL Pipeline

### 1. Extract

The dataset is extracted programmatically using the **Kaggle API**, reducing the need for manual dataset downloads.

### 2. Transform

Python and Pandas are used to:

- Load the raw dataset
- Inspect the data
- Handle missing values
- Correct data types
- Standardize column names
- Clean the dataset
- Prepare the data for database analysis
- Create/prepare financial metrics such as discount, sale price, and profit

### 3. Load

The processed dataset is loaded into **MySQL** for structured querying and business analysis.

The SQL schema defines an `orders_data` table containing order, date, geographic, product, quantity, discount, sales, and profit fields.

---

# 📈 SQL Analysis & KPIs

The project uses **CTEs, aggregate functions, CASE statements, GROUP BY, ORDER BY, and Window Functions** to answer business questions.

### 1. Top 10 Revenue-Generating Products

Identifies the **top 10 products by total sales**.

```sql
SELECT product_id, SUM(sale_price) AS sales
FROM orders_data
GROUP BY product_id
ORDER BY sales DESC
LIMIT 10;
```

This helps identify products contributing the most sales revenue.

---

### 2. Top 5 Products by Region

Uses `ROW_NUMBER()` with `PARTITION BY` to rank products within each region and identify the **top 5 products in every region**.

```sql
ROW_NUMBER() OVER(
    PARTITION BY region
    ORDER BY sales DESC
)
```

This provides a regional view of product performance.

---

### 3. Year-over-Year Sales Comparison

Compares monthly sales between **2022 and 2023**.

The analysis separates sales by year and compares the corresponding months to identify changes in sales performance.

```text
January 2022  → January 2023
February 2022 → February 2023
March 2022    → March 2023
...
```

This helps identify monthly sales growth and changes in revenue patterns.

---

### 4. Highest-Sales Month by Category

Calculates monthly sales for each category and uses `ROW_NUMBER()` to identify the **highest-sales month for every category**.

```sql
ROW_NUMBER() OVER(
    PARTITION BY category
    ORDER BY sales DESC
)
```

This helps identify seasonal or peak sales periods across product categories.

---

### 5. Sub-Category Sales Growth

Compares **2022 vs. 2023 sales** for each sub-category and calculates the percentage growth.

```sql
(sales_2023 - sales_2022) * 100 / sales_2022
```

The analysis then identifies the sub-category with the highest growth rate.

> **Note:** The SQL comment refers to "growth by profit", but the implemented calculation uses `sale_price` and therefore measures **sales growth**, not profit growth.

---

# 💡 Business Impact

The analysis can support retail decision-making by providing visibility into:

- **Product Performance** — identify high-revenue products.
- **Regional Performance** — understand which products perform strongly across regions.
- **Sales Growth** — track changes in sales between years and across months.
- **Category Planning** — identify peak sales periods for categories.
- **Sub-Category Growth** — identify rapidly growing product segments.
- **Inventory Planning** — use product and category demand patterns to support inventory decisions.
- **Sales Strategy** — use regional and product-level performance to inform sales planning.

---

# 🗄️ Database Structure

The cleaned dataset is stored in MySQL as:

```text
orders
└── orders_data
    ├── order_id
    ├── order_date
    ├── ship_mode
    ├── segment
    ├── country
    ├── city
    ├── state
    ├── postal_code
    ├── region
    ├── category
    ├── sub_category
    ├── product_id
    ├── quantity
    ├── discount
    ├── sale_price
    └── profit
```

The table definition is implemented directly in the project's SQL file.

---

# 📁 Project Structure

```text
Retail-Orders-Analysis/
│
├── Orders.ipynb
│   └── ETL pipeline
│       ├── Data extraction
│       ├── Data cleaning
│       ├── Transformation
│       └── Database loading
│
├── Retails_analysis.sql
│   └── SQL analytics
│       ├── Product rankings
│       ├── Regional analysis
│       ├── YoY sales comparison
│       ├── Category analysis
│       └── Sub-category growth
│
├── orders.csv
│   └── Retail orders dataset
│
├── orders.csv.zip
│   └── Compressed dataset
│
└── README.md
```

These files are present in the GitHub repository.

---

# 🚀 How to Run the Project

## 1. Clone the Repository

```bash
git clone https://github.com/omprakashbest/Retail-Orders-Analysis.git
cd Retail-Orders-Analysis
```

## 2. Install Dependencies

```bash
pip install pandas sqlalchemy pyodbc kaggle
```

## 3. Configure Kaggle API

Place your Kaggle API credentials:

```text
kaggle.json
```

in the appropriate Kaggle configuration location so the notebook can access the dataset.

## 4. Run the ETL Pipeline

Open:

```text
Orders.ipynb
```

in Jupyter Notebook and execute the notebook to perform the extraction, cleaning, transformation, and database-loading steps.

## 5. Configure MySQL

Create the database and table using:

```sql
CREATE DATABASE orders;
USE orders;
```

Then execute the table definition from:

```text
Retails_analysis.sql
```

## 6. Run SQL Analysis

Open:

```text
Retails_analysis.sql
```

in MySQL Workbench and execute the analytical queries.

---

# 📊 Skills Demonstrated

### Data Analytics
- Data Cleaning
- Data Transformation
- Exploratory Analysis
- KPI Analysis
- Business Analysis

### Python
- Pandas
- ETL Automation
- Data Processing
- Feature Engineering

### SQL
- Aggregations
- GROUP BY
- CASE WHEN
- CTEs
- Window Functions
- ROW_NUMBER()
- Date Functions
- Ranking
- Year-over-Year Analysis

### Data Engineering
- API-based Data Extraction
- ETL Pipeline Development
- Database Integration
- MySQL Data Loading

---

```text
Extract → Clean → Transform → Load → Analyze → Generate Insights
```

It combines **Python-based ETL, Pandas data processing, MySQL database management, and advanced SQL analytics** to convert raw retail order data into business-focused sales insights.
