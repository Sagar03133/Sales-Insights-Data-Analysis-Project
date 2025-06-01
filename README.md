  # Sales Insights Data Analysis - Project

**1. What is the average transaction value for USD and INR?**

SELECT currency, AVG(sales_amount) AS avg_transaction_value
FROM transactions
WHERE currency IN ('INR\r', 'USD\r')
GROUP BY currency;

**2. Which products generated the highest revenue globally(Top 5)?**

SELECT product_code, SUM(sales_amount) AS total_revenue
FROM transactions
WHERE currency IN ('INR\r', 'USD\r')
GROUP BY product_code
ORDER BY total_revenue DESC
LIMIT 5;

**3. Which product had the highest sales in Chennai, considering only INR transactions?**

SELECT product_code, SUM(sales_amount) AS total_revenue
FROM transactions
WHERE market_code = 'Mark001' AND currency = 'INR\r'
GROUP BY product_code
ORDER BY total_revenue DESC
LIMIT 1;

**4. What was the largest individual transaction amount in 2020**

SELECT MAX(sales_amount) AS max_transaction
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;

**5. What is the average revenue per transaction for each market?**

SELECT AVG(sales_amount) AS avg_revenue_per_transaction
FROM transactions;

**6. Which product had the highest sales in Chennai, considering only INR transactions?**

SELECT product_code, SUM(sales_amount) AS total_revenue
FROM transactions
WHERE market_code = 'Mark001' AND currency = 'INR\r'
GROUP BY product_code
ORDER BY total_revenue DESC
LIMIT 1;

**7. Which markets (regions) generated the highest sales?**

SELECT market_code AS Market, ROUND(SUM(sales_amount), 2) AS TotalSales
FROM transactions
GROUP BY market_code
ORDER BY TotalSales DESC;

**8. Find customers who spent more than the average total spent per customer.**

SELECT customer_code, SUM(sales_amount) AS total_spent  
FROM transactions  
GROUP BY customer_code  
HAVING total_spent > ( SELECT AVG(total)  
  FROM (SELECT SUM(sales_amount) AS total FROM transactions GROUP BY customer_code) AS t);
