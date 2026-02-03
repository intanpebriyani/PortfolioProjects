## 🍔 Swiggy Business & Customer Insights (Data Analyst Project)

### 📌 Project Overview
This project is an end-to-end SQL data analytics case study using Swiggy food order data.  
The objective is to transform raw transactional data into an analytics-ready data warehouse and generate business insights related to customer behavior, pricing, and demand trends.

All SQL queries are written in **a single SQL file**, structured with clear comment sections to represent each stage of the data pipeline (data cleaning, transformation, star schema design, and KPI analysis).

---

### 🛠 Tools & Technologies
- PostgreSQL
- SQL (DDL, DML, Window Functions, Aggregations)
- Data Warehousing (Star Schema)

---

### 📂 Project Structure
`Data/` : raw dataset or reference files  
- `Swiggy-SQL-Queries.sql` : main SQL script containing data cleaning, transformation, star schema, and KPI analysis


---

### 🔄 Data Workflow
1. **Raw Data Preparation**
   - Created staging table (`swiggy_raw`)
   - Removed invalid header rows
   - Performed record count validation

2. **Data Cleaning & Validation**
   - NULL and empty string checks
   - Duplicate detection and removal using `ROW_NUMBER()`
   - Data type conversion for dates, prices, ratings, and rating counts
  
     [Blank Empty String Check](Images/Swigy_blank-empty-string-check.png)
     [Data Validation](Images/Swiggy_data-validation.png)
     [Remove Duplicate](Images/Swiggy_remove-duplicate.png)


3. **Data Transformation**
   - Created a cleaned table (`swiggy_data`)
   - Standardized schema for analytical use

4. **Data Warehouse Design**
   - Implemented a **Star Schema** with:
     - Dimension tables: Date, Location, Restaurant, Category, Dish
     - Fact table: Swiggy Orders

5. **Business KPI Analysis**
   - Total Orders & Revenue
   - Average Price & Rating
   - Monthly, Quarterly, and Yearly trends
   - Top Cities, Restaurants, Categories, and Dishes
   - Price bucket and rating distribution analysis

---
### 📊 Dashboard Preview
Below is a preview of the dashboard built from the Swiggy data warehouse.

[Swiggy Dashboard 1](Images/Swiggy_Dashboard1.png)
[Swiggy Dashboard 2](Images/Swiggy_Dashboard2.png)

---
### 🎯 Key Insights
- Identified high-performing cities and restaurants
- Analyzed customer spending patterns
- Observed demand trends across time and weekdays
- Evaluated cuisine performance using order volume and ratings

---

### 🚀 Future Improvements
- Split SQL into modular scripts
- Optimize queries with indexing
- Automate ETL pipeline using Python
