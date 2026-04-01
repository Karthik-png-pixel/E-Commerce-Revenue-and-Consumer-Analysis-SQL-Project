[bquxjob_6da5681e_19d4a700116.csv](https://github.com/user-attachments/files/26419178/bquxjob_6da5681e_19d4a700116.csv)[bquxjob_7382efa6_19d4a6904b8.csv](https://github.com/user-attachments/files/26419066/bquxjob_7382efa6_19d4a6904b8.csv)# E-Commerce-Revenue-and-Consumer-Analysis-SQL-Project
## Project Description: Utilized SQL and BigQuery database to perform revenue and consumer analysis for an E-commerce website to help identify key high performance inventory based on total sales costs, customer loyalty based on number of recurring purchases made by each customer, and website activity on a monthly and daily basis. One of the main goals of this project was to help specific gauge ways in which the e-commerce company could better its sales by foucsing on areas like weaker selling products or targeting the customer segment that aren't purchasing as much from the store. This holistic overview approach will benefit the company in the long run and retain its status as one of the best e-commerce retail wesbites.

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
<img width="1051" height="592" alt="Screenshot 2026-04-01 at 3 05 24 PM" src="https://github.com/user-attachments/assets/11aff33f-63dd-4210-bfc9-7c76280ed570" />


 
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
<img width="1710" height="1107" alt="Screenshot 2026-04-01 at 3 07 22 PM" src="https://github.com/user-attachments/assets/adcaa1ab-4416-4d89-a7b3-e9cdaa4b4578" />
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

<img width="1710" height="1107" alt="Screenshot 2026-04-01 at 3 08 42 PM" src="https://github.com/user-attachments/assets/14d3cd73-0506-4257-bbf3-5db17d10abe4" />


 # Customer Loyalty Analysis
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


<img width="1710" height="1107" alt="Screenshot 2026-04-01 at 3 11 13 PM" src="https://github.com/user-attachments/assets/8f3f8565-77fb-464d-a817-54303fda87e9" />
