select * from online_sales_data;

--- Use EXTRACT(MONTH FROM order_date) for month.---
SELECT 
    EXTRACT(YEAR FROM Transaction_Date) AS year,
    EXTRACT(MONTH FROM Transaction_Date) AS month,
    COUNT(DISTINCT Transaction_ID) AS order_volume,
    SUM(Total_Revenue) AS total_revenue
FROM Online_Sales_Data
GROUP BY 
    EXTRACT(YEAR FROM Transaction_Date),
    EXTRACT(MONTH FROM Transaction_Date)
ORDER BY 
    year ASC, 
    month ASC;
    
    --- GROUP BY year/month.---
SELECT 
    DATE_FORMAT(Transaction_Date, '%Y-%m') AS Date_revenue,
    COUNT(DISTINCT Transaction_ID) AS order_volume,
    SUM(Total_Revenue) AS total_revenue
FROM Online_Sales_Data
GROUP BY Date_revenue
ORDER BY Date_revenue;

--- Use SUM() for revenue.---
SELECT
    EXTRACT(YEAR FROM Transaction_Date) AS year,
    EXTRACT(MONTH FROM Transaction_Date) AS month,
    SUM(Total_Revenue) AS total_revenue,
    COUNT(DISTINCT Transaction_ID) AS order_volume
FROM online_sales_data
GROUP BY year, month
ORDER BY year, month
LIMIT 12; 
  
-- example: COUNT(DISTINCT order_id) for volume.---

SELECT 
    EXTRACT(YEAR FROM Transaction_Date) AS year,
    EXTRACT(MONTH FROM Transaction_Date) AS month,
    SUM(Total_Revenue) AS monthly_revenue,
    COUNT(DISTINCT Transaction_ID) AS order_volume
FROM online_sales_data
GROUP BY year, month
ORDER BY year, month;

--- Use ORDER BY for sorting.---

SELECT 
    EXTRACT(YEAR FROM Transaction_Date) AS year,
    EXTRACT(MONTH FROM Transaction_Date) AS month,
    SUM(Total_Revenue) AS monthly_revenue,
    COUNT(DISTINCT Transaction_ID) AS order_volume
FROM online_sales_data
GROUP BY year, month
ORDER BY year ASC, month ASC;

--- Limit results for specific time periods.---

-- Monthly Revenue and Volume for 2024---
-- Monthly Revenue and Order Volume (Last 12 Months)
SELECT 
    EXTRACT(YEAR FROM Transaction_Date) AS year,
    EXTRACT(MONTH FROM Transaction_Date) AS month,
    SUM(Total_Revenue) AS monthly_revenue,
    COUNT(DISTINCT Transaction_ID) AS order_volume
FROM online_sales_data
WHERE Transaction_Date >= DATE_SUB(CURDATE(), INTERVAL 12 MONTH)
GROUP BY year, month
ORDER BY year ASC, month ASC;
