# Northwind Traders

## Introduction:

Sales and order analysis is the process of collecting, analyzing, and interpreting data about sales and orders to identify trends and patterns. This data can be used to make better decisions about pricing, product development, marketing, and sales operations.
However, it can also involve more complex statistical methods. Either way, the goal is to gain insights that will help boost sales.

## Benefits of sales and order analysis:

•	Identify trends and patterns

•	Improve sales performance

•	Increase customer satisfaction

•	Reduce costs

•	Identify top-performing products and services

•	Identify underperforming products and services

•	Find new sales and market opportunities

•	Forecast future sales

•	Improve sales team performance

•	Make better pricing decisions

•	Develop more effective marketing campaigns

•	Improve inventory management

•	Understand customer needs

•	Make better business decisions

I would like to analyze the sales and order dataset for the fictitious gourmet food supplier company Northwind Traders, which was created by [Maven Analytics](https://mavenanalytics.io/data-playground). 
The dataset contains information on customers, products, orders, shippers, and employees. I would like to use this data to identify trends in sales, customer behavior, and product popularity. 
This information could be used to improve the company's sales and marketing strategies.

## Steps involved to ensure good analysis: 

1. Data Cleaning and Preprocessing: This involves identifying and correcting any errors in the data, removing any duplicate or irrelevant data, and transforming the data into a format that is easy to analyze.

    * Checking for Null values
    * Checking for Duplicate values
    * Check data types
    * Standardize and transform data
    * Handle outliers
    * Validate data integrity
    * Perform data quality checks 
    
```sql
    -- Checking for null values
SELECT COUNT(*) 
FROM orders 
WHERE orderID IS NULL;
SELECT COUNT(*) 
FROM order_details 
WHERE orderID IS NULL;
SELECT COUNT(*) 
FROM customers 
WHERE customerID IS NULL;
SELECT COUNT(*) 
FROM products 
WHERE productID IS NULL;
SELECT COUNT(*) 
FROM categories 
WHERE categoryID IS NULL;
SELECT COUNT(*) 
FROM employees 
WHERE employeeID IS NULL;
SELECT COUNT(*) 
FROM shippers 
WHERE shipperID IS NULL;
```
 Output:
 
![no null](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/5c05bf37-2ed7-4eb4-a7de-41ff233d3842)
    
-------------------------------------------------------------------------
   
```sql
-- Checking for duplicate values
SELECT COUNT(*) 
FROM orders;

SELECT COUNT(*)
FROM (SELECT DISTINCT orderID, customerID,employeeID,orderDate
                    ,requiredDate,shippedDate,shipperID,freight
       FROM orders) AS unique_orders;

SELECT COUNT(*) 
FROM categories;

SELECT COUNT(*)
FROM (SELECT DISTINCT categoryID, categoryName,description
       FROM categories) AS unique_categories;

SELECT COUNT(*) 
FROM customers;

SELECT COUNT(*)
FROM (SELECT DISTINCT customerID,companyName,contactName,contactTitle,city,country
       FROM customers) AS unique_customers;	 
	   
SELECT COUNT(*) 
FROM employees;

SELECT COUNT(*)
FROM (SELECT DISTINCT  employeeID,employeeName,title,city,country,reportsTo
       FROM employees) AS unique_employees;	 

SELECT COUNT(*) 
FROM order_details;

SELECT COUNT(*)
FROM (SELECT DISTINCT  orderID,productID,unitPrice,quantity,discount
       FROM order_details) AS unique_order_details;	 

SELECT COUNT(*) 
FROM products;

SELECT COUNT(*)
FROM (SELECT DISTINCT productID,productName,quantityPerUnit,unitPrice,discontinued,categoryID  
       FROM products) AS unique_products;	 

SELECT COUNT(*) 
FROM shippers;

SELECT COUNT(*)
FROM (SELECT DISTINCT shipperID,companyName 
       FROM shippers) AS unique_shippers;
```
Output:

| Customers Table      | Employees Table      | Order_details Table  |
|-------------- |--------------|--------------|
| ![duplicate customers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/c3b3e951-bc51-4c2e-8f6d-7cab1d6ec608)| ![duplicate employees](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/22e2a3f5-ddb6-4340-aace-28d05783ad34)| ![duplicate order details](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/645db162-62dd-4d56-92a5-dcac56901e27) | 

 Orders table     |Products Table     | Shippers Table     | Categories Table      |
|--------------|--------------|--------------|--------------|
|![duplicate orders](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/e18cbcd2-a798-4660-be93-861153fd1b04)|![duplicate products](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/d72846a5-2f3a-4f26-88c0-ac8b80711ffb)|![duplicate shippers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/83c3f45e-bc84-447a-906f-1e4db5c28130)|![duplicate categories ](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/8d164e7f-962b-4ae1-a759-b4531b274959)|
   
Hint: Our dataset has been carefully cleaned and processed to ensure high data quality. We have taken steps to remove any missing values, ensuring that all the required information is present for each record. Additionally, we have meticulously checked for and eliminated any duplicate entries, ensuring that each entry in the dataset is unique. By addressing these issues, we can confidently state that our data is complete and free from any missing values or duplicate records.

------

```sql
-- Checking for Datatypes	   
SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'categories';
	   
SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'customers';

SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'employees';

SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'order_details';

SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'orders';

SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'products';

SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'shippers';
```
Output:

![datatype order details](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/d069b2af-0347-4fac-b287-c15a5c178ce1)
![datatype orders](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/862f51cd-47ca-4f71-8f51-3682eaa6004d)
![datatype products](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/c62faf9e-2037-4e9d-9ec9-541820d31298)
![datatype shippers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/dc8a000f-ef1b-459e-ba56-bcc2524a48d9)
![datatype categories](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/a8c3e4e9-ba06-4edb-9dea-9efc967d87ab)
![datatype customers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/93a196d4-442c-4dcb-b182-84e765362836)
![datatype employees](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/2596a8fa-6c75-4c8d-9d08-d16e97645f0c)











