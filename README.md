# E-Commerce-Revenue-and-Consumer-Analysis-SQL-Project

# How many users visit per day? 
```
SELECT 
DATE(created_at) AS date_accessed,
count(distinct user_id) AS daily_active_users
 FROM `bigquery-public-data.thelook_ecommerce.events` 
 GROUP BY 
 date_accessed
 ORDER BY 
 date_accessed
```
 
 # How many users visit the website per month?
 ```
SELECT 
FORMAT_DATE('%Y-%m', DATE(created_at)) AS month,
count(distinct user_id) AS monthly_active_users
 FROM `bigquery-public-data.thelook_ecommerce.events` 
 GROUP BY 
 month
 ORDER BY 
 month
```


 # Revenue Analysis: Find the total revenue by  product category and identify which one yielded the highest profitablity.

 ```
 SELECT
 p.category,
 SUM(oi.sale_price) AS total_revenue
 FROM `bigquery-public-data.thelook_ecommerce.products` p
 INNER JOIN `bigquery-public-data.thelook_ecommerce.order_items` oi ON 
 p.id = oi.id
 GROUP BY
 p.category
 ORDER BY
 total_revenue desc;
```

 # Identifying Repeat vs One time Customers
 ```
 SELECT 
 user_id,
 count(order_id) AS total_orders,
 CASE
 WHEN count(order_id) = 1 then 'one_time_customer'
 ELSE 'Repeat'
 END AS customer_type
 FROM `bigquery-public-data.thelook_ecommerce.orders`
 GROUP BY user_id
```
