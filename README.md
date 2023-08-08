# SQL-Maven-Anaylytics-Pizza-Sales
In this project, I am working with Maven Analytics Pizza dataset using MySQL to answer the following questions: 

1. Total Revenue?
2. AVG order value?
3. Total Pizzas Sold?
4. Total Orders?
5. AVG Pizzas Per Order?
6. Daily Trend for Total Orders?
7. Monthly Trend for Total orders?
8. PCT % of sales by Pizza categories
9. PCT % of Pizzas sold by Pizza Size
10. Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
11. Bottom 5 Pizzas
12. Top 5 Pizzas by Quantity by Orders

--------------------------------------------------

PIZZA SALES SQL QUERIES

A.	KPI’s

1.	Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales





	
2.	Average Order Value:
SELECT SUM(total_price) / COUNT(DISTINCT order_id) as Avg_Order_Value FROM pizza_sales





3.	Total Pizzas Sold:
SELECT SUM(quantity) AS Total_Pizza_Sold FROM pizza_sales






4.	Total Orders:
SELECT COUNT(DISTINCT order_id) AS Total_orders FROM pizza_sales
  





5.	Average Pizzas Per Order:
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_Per_Order FROM pizza_sales













6.	Daily Trend for Total Orders:
SELECT DAYNAME(STR_TO_DATE(order_date, '%m/%d/%Y')) AS order_day, COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
WHERE STR_TO_DATE(order_date, '%m/%d/%Y') IS NOT NULL
GROUP BY DAYNAME(STR_TO_DATE(order_date, '%m/%d/%Y'))








7.	Monthly Trend for Total Orders:
SELECT DATE_FORMAT(STR_TO_DATE(order_date, '%m/%d/%Y'), '%M') AS Month_Name, COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY DATE_FORMAT(STR_TO_DATE(order_date, '%m/%d/%Y'), '%M')
ORDER BY Total_orders DESC











8.	Percentage of Sales by Pizza Category:
SELECT pizza_category, SUM(total_price) as Total_Sales, SUM(total_price) * 100 / (SELECT sum(total_price) from pizza_sales WHERE MONTH(STR_TO_DATE(order_date, '%m/%d/%Y')) = 1) AS PCT
FROM pizza_sales 
WHERE MONTH(STR_TO_DATE(order_date, '%m/%d/%Y')) = 1
GROUP BY pizza_category;
















9.	Percentage of Pizzas Sold by Pizza Size
SELECT pizza_size, SUM(total_price) AS DECIMAL(10,2)) as Total_Sales, CAST(sum(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales 
GROUP BY pizza_size;








10.	Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;








11.	Bottom 5 Pizzas
SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
LIMIT 5;








12.	Top 5 Pizzas by Quantity by Orders:
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;

