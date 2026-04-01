[bq-results-20260401-233052-1775086258520.csv](https://github.com/user-attachments/files/26423271/bq-results-20260401-233052-1775086258520.csv)# E-Commerce-Revenue-and-Consumer-Analysis-SQL-Project
## Project Description: Analyzed e-commerce data using SQL in BigQuery (thelook_ecommerce dataset) to evaluate customer behavior, sales performance, and website activity. Developed queries to track daily and monthly user engagement and segment customers into one-time and repeat buyers based on purchase behavior.

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

## User engagement was found to be very minimal to begin the month with most days leading to 0 website visits, however the 2nd half of the month and the subsequent months in the year 2019 steadily saw more and more user engagement albeit still at small numbers.

 
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

<img width="1710" height="1107" alt="Screenshot 2026-04-01 at 7 32 32 PM" src="https://github.com/user-attachments/assets/12e8e76e-cc5d-4a3d-8b84-4cc36d3101ff" />

### 5 year trend 
<img width="1710" height="1107" alt="Screenshot 2026-04-01 at 7 47 04 PM" src="https://github.com/user-attachments/assets/d6f22537-4151-46ff-a7cf-020d4a98d825" />



## As the e-commerce company grew and the website started gaining more popularity, the subsequent years yielded higher monthly activity on its website, reaching consistently in the hundreds at its peak. This marked a significant and notable uptick in overall engagement from its early days in 2019 when user activity was largely in the single digits.






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
