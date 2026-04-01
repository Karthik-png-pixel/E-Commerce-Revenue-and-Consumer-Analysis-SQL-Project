[bquxjob_7382efa6_19d4a6904b8.csv](https://github.com/user-attachments/files/26419066/bquxjob_7382efa6_19d4a6904b8.csv)# E-Commerce-Revenue-and-Consumer-Analysis-SQL-Project
## Project Description: 

# How many users visit the website daily? 
```
SELECT 
DATE(created_at) AS date_accessed,
count(distinct user_id) AS daily_active_users
 FROM `bigquery-public-data.thelook_ecommerce.events` 
 GROUP BY 
 date_accessed
 ORDER BY 
 date_accessed
Limit 30;
```
[Uploading bquxjob_7382efa6_19d4a6date_accessed,daily_active_users
2019-01-02,0
2019-01-03,0
2019-01-04,0
2019-01-05,0
2019-01-06,0
2019-01-07,0
2019-01-08,0
2019-01-09,1
2019-01-10,0
2019-01-11,0
2019-01-12,0
2019-01-13,0
2019-01-14,1
2019-01-15,0
2019-01-16,0
2019-01-17,0
2019-01-18,1
2019-01-19,0
2019-01-20,0
2019-01-21,1
2019-01-22,0
2019-01-23,0
2019-01-24,0
2019-01-25,0
2019-01-26,1
2019-01-27,1
2019-01-28,1
2019-01-29,0
2019-01-30,1
2019-01-31,1904b8.csv…]()


 
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
