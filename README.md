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

## metrics used in sales and order analysis:

•	Sales revenue: This is the total amount of money generated from sales.

•	Sales growth: This is the percentage change in sales revenue from one period to the next.

•	Sales per customer: This is the average amount of money spent by each customer.

•	Sales per salesperson: This is the average amount of money generated by each salesperson.

•	Sales by product: This shows how much of each product is being sold.

•	Sales by region: This shows how much sales are generated in each region.

•	Sales by channel: This shows how much sales are generated through each sales channel.

•	Sales volume: This is the total amount of sales made in a given period.

•	Sales value: This is the total amount of revenue generated by sales in a given period.

•	Orders placed: This is the number of orders placed by customers in a given period.

•	Average order value: This is the average amount of money spent by customers on each order.

•	Customer lifetime value: This is the total amount of money that a customer is expected to spend with your business over their lifetime.

By tracking these metrics, you can get a better understanding of your sales performance and identify areas where you can improve.

I would like to analyze the sales and order dataset for the fictitious gourmet food supplier company Northwind Traders, which was created by [Maven Analytics](https://mavenanalytics.io/data-playground). 
The dataset contains information on customers, products, orders, shippers, and employees. I would like to use this data to identify trends in sales, customer behavior, and product popularity. 
This information could be used to improve the company's sales and marketing strategies.

## Steps involved to ensure good analysis: 

1. Data Cleaning and Preprocessing: This involves identifying and correcting any errors in the data, removing any duplicate or irrelevant data, and transforming the data into a format that is easy to analyze.

    * Checking for Null values
    
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
    
    * Checking for Duplicate values 
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

![dup2](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/232a8170-da6a-42dd-974b-8fd4a3c63b76)
![dup](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/e4f721ee-ec69-4d71-8d01-4af63c1b5af1)
![dup3](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/d8482395-6091-4ed5-ae9d-c4b5340732bf)
![dup4](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/c2d5809a-8bd4-4f03-ac87-82ef0046f48a)
   
Our dataset has been carefully cleaned and processed to ensure high data quality. We have taken steps to remove any missing values, ensuring that all the required information is present for each record. Additionally, we have meticulously checked for and eliminated any duplicate entries, ensuring that each entry in the dataset is unique. By addressing these issues, we can confidently state that our data is complete and free from any missing values or duplicate records.

