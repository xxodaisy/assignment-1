# 📊 Wholesale Sales Analysis – SQL & Spreadsheet Project

## 📌 Background
This project was part of an assignment I completed before securing a job. The objective was to analyze wholesale sales data using MySQL for querying and a Spreadsheet for data visualization.

## 🔍 Project Scope

### 📥 Dataset & Tools Used

Dataset: Sample wholesale sales data

Tools: MySQL for querying & Spreadsheet (Google Sheets/Excel) for visualization

I answered several key business questions using optimized SQL queries and provided insights as a Business Intelligence Analyst.

## Questions
A. You are going to import the sql data file and insert that data into the Mysql database.

Download the sample data here: sample wholesale.sql Please import the data into your mysql database

B. Please write in document the query for each question, show the result of the query, and give your
analysis of the data. Make sure your query is the most optimized.

## 🏆 Key Business Questions & SQL Queries

### 1️⃣ Which Product is the Most Bought Each Month?

This query identifies the best-selling product for each month based on total sales.

```sql
SELECT
    `Month`,
    `Product_name`,
    `Category`,
    `Total_Sales` AS `Most_Bought_Product`
FROM (
    SELECT
        EXTRACT(MONTH FROM `Order_Date`) AS `Month`,
        `Product_name`,
        `Category`,
        SUM(`Sales`) AS `Total_Sales`,
        ROW_NUMBER() OVER(PARTITION BY EXTRACT(MONTH FROM `Order_Date`) ORDER BY SUM(`Sales`) DESC) AS `Rank`
    FROM `sales`
    GROUP BY `Month`, `Product_name`, `Category`
) ranked_sales
WHERE `Rank` = 1;
```
✅ Insight: This helps businesses understand seasonal demand and adjust inventory accordingly.

### 2️⃣ What are the Total Sales from Each City? What are the Top 3 Cities?

This query calculates total sales by city and ranks the top-performing ones.

```sql
select `City`,
SUM(`Sales`) as `Total_Sales`
from `sales`
group by `City`
order by `Total_Sales` DESC
`Limit`3
```
✅ Insight: Identifies high-performing regions, helping businesses allocate resources efficiently.

### 3️⃣ Which Product is the Top Selling in Each City?

This query determines the best-selling product for every city.

```sql
SELECT
    `Product_Name`,
    `City`,
    `Category`,
    `Total_Sales`
FROM (
    SELECT
        `Product_Name`,
        `City`,
        `Category`,
        SUM(`Sales`) AS `Total_Sales`,
        ROW_NUMBER() OVER(PARTITION BY `City` ORDER BY SUM(`Sales`) DESC) AS `Rank`
    FROM `sales`
    GROUP BY `Product_Name`, `City`, `Category`
) ranked_sales
WHERE `Rank` = 1
ORDER BY `Total_Sales` DESC;
```
✅ Insight: Helps businesses customize marketing strategies for different cities.

### 4️⃣ What is the Average Profit Per Order?

This query calculates the average profit for each order.

```sql
SELECT
    `Order_ID`,
    `Category`,
    `Average_Profit`  AS `Total_Average_Profit`
FROM (
    SELECT
        `Order_ID`,
        `Category`,
        AVG(`Profit`) AS `Average_Profit`
    FROM `sales`
    GROUP BY `Order_ID`, `Category`
) avg_profit_per_category
ORDER BY `Total_Average_Profit` DESC;
```
✅ Insight: Assists in profit margin analysis and pricing strategies.

## 📊 Data Visualization & Insights

The results from the SQL queries were visualized using Spreadsheets to present:

📌 Top-selling products per month

📌 Sales distribution by city

📌 Best-selling products per region

📌 Average profit trends

For more detail, you can read [my article](https://medium.com/@ciaamoons/archieve-an-assignment-6b6f988b7ebc) in here

Thank you!

