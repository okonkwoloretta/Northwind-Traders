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
   
## Insight:  
 Our dataset has been carefully cleaned and processed to ensure high data quality. We have taken steps to remove any missing values, ensuring that all the required information is present for each record. Additionally, we have meticulously checked for and eliminated any duplicate entries, ensuring that each entry in the dataset is unique. By addressing these issues, we can confidently state that our data is complete and free from any missing values or duplicate records.

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

## Insight:
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

## Insight: 
Customer "QUEEN" has multiple orders with varying quantities, such as 12, 40, 70, and 42.
Customer "ERNSH" also has orders with quantities like 45, 50, 30, and 70.
Customer "RATTC" has orders with quantities such as 30, 28, 60, and 30.
Other customers like "SAVEA," "QUICK," "GREAL," "FOLIG," "HUNGO," and "WHITC" also show varying order quantities.

To further investigate if the high freight values are justified by the large order sizes, let's calculate the average order quantity for each customer and compare it to the overall average order quantity. This will help determine if certain customers consistently place larger orders than others. And also analyze the relationship between the order quantity and the freight cost by calculating metrics such as the average freight cost per unit quantity for each customer. This will provide insights into whether customers with higher order quantities also tend to have higher freight costs per unit.

```sql
-- Calculate average order quantity for each customer
SELECT TOP (20) customerID, AVG(quantity) AS avg_order_quantity
FROM orders o
INNER JOIN order_details od 
ON o.orderID = od.orderID
GROUP BY customerID
```
Output:

|customerID|	avg_order_quantity
|-----------|---------------------|
BLONP|	25|
SEVES|	31||-----------|---------------------|
OLDWO|	25|
THEBI|	6|
FRANS|	5|
MAGAA|	20|
SIMOB|	25|
ALFKI|	14|
FAMIA|	18|
LAZYK|	10|
GROSR|	8|
FOLKO|	27|
CHOPS|	21|
ERNSH|	44|
FRANK|	31|
HILAA|	24|
CENTC|	5|
ISLAT|	12|
GOURL|	16|
BERGS|	19|

```sql
-- Calculate overall average order quantity
SELECT AVG(quantity) AS overall_avg_order_quantity
FROM orders o
INNER JOIN order_details od 
ON o.orderID = od.orderID;
```
Output:

|overall_avg_order_quantity|
|-----------|
|23|

```sql
-- Calculate average freight cost per unit quantity for each customer
SELECT customerID, AVG(freight / quantity) AS avg_freight_per_unit
FROM orders o
INNER JOIN order_details od 
ON o.orderID = od.orderID
GROUP BY customerID
ORDER BY avg_freight_per_unit desc
```

Output:

|customerID|	avg_freight_per_unit|
|-------------|----------|
FOLIG|	20.7103186530762|
QUEEN|	9.59296674097436|
ERNSH|	9.30343513452964|
RANCH|	9.09067650144062|
SIMOB|	8.49795695269045|
BERGS|	8.18355692328988|
THEBI|	8.02728563036237|
OCEAN|	8.00287884798917|
SANTG|	7.89765802704626|
ALFKI|	7.41343236187148
SPECD|	7.21396010678912|
SAVEA|	7.12864017452832|
GREAL|	7.10003620519439|
QUICK|	6.8855187372951|
HUNGO|	6.78914775451192|
MORGK|	6.63430287521897|
SPLIR|	6.55971498553715|
FOLKO|	6.5533369800153|
ANATR|	6.45811898935409|
THECR|	6.44931263128916|
LETSS|	6.42166311400277|
PICCO|	6.2766365140911|
RATTC|	6.27302221364632|
TORTU|	6.20738032311772|
WHITC|	5.94930917333421|
GROSR|	5.87587507963181|
EASTC|	5.66431761562148|
PRINI|	5.64222787947882|
LEHMS|	5.55300410500085|
OLDWO|	5.49672612203492|
PERIC|	5.47009517901034|
RICAR|	5.43460615612772|
MEREP|	5.12856921760547|
RICSU|	5.09585673753547|
ISLAT|	5.01626710264826|
SEVES|	4.96380133903216|
WARTH|	4.72429268979236|
OTTIK|	4.70975591849028|
BONAP|	4.70011752281354|
DRACD|	4.63758019159711|
VICTE|	4.63595503838857|
GODOS|	4.51135323485757|
TRAIH|	4.47061625653894|
VAFFE|	4.4551530974496|
BLONP|	4.32951046093043|
MAGAA|	4.25174936383219|
MAISD|	4.17045765617648|
FRANR|	4.11346033565582|
QUEDE|	4.10177161062048|
AROUT|	4.09769587221221|
LACOR|	4.07922939398362|
FRANK|	4.0514938414045|
LAMAI|	3.95788834718973|
SUPRD|	3.89430667833513|
FURIB|	3.89104281904206|
ROMEY|	3.88992866050629|
HILAA|	3.87669793385803|
TRADH|	3.82604494778228|
KOENE|	3.82034633334573|
COMMI|	3.78804990824726|
WOLZA|	3.62321433935847|
LILAS|	3.61476854246304|
GOURL|	3.55474061701531|
WELLI|	3.48872051119879|
HANAR|	3.48581958329157|
NORTS|	3.45354164226188|
BLAUS|	3.40618706989248|
CONSH|	3.29923479475943|
WANDK|	3.25686987306318|
LONEP|	3.08327800157119|
BOTTM|	3.06952907636006|
HUNGC|	3.06863233271651|
BSBEV|	3.04926408867299|
BOLID|	2.89346936013964|
LINOD|	2.71784652998875|
REGGC|	2.55386850784545|
CHOPS|	2.4955247463903|
ANTON|	2.43770491342919|
WILMK|	2.34075490838172|
FRANS|	2.27652498006821|
CACTU|	1.91732789384467|
DUMON|	1.89344794851131|
VINET|	1.8917794068749|
CENTC|	1.7875|
FAMIA|	1.66215377822954|
GALED|	1.5707500398159|
TOMSP|	1.34988522051143|
LAZYK|	0.970000004768372|
LAUGB|	0.544258927447455|


we can observe the following:

- The average order quantity varies among customers, ranging from 5 to 44 units. This indicates that certain customers consistently place larger orders compared to others.

- The overall average order quantity for all customers is 23 units. Comparing individual customers' average order quantities to this overall average can provide insights into their ordering patterns.

- The average freight cost per unit quantity also varies among customers, ranging from 0.97 to 9.30. This metric helps assess the relationship between order quantity and freight cost.

- There is variation in the average freight cost per unit quantity among customers. Some customers have relatively low average costs, while others have higher average costs.

It is important to note that other factors, such as the distance of shipping, shipping methods, packaging, and other logistical considerations, may also impact the freight costs. These factors are not taken into account in the provided data.

If we consider the average order quantity and average freight cost per unit quantity among the customers, there don't seem to be any customers who stand out as extreme or unusual compared to the rest. The values for these metrics vary to some extent, indicating natural differences in customer ordering patterns and associated freight costs. However, there are no clear indications of customers with significantly higher or lower values that would be considered outliers.

--------
2. Perform exploratory data analysis (EDA) like answering some questions to drive insights from our dataset:

```sql
--- 1. Which products have the highest sales revenue? Are there any specific product categories that contribute significantly to the overall revenue?

SELECT TOP (10) p.productName, c.categoryName, ROUND(SUM(od.unitPrice * od.quantity), 2) AS totalRevenue
FROM products p
INNER JOIN categories c 
  ON p.categoryID = c.categoryID
INNER JOIN order_details od 
  ON p.productID = od.productID
GROUP BY p.productID, p.productName, c.categoryName
ORDER BY totalRevenue DESC;
```

Output:

|Sales Rev by Products|
|-----------|
|![revenue by products](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/8e76f20f-8df8-4ebc-a8a0-fa26d9efb9a9)|



## Insights:

The top-selling products along with their corresponding categories and total sales revenue
- Côte de Blaye - Category: Beverages, Total Revenue: $149,984.2
- Thüringer Rostbratwurst - Category: Meat & Poultry, Total Revenue: $87,736.4
- Raclette Courdavault - Category: Dairy Products, Total Revenue: $76,296
- Tarte au sucre - Category: Confections, Total Revenue: $49,827.9
- Gnocchi di nonna Alice - Category: Grains & Cereals, Total Revenue: $45,121.2
- Manjimup Dried Apples - Category: Produce, Total Revenue: $44,742.6
- Carnarvon Tigers - Category: Seafood, Total Revenue: $31,987.5

These products contribute significantly to the overall revenue.

## Recommendations:

- On Beverage Category: The product "Côte de Blaye" generates the highest revenue. Consider increasing marketing efforts, expanding the product range, or exploring opportunities for partnerships or collaborations within the beverage category to further capitalize on its success.

- Enhance Meat & Poultry: The "Thüringer Rostbratwurst" and "Alice Mutton" are popular choices, consider introducing new meat and poultry products, improving product quality, or offering special promotions to attract more customers and increase sales within this category.

- Dairy Products: "Raclette Courdavault" and "Camembert Pierrot" are top-selling products. Develop targeted marketing campaigns to highlight the unique features, taste, and quality of these products. Consider collaborating with local cheese producers or organizing tasting events to increase customer awareness and drive sales.

- Confections and Grains & Cereals: "Tarte au sucre" and "Gnocchi di nonna Alice" are performing well in the Confections and Grains & Cereals categories, respectively. Consider expanding the product range in these categories, introducing new flavors or variations, and promoting them through appealing packaging, social media campaigns, or collaborations with influencers or food bloggers.

- Produce and Seafood: "Manjimup Dried Apples" and "Carnarvon Tigers" represent the Produce and Seafood categories. Ensure a steady supply of fresh produce and high-quality seafood products. Explore partnerships with local farmers and fishermen to source fresh and unique products, and educate customers about the freshness, sustainability, and health benefits of these products.
----
```sql
--- 2. What is the distribution of order quantities? Are there any patterns or trends?
SELECT quantity, COUNT(*) AS frequency
FROM order_details
GROUP BY quantity
ORDER BY quantity;
```
Output:
|Order of quantity|
|---------------------|
|![frequency by quantity](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/34e6b0a5-6062-4423-ae6a-3f60e58bc70d)|


Most common order quantities: The order quantities of 10, 20, and 30 appear frequently in the dataset, with 181, 252, and 194 occurrences respectively. This suggests that these quantities are popular among customers.

Small order quantities: There is a range of small order quantities, ranging from 1 to 9, which have relatively low frequencies. This indicates that while some customers place smaller orders, they are not as common as larger order quantities.

Large order quantities: There are also some relatively large order quantities in the dataset, such as 40, 50, 60, and 100, with 113, 75, 58, and 10 occurrences respectively. These larger order quantities may represent bulk orders or orders from commercial customers

-----

```sql
--- 3. Which customers have the highest number of orders? Are there any loyal or frequent customers?
SELECT c.customerID, c.companyName, COUNT(o.orderID) AS orderCount
FROM customers c
INNER JOIN orders o 
  ON c.customerID = o.customerID
GROUP BY c.customerID, c.companyName
ORDER BY orderCount DESC;
```
Output:
|Total Orders by Customers|
|---------------------|
|![Orders by customers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/890e75d6-3b3f-4b11-9ddd-332a4f47a6c2)|

## Insights:
- customer with the highest number of orders is "SAVEA" with 31 orders.
- The top 10 customers with the highest order counts range from 31 to 15 orders.
- There are several customers with relatively lower order counts, ranging from 15 to 2 orders.

## Recommendations:

- Focus on retaining loyal and frequent customers, such as "SAVEA," "ERNSH," and "QUICK," who consistently place a high number of orders. Offer them incentives, personalized promotions, or exclusive benefits to encourage their continued loyalty.
- Identify the reasons behind the lower order counts for customers with 15 or fewer orders. Reach out to these customers to gather feedback, understand their needs and preferences, and find ways to enhance their experience to increase their order frequency.
- Consider implementing a customer loyalty program to incentivize repeat purchases and encourage customers to increase their order counts. Rewards, discounts, or exclusive perks can be offered to customers based on their order frequency and total spending.
- Analyze the purchasing patterns and behaviors of the top customers to identify potential cross-selling or upselling opportunities. Recommend related or complementary products to these customers to maximize their order value.
- Implement targeted marketing campaigns or personalized recommendations based on customers' past orders to increase engagement and encourage repeat purchases.

-----
```sql
--- 4. How does the freight cost vary across different regions or countries?
SELECT c.country, AVG(o.freight) AS average_freight_cost
FROM orders o
JOIN customers c 
 ON o.customerID = c.customerID
GROUP BY c.country;
```
Output:
|Avg Freight per Country |
|-----------|
|![Freight cost per country](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/064d6204-951d-4446-9f13-e18d6dd9d88b)|

## Insights:

There is significant variation in average freight costs across different countries. 
- The highest average freight cost is observed in Austria (184.79), while the lowest is in Poland (25.11).

- European countries like Austria, Ireland, Germany, Sweden, Denmark, Switzerland, Belgium, and Portugal have relatively higher average freight costs compared to other regions.

- North American countries like the USA and Canada also have relatively high average freight costs but are lower compared to some European countries.

- South American countries like Venezuela, Brazil, and Argentina have moderate average freight costs.

- Countries like France, the UK, Norway, Finland, Mexico, Spain, Italy, and Poland have relatively lower average freight costs.

## Recommendations:

- Identify the factors contributing to higher freight costs in countries like Austria, Ireland, and Germany.
- Analyze the transportation infrastructure, customs procedures, and logistics networks to identify potential areas for optimization and cost reduction.
- Explore opportunities for negotiation or collaboration with shipping companies or freight forwarders in countries with high average freight costs. 
- Seek competitive rates and optimize shipping routes to reduce costs.
- Monitor and analyze freight cost trends over time for each country. 
- Identify any patterns or fluctuations that may impact cost optimization strategies.
- Consider regional or localized distribution centers in countries with higher average freight costs to reduce transportation distances and costs.
- Evaluate the impact of trade agreements, tariffs, and customs regulations on freight costs in different countries. Stay updated with changes in trade policies that may affect shipping costs and adjust strategies accordingly.
- Benchmark average freight costs against industry standards and competitors to gauge competitiveness and identify areas for improvement.
- Continuously track and analyze customer demand and order patterns in different countries to optimize inventory management and minimize costly shipping methods.
---------

```sql
--- 5. Can we identify any seasonal trends in sales? Are there specific months or periods where sales are consistently higher?
SELECT
    DATEPART(MONTH, o.orderDate) AS salesMonth,
    SUM(od.quantity) AS totalQuantity,
    ROUND(SUM(od.quantity * od.unitPrice),2) AS totalSales
FROM
    orders o
    JOIN order_details od ON o.orderID = od.orderID
GROUP BY
    DATEPART(MONTH, o.orderDate)
ORDER BY
    totalSales DESC;
```
Output:
|   Seasonal Trends in Sales|
|-----------|
|  ![Sales trend by month](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/ef33eed0-2cb9-41f2-94ae-3e72d40efb8e)|

## Insights:
Seasonal Sales Patterns Month 4 (April), 1 (January), 3 (March), 2 (February), and 12 (December) exhibit higher sales compared to the remaining month, with 6,592 units sold and $190,329.95 in sales in April, and 4,882 units sold and $128,429.66 in sales in December.  These months may be influenced by seasonal factors, holidays, or specific events that drive customer demand.

## Recommendations:

- Allocate additional resources and marketing efforts during the months of April, January, March, February, and December to maximize sales potential. Identify specific marketing strategies or promotions that align with the seasonal trends and customer preferences during these months.

- Conduct a deeper analysis to understand the factors contributing to higher sales in these specific months. Consider external factors such as holidays, cultural events, or industry-specific trends that could impact customer buying behavior. This analysis will help tailor your marketing and sales strategies accordingly

-----
```sql
--- 6. Can we identify any sales trends or patterns over time?
SELECT
    YEAR(o.orderDate) AS salesYear,
    MONTH(o.orderDate) AS salesMonth,
    ROUND(SUM(od.quantity * od.unitPrice * (1 - od.discount)), 2) AS monthlySales
FROM
    orders o
    JOIN order_details od ON o.orderID = od.orderID
GROUP BY
    YEAR(o.orderDate),
    MONTH(o.orderDate)
ORDER BY
    salesYear, salesMonth;
```

Output:

| Yearly Sales Trend|
|-----------|
|![yearly sales](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/8b704f16-0819-4246-bfc0-caa98f9c0038)|

## Insight:
- There seems to be a consistent pattern of higher sales during certain months. For example, sales tend to be higher in the last quarter of the year (October to December). 
This could be attributed to holiday seasons or promotional campaigns during that period.

- Sales show variations across different years. It's important to examine the factors that contributed to the significant increase in sales from 2013 to 2014, particularly in the months of January, April, and December.
--------

```sql
--- 7.  best and worst selling products
SELECT
    products.productName,
    SUM(order_details.quantity) AS totalQuantity
FROM order_details
INNER JOIN products 
	ON order_details.productID = products.productID
GROUP BY products.productName
ORDER BY totalQuantity DESC;
```
Output:
| Top and Bottom Products sold|
|-----------|
|![top bottom products sold](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/c63bb81c-00f5-4893-8c7c-49bbc376a185)|           

## Insights:

- The best-selling products are "Camembert Pierrot," "Raclette Courdavault," and "Gorgonzola Telino." These products have the highest total quantity sold.

- The worst-selling products are "Gravad lax," "Genen Shouyu," and "Mishi Kobe Niku." These products have the lowest total quantity sold.

## Recommendations:

- Focus on promoting and highlighting the best-selling products to further increase their sales. Consider offering special deals or discounts on these products to attract more customers.

- Analyze the reasons behind the low sales of the worst-performing products. Evaluate their demand and popularity among customers. It may be necessary to assess the product quality, marketing strategies, or customer preferences to understand why they are not selling well.

- Identify potential opportunities for cross-selling or upselling. Look for products that are frequently purchased together with the best-selling items. Promote these complementary products to customers who are already interested in the popular items, increasing the chances of additional sales.

- Consider introducing new products that align with market trends and customer demands while phasing out or repositioning underperforming products.

- Collaborate with key customers to understand their specific needs and preferences. Develop tailored marketing campaigns or loyalty programs to strengthen relationships and drive repeat business.

- Monitor competitors' products and pricing strategies. Stay competitive by offering unique value propositions, competitive pricing, or additional services to attract customers.
------

```sql
--- 8. Key customers
SELECT customers.customerID,
    customers.companyName,
    SUM(order_details.quantity * order_details.unitPrice) AS totalSales 
FROM orders
INNER JOIN  customers
    ON orders.customerID = customers.customerID
INNER JOIN order_details
     ON orders.orderID = order_details.orderID
GROUP BY customers.customerID,
    customers.companyName    
ORDER BY totalSales DESC;
```
Output:
| Top and Bottom Products sold|
|-----------|
|![Key customers](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/ba8b8cf4-005b-4d98-9d19-74dba9d0a1b6)|

## Insights:

- The top key customers based on total sales are "QUICK-Stop," "Save-a-lot Markets," and "Ernst Handel." These customers have the highest total sales.

- The lowest key customers based on total sales are "Galería del gastrónomo," "North/South,", "Laughing Bacchus Wine Cellars" and "Centro comercial Moctezuma". These customers have the lowest total sales.

## Recommendations:

- Nurture and strengthen relationships with the top key customers to encourage repeat business. Offer personalized promotions, discounts, or loyalty programs to incentivize them to continue purchasing from your company.

- Analyze the sales patterns and preferences of the top key customers to identify potential cross-selling or upselling opportunities. Understand their specific needs and recommend complementary products or services that align with their purchasing history.

- Investigate the reasons behind the lower sales of the lowest key customers. Reach out to them to gather feedback and understand their concerns or reasons for not making frequent purchases. Consider offering special incentives or tailored solutions to encourage them to increase their engagement.

- Identify potential growth opportunities among the mid-tier customers. These customers may have the potential to become key customers with the right nurturing and targeted marketing efforts. Develop strategies to engage them further and increase their sales volume.

- Consider organizing customer appreciation events or exclusive networking opportunities to foster stronger relationships with key customers. Such events can create a platform for collaboration, feedback sharing, and strengthening partnerships.
------

```sql
--- 9. Determine if shipping costs are consistent across providers
SELECT
    shippers.companyName AS shipper,
    AVG(orders.freight) AS averageFreight
FROM orders   
INNER JOIN  shippers
    ON orders.shipperID = shippers.shipperID
GROUP BY shippers.companyName;
```
Output:
| Avg Freight Fee|
|-----------|
|![shipper fee](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/0c688088-57f4-450a-9dcc-9685b78cbda2)|

## Insights:

- Among the three shipping providers, Speedy Express has the lowest average freight cost at $65.001 per shipment, while United Package has the highest average freight cost at $86.640 per shipment.

Federal Shipping falls in between the other two providers, with an average freight cost of $80.441 per shipment.

## Recommendations:

- Analyze the shipping cost breakdown provided by each shipping provider. Look into factors such as distance, package weight, delivery speed, and any additional services or surcharges included in the freight cost. This analysis will help identify any discrepancies or variations in the cost structure.

- Consider factors such as delivery time, reliability, package handling, customer support, and overall customer satisfaction. While cost is essential, it should be balanced with the quality and reliability of the shipping service.

- Engage in discussions with each provider to understand their pricing structure, any available promotions, and the possibility of establishing long-term partnerships that offer cost advantages.

- Track metrics such as on-time delivery, package condition upon arrival, and any instances of lost or damaged shipments. Consistently assess the reliability and effectiveness of the shipping providers to ensure they meet your company's standards and customer expectations.
---
```sql
---KPIs
--1. Total Number of Orders
SELECT COUNT(DISTINCT orderID) AS TotalOrders
FROM orders;
```
|TotalOrders|
|-----------|
|830|

```sql
--2. Total Revenue
SELECT ROUND(SUM(unitPrice * quantity * (1 - discount)), 2) AS TotalRevenue
FROM order_details;
```
|TotalRevenue|
|-----------|
|1265793.04|

```sql
--3. Average Order Value
SELECT ROUND(AVG(unitPrice * quantity * (1 - discount)), 2) AS AverageOrderValue
FROM order_details;
```
|AverageOrderValue|
|-----------|
|587.37|

```sql
--4. Number of Customers
SELECT COUNT(DISTINCT customerID) AS CustomerCount
FROM customers;
```
|CustomerCount|
|-----------|
|91|

```sql
--5. Number of Products
SELECT COUNT(DISTINCT productID) AS ProductCount
FROM products;
```
|ProductCount|
|-----------|
|77|

## Dashboard View

![northwind frame](https://github.com/okonkwoloretta/Northwind-Traders/assets/116097143/bad457fa-f296-44f5-a9be-a5ce9d9b44a5)

