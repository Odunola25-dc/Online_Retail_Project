#  Online Retail Sales Analysis (SQL Project)

This project uses SQL to analyze sales and customer behavior in an online retail dataset. It covers customer segmentation, sales performance, product popularity, revenue trends, and customer value insights.

##  Dataset
- *Source*: Online Retail (commonly found on UCI Machine Learning Repository or Kaggle)
- *Table Used*: online_retail
- *Key Columns*: InvoiceNo, Description, Quantity, UnitPrice, InvoiceDate, CustomerID, Country

##  Objectives

1. *Customer Segmentation*
   - Categorize customers based on purchase frequency (one-time, repeat, high-value).

2. *Revenue Insights*
   - Total revenue generated per segment and per country.
   - Identify top-performing countries.

3. *Product Analysis*
   - Top 10 most purchased products.
   - Country-level breakdown for top products.

4. *Monthly Sales Trend*
   - Monthly sales patterns to spot seasonal spikes and dips.

5. *Customer Lifetime Value (CLV)*
   - Total revenue per customer.
   - Top 5 customers by total spend.

6. *Product Category Performance*
   - Group product descriptions into categories (e.g., BLUE, CREAM, ROSE, etc.).
   - Analyze revenue by category.

##  Sample SQL Logic

- *Customer Segmentation*
```sql
SELECT 
  CustomerID,
  COUNT(DISTINCT InvoiceNo) AS purchase_frequency,
  CASE
    WHEN COUNT(DISTINCT InvoiceNo) = 1 THEN 'OneTime-purchase'
    WHEN COUNT(DISTINCT InvoiceNo) BETWEEN 2 AND 6 THEN 'Repeat-purchase'
    ELSE 'High-purchase'
  END AS Customer_Segmentation
FROM online_retail
GROUP BY CustomerID;

- *Top 10 Products*
SELECT 
  Description, 
  SUM(Quantity) AS total_quantity_sold
FROM online_retail
GROUP BY Description
ORDER BY total_quantity_sold DESC
LIMIT 10;

- *Revenue by Country*
SELECT 
  Country, 
  ROUND(SUM(Quantity * UnitPrice), 2) AS Total_sales_revenue
FROM online_retail
GROUP BY Country
ORDER BY Total_sales_revenue DESC;
