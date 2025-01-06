# Pizza_Sales_Project
## Project Overview
This project focuses on analyzing pizza sales data to derive bussiness insight and address specific business requirement while using SQL and Power Bi to analyze and create interactive visuals that sloves the business problems.
## Table of Content
[Project Overview](#project-overview)

[Bussines Requirements](#bussines-requirements)

[Data Source](#data-source)

[Tools Used](#tools-used)

[Exploratory Data Analysis](#exploratory-data-analysis)

### Business Requirements
### KPIs
1. Total Revenue: The sum of the total price of all pizza orders. 
2. Total Sales: The sum of the quantities of all the pizza sold.
3. Average Order Value: The average amount spentper order, calculated by dividing the total revenue by the total number of orders.
4. Total Orders: The total number of orders placed
5. Average Pizza Per Orders: The average number of pizzas sold per orders, calculated by dividing the total number of pizza sold by the total number of orders.

### Exploratory Data Analysis
1. Which pizza generates the higest sales by quantity: Identify best-performing pizza to maximize revenue.
2. Which ingredients are used most frequently: Understand customer behaviour to optimize the menu.
3. What are the peak hours for sales: Identity sales patterns to optimize marketing strategies and inventory planning. 
4. Which pizza categories generates the highest revenue: Drive revenue growth through pricing and promotion.
5. Which months generates the highest revenue: Adjust inventory and promotions for seasonal trends.
6.Rank pizza by total sales using a window function: Find the top-performing pizza.
7. Monthly revenue trend: Identify seasonal patterns and high-performing products to guide future planning.
8. Pizza size popularity: Understand customer behaviour to tailor offering and marketing campaigns.

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

### Key Performance Indicator (KPIs)
---Total Revenue
```sql
SELECT
	SUM(total_price) AS Total_Revenue
FROM pizza_sale_clean;
```

---Total Sales
```sql
SELECT 
 	COUNT(quantity) AS Total_sales
FROM pizza_sale_clean;
```

---Total Orders
```sql
SELECT
 	COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sale_clean;
```

---Average Order Value
```sql
SELECT
	SUM(total_price)/
	COUNT(DISTINCT order_id) AS Average_order_Value
FROM pizza_sale_clean;
```

---Average Pizza Per Orders
```sql
SELECT
	CAST(SUM(quantity)AS DECIMAL(10,2))/
 	CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS Avg_Pizza_Per_Order
FROM pizza_sale_clean;
```


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
