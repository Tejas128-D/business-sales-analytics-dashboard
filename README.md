# # # 📊 Business Sales Analytics Dashboard | SQL + Power BI

## Author

**Tejas R**
Data Analyst | Power BI | SQL

---

## Project Overview

This project focuses on analyzing sales data for **AtliQ Hardware**, a computer hardware manufacturer operating in multiple markets. The objective is to generate meaningful sales insights that help stakeholders make **data-driven decisions**.

The project demonstrates an **end-to-end data analytics workflow**, including:

* Data discovery
* SQL data analysis
* Data cleaning
* ETL processes
* Data modeling
* Building an interactive **Power BI dashboard**

---

## Problem Statement

AtliQ Hardware faced several challenges in understanding their sales performance:

* Sales reporting was manual and slow.
* Decision-making relied on verbal updates instead of real data.
* There was no centralized system to monitor sales performance across markets.

The goal of this project is to create an **interactive dashboard** that provides clear insights into sales performance and business trends.

---

## Project Planning (AIMS Grid)

### Purpose

Identify business problems in sales reporting and create a solution using data analytics.

### Stakeholders

* Marketing Team
* Sales Team
* IT Team
* Data Analytics Team

### End Result

An **interactive Power BI dashboard** that provides real-time sales insights.

### Success Criteria

* Faster reporting
* Improved business decision-making
* Better visibility of sales trends

---

## Data Source

The dataset used in this project is stored in a **MySQL database dump file**.

Database tables include:

* **customers** – customer information
* **products** – product details
* **transactions** – sales transaction records
* **markets** – market location data
* **date** – date dimension table

The **transactions table** acts as the main fact table containing sales information such as:

* product_code
* customer_code
* sales_amount
* currency
* order_date

---

## Data Analysis Using SQL

### Show all customer records

```sql
SELECT * FROM customers;
```

### Show total number of customers

```sql
SELECT COUNT(*) FROM customers;
```

### Show transactions for Chennai market

```sql
SELECT * 
FROM transactions
WHERE market_code = 'Mark001';
```

### Show distinct product codes sold in Chennai

```sql
SELECT DISTINCT product_code
FROM transactions
WHERE market_code = 'Mark001';
```

### Show transactions where currency is USD

```sql
SELECT *
FROM transactions
WHERE currency = 'USD';
```

### Show transactions in 2020

```sql
SELECT transactions.*, date.*
FROM transactions
INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year = 2020;
```

### Show total revenue in 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year = 2020
AND (transactions.currency = "INR\r" OR transactions.currency = "USD\r");
```

### Show revenue in January 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year = 2020
AND date.month_name = "January"
AND (transactions.currency = "INR\r" OR transactions.currency = "USD\r");
```

### Show revenue from Chennai in 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year = 2020
AND transactions.market_code = "Mark001";
```

---

## ETL Process in Power BI

Power BI was connected to the MySQL database to perform **ETL (Extract, Transform, Load)** operations.

### Data Loading

Tables were imported directly from the MySQL database.

### Data Modeling

A **Star Schema model** was created:

* Transactions → Fact Table
* Customers, Products, Markets, Date → Dimension Tables

### Data Cleaning

Several data issues were addressed:

* Removed markets such as **New York and Paris**
* Filtered transactions with **sales amount ≤ 0**
* Removed duplicate currency values caused by hidden characters

---

## Currency Normalization

Sales transactions existed in **USD and INR** currencies.

To standardize revenue calculations, USD values were converted into INR using a fixed exchange rate.

Power Query formula:

```
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount])
```

---

## Power BI Dashboard

An interactive **Sales Insights Dashboard** was developed in Power BI.

### Key Metrics

* Total Revenue
* Total Sales Quantity
* Revenue by Market
* Revenue by Customer
* Revenue Trend Over Time

### Dashboard Features

**KPI Cards**
Display total revenue and sales quantity.

**Market Analysis**
Revenue contribution by different markets.

**Customer Analysis**
Top performing customers.

**Product Analysis**
Best selling products.

**Time Analysis**
Year and month filters to analyze sales trends.

### Interactivity

The dashboard supports **cross-filtering**, allowing users to click on a market or year to dynamically update all visualizations.

---

## Tools & Technologies

* SQL (MySQL)
* Power BI
* Power Query
* DAX
* Data Modeling
* ETL Processes

---

## Project Outcome

The dashboard provides stakeholders with:

* Clear insights into **sales performance**
* Identification of **top customers and products**
* Monitoring of **revenue trends**
* Ability to make **data-driven decisions**

This project demonstrates the **complete lifecycle of a real-world data analytics project**, from raw data exploration to building an interactive business intelligence dashboard.
