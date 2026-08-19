# Walmart Sales Data Analysis

An end-to-end data analysis project that cleans raw Walmart sales data in Python, loads it into a SQL database (MySQL and PostgreSQL), and answers a set of business questions using SQL.

## Project Overview

This project walks through a typical data analyst workflow:

1. **Explore & clean** raw transactional data using Python (Pandas) in a Jupyter Notebook.
2. **Load** the cleaned dataset into MySQL and PostgreSQL databases.
3. **Query** the data with SQL to answer real-world Walmart business questions covering sales, payments, ratings, profit, and revenue trends.

## Repository Contents

| File | Description |
|---|---|
| `project.ipynb` | Jupyter notebook containing the full data exploration, cleaning, and database-loading workflow. |
| `MySQL_Queries.sql` | SQL queries (written for MySQL) that answer each business problem. |
| `Walmart_Business_Problems.pdf` | Write-up of the nine business questions this project answers, with the purpose behind each one. |
| `walmart_clean_data.csv` | Cleaned dataset exported from the notebook (generated after running the cleaning steps). |

## Dataset

The raw dataset (`Walmart.csv`) contains Walmart sales transactions with the following fields:

| Column | Description |
|---|---|
| `invoice_id` | Unique transaction identifier |
| `Branch` | Store branch code |
| `City` | City where the branch is located |
| `category` | Product category |
| `unit_price` | Price per unit (originally formatted as currency, e.g. `$74.69`) |
| `quantity` | Number of units sold |
| `date` | Transaction date |
| `time` | Transaction time |
| `payment_method` | Payment method used (Cash, Credit card, Ewallet) |
| `rating` | Customer rating for the transaction |
| `profit_margin` | Profit margin for the transaction |

## Data Cleaning Steps (in `project.ipynb`)

1. Loaded the raw CSV with `pandas.read_csv`, ignoring encoding errors.
2. Removed duplicate rows.
3. Dropped rows with missing values.
4. Converted `unit_price` from a currency string (e.g. `$74.69`) to a float.
5. Added a computed `total` column (`unit_price * quantity`).
6. Standardized all column names to lowercase.
7. Exported the cleaned data to `walmart_clean_data.csv`.
8. Loaded the cleaned data into a `walmart` table in both **MySQL** (via `SQLAlchemy` + `PyMySQL`) and **PostgreSQL** (via `SQLAlchemy` + `psycopg2`).

## Business Questions Answered (SQL)

The SQL queries in `MySQL_Queries.sql` answer the following:

1. **Payment method analysis** — transactions and quantity sold per payment method.
2. **Top category per branch** — highest-rated product category in each branch.
3. **Busiest day per branch** — day of the week with the most transactions per branch.
4. **Quantity sold by payment method** — total items sold per payment type.
5. **Category ratings by city** — min, max, and average rating per category, per city.
6. **Profit by category** — total profit per category, ranked highest to lowest.
7. **Preferred payment method per branch** — most frequently used payment method at each branch.
8. **Sales by shift** — transaction volume split into Morning, Afternoon, and Evening shifts per branch.
9. **Revenue decline year-over-year** — the 5 branches with the largest revenue decrease from 2022 to 2023.

See `Walmart_Business_Problems.pdf` for the full business context and purpose behind each question.

## Tech Stack

- **Python**: `pandas`, `sqlalchemy`, `pymysql`, `psycopg2`
- **Databases**: MySQL, PostgreSQL
- **SQL techniques used**: `GROUP BY`, window functions (`RANK() OVER (PARTITION BY ...)`), CTEs, `CASE` statements, date functions (`STR_TO_DATE`, `DAYNAME`, `YEAR`), subqueries


