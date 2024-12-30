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
