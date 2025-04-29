# Sales Data SQL Database

## Overview
This repository contains SQL scripts for creating and querying a sales database. The database is designed to track sales transactions across different categories, locations, and customers, providing insights through various analytical queries.

## Database Structure

### Database
- `sales_data_1`: Main database containing sales-related information

### Tables
- `sales_data_1`: Main table storing individual sales transactions with the following columns:
  - `OrderID`: Unique identifier for each order
  - `Amount`: Sale amount
  - `Profit`: Profit from the sale
  - `Quantity`: Number of items sold
  - `Category`: Product category
  - `SubCategory`: Product subcategory
  - `PaymentMode`: Method of payment
  - `OrderDate`: Date of the order
  - `CustomerName`: Name of the customer
  - `City`: City where the sale occurred
  - `State`: State where the sale occurred
  - `YearMonth`: Month and year of the sale (format: YYYY-MM)

## Included Queries

### Category Sales Analysis
```sql
SELECT Category, SUM(Amount) AS Total_Sales
FROM sales
GROUP BY Category
ORDER BY Total_Sales DESC;
```
This query shows total sales amount by product category, sorted from highest to lowest sales.

### Top 5 Most Profitable States
```sql
SELECT State, SUM(Profit) AS Total_Profit
FROM sales
GROUP BY State
ORDER BY Total_Profit DESC
LIMIT 5;
```
This query identifies the top 5 states by total profit.

### High-Performing Cities
```sql
SELECT City, SUM(Profit) AS City_Profit
FROM sales
GROUP BY City
HAVING City_Profit > (SELECT AVG(Profit) FROM sales);
```
This query lists cities with above-average profit performance.

### Views

The database includes a predefined view for quick access to category performance metrics:

```sql
CREATE VIEW category_performance AS
SELECT Category, SUM(Amount) AS Total_Sales, SUM(Profit) AS Total_Profit, AVG(Quantity) AS Avg_Quantity
FROM sales
GROUP BY Category;
```

## Setup Instructions

1. Import the SQL script into your preferred database management system
2. Execute the script to create the database and table structure
3. Import your sales data into the `sales_data_1` table
4. Run the included queries to analyze your sales data

## Notes

- There appears to be a discrepancy in the database/table naming. The queries reference a `sales` table, but the table created is named `sales_data_1`.
- The script checks for indexes on the Sales table using `SHOW INDEX FROM Sales`

## Further Development

Potential improvements:
- Add indexes for frequently queried columns
- Create additional views for common analytics scenarios
- Implement stored procedures for complex reporting needs
- Establish foreign key relationships if expanding to multiple tables
