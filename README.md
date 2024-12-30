# Pizza_Sales_Project
## Project Overview
This project focuses on analyzing pizza sales data to derive bussiness insight and address specific business requirement while using SQL and Power Bi to analyze and create interactive visuals that sloves the business problems.
## Table of Content
[Project Overview](#project-overview)

[Bussines Requirements](#bussines-requirements)

[Data Source](#data-source)

[Tools Used](#tools-used)

### Bussines Requirements
1. Identify best-performing products to maximize revenue: Which pizza generates the higest sales by quantity.
2. Understand customer behaviour to optimize the menu: Which ingredients are used most frequently.
3. Identity sales patterns for better resource planning: What are the peak hours for sales.
4. Drive revenue growth through pricing and promotion: which pizza categories generates the highest revenue.
5. Adjust inventory and promotions for seasonal trends: Which months generates the highest revenue.
6. Find the top-performing pizza: Rank pizza by total sales using a window function.

### Power Bi visuals
1. Sales Overview Dashboard: Total sales and revenue by pizza name, Monthly sales trend.
2. Customer Behaviour Dashboard: Pizza size popularity, Sales by hour and weekday.
3. Revenue Optimization Dashboard: Revenue by pizza size and category, Contribution of top 5 pizzas to total revenue.

### Key Performance Indicator (KPIs)
1. Total sales by pizza,category and size.
2. Revenue trend by month.
3. Peak sales hours and days.
4. Ingredient usage ranking.
5. Seasonal revenue patterns.

### Data Source 
The dataset used for this analysis was obtained from Kaggle and can be accessed using this link [Download Here](https://www.kaggle.com)

### Tools Used
Structured Query Language (SQL) 
- for Data Cleaning
- for Data Transformation
- for Exploratory Data Analysis

Power Bi
- for Visualization
- for Data Modeling

Github
- for portfolio building and
- Project Documentation

### Exploratory Data Analysis
---Analyze sales performance, which pizza generate higest sales by quantity
```Sql
SELECT pizza_name,
	pizza_size,
	SUM(quantity) AS total_sales
FROM pizza_sale_clean
GROUP BY pizza_name, pizza_size
ORDER BY total_sales DESC;
```

--- Which ingredient are used most frequently
```sql
SELECT pizza_ingredient,
	COUNT(pizza_ingredient) 
FROM pizza_sale_clean
GROUP BY pizza_ingredient
ORDER BY pizza_ingredient DESC;
```

---Identify sales patterns for better resource planning,what are the peak hours for sales
```sql
SELECT pizza_name,pizza_size,pizza_category,
	EXTRACT(HOUR FROM order_time) AS sales_hour,
	SUM(total_price) AS total_sales
FROM pizza_sale_clean
GROUP BY pizza_name, pizza_size, pizza_category,sales_hour
ORDER BY total_sales DESC;
```

---Drive revenue growth through pricing and promotion,which pizza categories generatethe highest revenue.
```sql
SELECT pizza_category,
	SUM(total_price) AS revenue
FROM pizza_sale_clean
GROUP BY pizza_category
ORDER BY revenue DESC;
```

---Which month generates the highest revenue
```sql
SELECT
	CASE
	WHEN month = 1 THEN 'January'
	WHEN month = 2 THEN 'February'
	WHEN month = 3 THEN 'March'
	WHEN month = 4 THEN 'April'
	WHEN month = 5 THEN 'May'
	WHEN month = 6 THEN 'June'
	WHEN month = 7 THEN 'July'
	WHEN month = 8 THEN 'August'
	WHEN month = 9 THEN 'September'
	WHEN month = 10 THEN 'October'
	WHEN month = 11 THEN 'November'
	WHEN month = 12 THEN 'December'
	END AS month,total_revenue
FROM (
SELECT 
	EXTRACT(MONTH FROM order_date) AS month,
	SUM(total_price) AS total_revenue
FROM pizza_sale_clean
GROUP BY month) AS monthly_revenue
ORDER BY total_revenue DESC;
```

---Rank pizza by total sales using a window function.
```sql
SELECT pizza_name,
	SUM(total_price) AS total_sales,
	RANK() OVER(ORDER BY SUM(total_price)DESC) AS sales_rank
FROM pizza_sale_clean
GROUP BY pizza_name;
```
