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

 Orders table     |Products Table     | Shippers Table     | Categories Table      |
|--------------|--------------|--------------|--------------|
![datatype orders](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/862f51cd-47ca-4f71-8f51-3682eaa6004d)|![datatype products](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/c62faf9e-2037-4e9d-9ec9-541820d31298)|![datatype shippers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/dc8a000f-ef1b-459e-ba56-bcc2524a48d9)|![datatype categories](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/a8c3e4e9-ba06-4edb-9dea-9efc967d87ab)|    

 Orders_details table     |Customers Table     | Employees Table 
|--------------|--------------|--------------|
![datatype order details](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/d069b2af-0347-4fac-b287-c15a5c178ce1)|![datatype customers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/93a196d4-442c-4dcb-b182-84e765362836)|![datatype employees](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/2596a8fa-6c75-4c8d-9d08-d16e97645f0c)|

Hint:
Our dataset has been carefully structured and validated to ensure that each column contains data in the appropriate format. We have taken the necessary steps to verify that all data types are correctly assigned to their respective columns. By ensuring the data is in its correct data type, we can confidently analyze and interpret the dataset accurately.

------------------

```sql
-- Checking for outliers
SELECT o.orderID, o.customerID, o.orderDate, od.quantity, od.unitPrice, o.freight
FROM orders o
INNER JOIN order_details od 
ON o.orderID = od.orderID
WHERE o.freight > (SELECT AVG(freight) + 3 * STDEV(freight) 
                   FROM orders)
ORDER BY o.customerID 
```
Output:
|orderID     |customerID| orderDate  | quantity |unitPrice|freight|
|------------|----------|------------|----------|---------|--------------|
10430|	ERNSH|	2014-01-30|	45|	31.2000007629395|	458.779998779297
10430|	ERNSH|	2014-01-30|	50|	8|	                458.779998779297
10430|	ERNSH|	2014-01-30|	30|	30.3999996185303|	458.779998779297
10430|	ERNSH|	2014-01-30|	70|	44|	                458.779998779297
10514|	ERNSH|	2014-04-22|	39|	81|	                789.950012207031
10514|	ERNSH|	2014-04-22|	35|	45.5999984741211|	789.950012207031
10514|	ERNSH|	2014-04-22|	70|	38|	                789.950012207031
10514|	ERNSH|	2014-04-22|	39|	21.0499992370605|	789.950012207031
10514|	ERNSH|	2014-04-22|	50|	7.75|	                789.950012207031
10633|	ERNSH|	2014-08-15|	36|	38|	                477.899993896484
10633|	ERNSH|	2014-08-15|	13|	6|	                477.899993896484
10633|	ERNSH|	2014-08-15|	35|	31.2299995422363|	477.899993896484
10633|	ERNSH|	2014-08-15|	80|	49.2999992370605|	477.899993896484
11017|	ERNSH|	2015-04-13|	25|	10|	                754.260009765625
11017|	ERNSH|	2015-04-13|	110|	55|	                754.260009765625
11017|	ERNSH|	2015-04-13|	30|	15|	                754.260009765625
10634|	FOLIG|	2014-08-15|	35|	30|	                487.380004882813
10634|	FOLIG|	2014-08-15|	50|	62.5|	                487.380004882813
10634|	FOLIG|	2014-08-15|	15|	53|	                487.380004882813
10634|	FOLIG|	2014-08-15|	2|	7.75|	                487.380004882813
10816|	GREAL|	2015-01-06|	30|	263.5|	                719.780029296875
10816|	GREAL|	2015-01-06|	20|	49.2999992370605|	719.780029296875
10897|	HUNGO|	2015-02-19|	80|	123.790000915527|	603.539978027344
10897|	HUNGO|	2015-02-19|	36|	25.8899993896484|	603.539978027344
10912|	HUNGO|	2015-02-26|	40|	21|	                580.909973144531
10912|	HUNGO|	2015-02-26|	60|	123.790000915527|	580.909973144531
10372|	QUEEN|	2013-12-04|	12|	64.8000030517578|	890.780029296875
10372|	QUEEN|	2013-12-04|	40|	210.800003051758|	890.780029296875
10372|	QUEEN|	2013-12-04|	70|	27.2000007629395|	890.780029296875
10372|	QUEEN|	2013-12-04|	42|	27.7999992370605|	890.780029296875
10691|	QUICK|	2014-10-03|	30|	18|	                810.049987792969
10691|	QUICK|	2014-10-03|	40|	123.790000915527|	810.049987792969
10691|	QUICK|	2014-10-03|	40|	46|	                810.049987792969
10691|	QUICK|	2014-10-03|	24|	19.4500007629395|	810.049987792969
10691|	QUICK|	2014-10-03|	48|	49.2999992370605|	810.049987792969
10540|	QUICK|	2014-05-19|	60|	10|	                1007.64001464844
10540|	QUICK|	2014-05-19|	40|	31.2299995422363|	1007.64001464844
10540|	QUICK|	2014-05-19|	30|	263.5|	                1007.64001464844
10540|	QUICK|	2014-05-19|	35|	12.5|	                1007.64001464844
10479|	RATTC|	2014-03-19|	30|	210.800003051758|	708.950012207031
10479|	RATTC|	2014-03-19|	28|	26.2000007629395|	708.950012207031
10479|	RATTC|	2014-03-19|	60|	44|	                708.950012207031
10479|	RATTC|	2014-03-19|	30|	26.6000003814697|	708.950012207031
10612|	SAVEA|	2014-07-28|	70|	31|	                544.080017089844
10612|	SAVEA|	2014-07-28|	55|	19|	                544.080017089844
10612|	SAVEA|	2014-07-28|	18|	20|	                544.080017089844
10612|	SAVEA|	2014-07-28|	40|	34|	                544.080017089844
10612|	SAVEA|	2014-07-28|	80|	18|	                544.080017089844
10847|	SAVEA|	2015-01-22|	80|	18|	                487.570007324219
10847|	SAVEA|	2015-01-22|	12|	9.19999980926514|	487.570007324219
10847|	SAVEA|	2015-01-22|	60|	26|	                487.570007324219
10847|	SAVEA|	2015-01-22|	36|	9.5|	                487.570007324219
10847|	SAVEA|	2015-01-22|	45|	34|	                487.570007324219
10847|	SAVEA|	2015-01-22|	55|	215|	                487.570007324219
10983|	SAVEA|	2015-03-27|	84|	6|	                657.539978027344
10983|	SAVEA|	2015-03-27|	15|	19.5|	                657.539978027344
11030|	SAVEA|	2015-04-17|	100|	19|	                830.75
11030|	SAVEA|	2015-04-17|	70|	21.3500003814697|	830.75
11030|	SAVEA|	2015-04-17|	60|	123.790000915527|	830.75
11030|	SAVEA|	2015-04-17|	100|	55|	                830.75
11032|	WHITC|	2015-04-17|	35|	19|	                606.190002441406
11032|	WHITC|	2015-04-17|	25|	263.5|	                606.190002441406
11032|	WHITC|	2015-04-17|	30|	55|	                606.190002441406
