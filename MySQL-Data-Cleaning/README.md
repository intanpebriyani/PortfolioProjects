### MySQL Data Cleaning and Exploratory Data Analysis (EDA)

This project focuses on cleaning and exploring a real-world dataset of global company layoffs (2020–2023).
The goal is to transform raw, messy data into a clean and reliable dataset that can be used for meaningful insights and visualization.

Learning Source: Alex The Analyst – MySQL Data Cleaning Tutorial

Dataset: Kaggle – Layoffs Dataset (2022)

Author: Intan Pebriyani

Date: October 2025

---

 **Project Objectives**

- Perform data cleaning to prepare the dataset for analysis

- Standardize inconsistent fields (company, industry, date, country)

- Handle missing and duplicate data accurately

- Conduct exploratory data analysis (EDA) to identify trends and insights

---

**Tech Stack**

- Language: MySQL

- Environment: MySQL Workbench

- Techniques Used:

  - CTEs and Window Functions (ROW_NUMBER, DENSE_RANK, etc.)

  - String and Date Manipulation (TRIM, STR_TO_DATE, SUBSTRING)

  - Data Aggregation (SUM, GROUP BY)

  - Ranking and Rolling Totals

---

**Data Cleaning Steps**

- Created a staging table to keep the raw data safe.

- Removed duplicate rows using a CTE and the ROW_NUMBER() function.

- Standardized text data:

  - Trimmed spaces in company names.

  - Unified “Crypto” industries under one label.

  - Fixed country names like United States. → United States.

- Converted date formats from text to DATE type.

- Handled NULL values — retained them to preserve data integrity for future analysis.

- Removed unnecessary rows where both layoff metrics were NULL.

---

**Exploratory Data Analysis (EDA)**

After cleaning, exploratory queries were performed to uncover insights such as:

- Date Range: 2020–2023

- Top Companies by Layoffs: Meta, Amazon, Google, Microsoft

- Top Industries Affected: Tech, Retail, and Crypto

- Top Countries by Layoffs: United States, India, and the United Kingdom

- Peak Layoff Period: Late 2022 – early 2023

- Funding Insights: Some startups raised millions before massive layoffs

- Rolling Totals: Visualized cumulative layoffs over time using window functions

---

**Key Insights**

- Global Trend: Layoffs surged during 2022–2023, especially in the tech industry.
- Industry Impact: Crypto and technology sectors faced the highest layoff numbers.
- Geographic Pattern:	The United States accounted for the majority of layoffs.
- Company Scale:	Startups and late-stage funded companies were most affected.
- Time Trend:	Layoff activity peaked in Q4 2022, reflecting post-pandemic corrections.

---

**What I Learned**

- How to apply data cleaning logic systematically in SQL

- The importance of using staging tables to protect raw data

- How to detect and remove duplicates with ROW_NUMBER()

- How to create rolling totals and use CTEs for structured analysis

- Improved understanding of data preparation for dashboards and storytelling
