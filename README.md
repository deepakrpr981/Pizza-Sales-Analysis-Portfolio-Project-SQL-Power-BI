# Pizza-Sales-Analysis-Portfolio-Project-SQL-Power-BI
![OIP](https://github.com/user-attachments/assets/378f0baa-35ec-4965-aae7-9fa63bb3486d)

The raw data for this project is presented in 4 CSV files. This data represents a year’s worth of sales for a pizza outlet, and they need to answer a few questions which will help them make important decisions to increase sales and improve their business.
The project is done in Microsoft SQL server and presented in Power BI. The data was loaded into 4 tables. This project involves the use of simple joins and sub-queries.

---
# About Data Set
The raw data for this project is presented in 4 CSV files. This data represents a year’s worth of sales for a pizza outlet, and they need to answer a few questions which will help them make important decisions to increase sales and improve their business.
The project is done in Microsoft SQL server and presented in Power BI. The data was loaded into 4 tables. This project involves the use of simple joins and sub-queries.

---
# Data source:
https://www.kaggle.com/datasets/mysarahmadbhat/pizza-place-sales

---
# QUESTIONS TO BE ANSWERED:

---
# KPIs 
1. Total Revenue (How much money did we make this year?)
2. Average Order Value
3. Total Pizzas Sold
4. Total Orders
5. Average Pizzas per Order

***
# QUESTIONS TO ANSWER
1. Daily Trends for Total Orders
2. Hourly Trend for Total Orders
3. Percentage of Sales by Pizza Category
4. Percentage of Sales by Pizza Size
5. Total Pizzas Sold by Pizza Category
6. Top 5 Pizzas by Revenue
7. Bottom 5 Pizzas by Revenue
8. Top 5 Pizza By Quantity
9. Bottom 5 Pizza By Quantity
10. Top 5 Pizza By Total Orders
11. Bottom 5 Pizza By Total Orders

---
# FINDINGS
1. Total Revenue for the year was $817,860
2. Average Order Value was $38.31
3. Total Pizzas Sold – 50,000
4. Total Orders – 21,000
5. Average Pizzas per Order – 2

# ANSWER TO QUESTIONS
1. The busiest days are Thursday (3239 orders), Friday (3538 orders) and Saturday (3158 orders). Most sales are recorded on Friday
2. Most orders are placed between 12pm to 1pm, and 5pm to 7pm
3. Classic pizza has the highest percentage sales (26.91%), followed by Supreme (25.46%), Chicken (23.96%) and Veggie (23.68%) pizzas
4. Large size pizzas record the highest sales (45.89%) followed by medium (30.49%), then small (21.77%). XL and XXL only account for 1.72% and 0.12% respectively
5. Classic Pizza accounts for the highest sales (14,888 pizzas) followed by Supreme (11,987 pizzas), Veggie (11,649 pizzas) and Chicken (11,050 pizzas)

---
# CONCLUSION
The outlet should capitalize on Large size Classic, Supreme, Veggie and Chicken pizzas.
Since XL and XXL pizzas account for such a small percentage of their sales (just 1.94%), they can safely get rid of these pizza sizes.
Even though the Brie Carre pizza is the worst seller, it recorded 490 pizzas sold. It would still be a good idea to keep it in the menu.

1. Total Revenue:
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales_1;
```
2. Average Order Value
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales_1;
```
3. Total Pizzas Sold
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales_1
``` 
4. Total Orders
```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales_1
```    
5. Average Pizzas Per Order
```sql
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales_1
```    
7. Daily Trend for Total Orders
   
```sql
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales_1
GROUP BY DATENAME(DW, order_date)
```    
8. Monthly Trend for Orders
```sql   
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales_1
GROUP BY DATENAME(MONTH, order_date)
```
9. D. % of Sales by Pizza Category
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales_1) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales_1
GROUP BY pizza_category
```
10. % of Sales by Pizza Size
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales_1) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales_1
GROUP BY pizza_size
ORDER BY pizza_size
```
11. Total Pizzas Sold by Pizza Category
```sql
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales_1
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
```
12. Top 5 Pizzas by Revenue
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales_1
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
```
13. Bottom 5 Pizzas by Revenue
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales_1
GROUP BY pizza_name
```
14. top 5 pizza by quantity
```sql
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales_1
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```
15. Bottom 5 pizza by quantity
```sql
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales_1
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```
16. top 5 pizza by Orders
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales_1
GROUP BY pizza_name
ORDER BY Total_Orders DESC
```
16. Bottom 5 pizza by Orsers
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales_1
GROUP BY pizza_name
ORDER BY Total_Orders DESC
```


---
Thanks


























