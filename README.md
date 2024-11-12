# LITA-CAPSTONE-PROJECT
A documentation of my capstone project at LITA organised by the incubator hub 
---
## TABLE OF CONTENT

### [PROJECT TITLE](#project-title)

### [PROJECT OVERVIEW](#project-overview)

### [DATA SOURCES](#data-sources)

### [DATA FORMS](#data-forms)

### [TOOLS USED](#tools-used)

### [DATA CLEANING AND PREPARATION](#data-cleaning-and-preparation) 

### [EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)

### [DATA VISUALISATION](#data-visualisation)

---
### PROJECT TITLE: SALES PERFORMANCE ANALYSIS AND CUSTOMER SUBSCRIPTION ANALYSIS 
---
### PROJECT OVERVIEW
---
#### Project Overview for sales data
This project focuses on analyzing the sales performance of a retail store and drawing key insights such as top-selling products, regional performance, and monthly sales trends. The goal is to understand the trends and take actionable steps to increase revenue in each region 

#### Project Overview for customer subscription data
This project analyzes the trends of a subscription service. It answers major questions on the most used subscription package and the renewal and cancellation patterns.
---
### Data Sources
Both datas where sourced from public sites and provided by the facilitator

#### DATA FORMS
- The data provided are Structured data (Data in tabular form like spreadsheet or database)
---
### TOOLS USED
- Microsoft Excel - (Data entry, data cleanup and analysis)
- SQL- Standard Query Language (Data entry, data management and retrieval)
- Power bi- (Data visualisation and report)
- Github - (Data analyst Portfolio building)
---
### DATA CLEANING AND PREPARATION
After the data retrieval into excel, the data were cleaned and prepared for the pivot table summary 
##### For the sales data, a new column was added to calculate the total sales amount on each order 

![Screenshot (12)](https://github.com/user-attachments/assets/ee65f869-8e0b-4f42-9961-17af11dba027) 

---
### EXPLORATORY DATA ANALYSIS 
#### For sales data
- summary of total sales by product, region, and month.
- average sales per product and total revenue by region.
- total sales for each product category.
- number of sales transactions in each region.
- highest-selling product by total sales value.
- total revenue per product.
- monthly sales totals for the current year.
- top 5 customers by total purchase amount.
- percentage of total sales contributed by each region.
- Products with no sales in the last quarter.

#### For customer subscription  data
- Average subscription duration and most popular subscription types.
- total number of customers from each region.
- most popular subscription type by the number of customers.
- customers who canceled their subscription within 6 months.
- average subscription duration for all customers.
- customers with subscriptions longer than 12 months.
- total revenue by subscription type.
- top 3 regions by subscription cancellations.
- total number of active and canceled subscriptions.

#### Excel EDA for sales data
- Pivot table summary 
![Screenshot (13)](https://github.com/user-attachments/assets/5f23a913-37e1-40fe-a9e7-43198bc44807)

- Other metrics calculated with excel formulas 
![Screenshot (14)](https://github.com/user-attachments/assets/d86e2cd6-80bc-4d44-8929-4e6ec35f3020) 

#### SQL EDA FOR SALES DATA 
- Total sales per product
```sql
SELECT Product, SUM(Quantity * UnitPrice) AS TotalSales
FROM [dbo].[LITA Capstone Project csv]
GROUP BY Product;
```
![Screenshot (15)](https://github.com/user-attachments/assets/fac6a75f-ee04-493c-9d47-6fd42c11ba65) 
- Number of sales transaction in each region
```sql
Select Region, COUNT (OrderID) as NumOftransactions
from [dbo].[LITA Capstone Project csv]
group by region
```
- Highest selling product by total sales value
![image](https://github.com/user-attachments/assets/03c6f402-12dc-437c-991c-ce1c1c334439)

-Total revenue per product
```sql
Select product, sum (sales_amount) as totalrevenue
from [dbo].[LITA Capstone Project csv]
group by product
```
- total monthly sales for 2024
```sql
SELECT MONTH(OrderDate) AS Month,
SUM(sales_amount) AS Totalmonthlysales
FROM [dbo].[LITA Capstone Project csv]
WHERE YEAR(OrderDate) = 2024
GROUP BY MONTH(OrderDate)
order BY MONTH
```
- Top 5 customers by purchase amount
- ![image](https://github.com/user-attachments/assets/1f611c0f-f974-4998-94bb-96cee1eea4ca)

- percentage of total sales contributed by each region
```sql
SELECT Region, SUM(Sales_amount) AS RegionTotalSales,
FORMAT(ROUND((SUM(Sales_amount) / CAST((SELECT SUM(Sales_amount) 
FROM [dbo].[LITA Capstone Project csv]) AS DECIMAL(10,2)) * 100), 1), '0.#') 
AS PercentageOfTotalSales
FROM [dbo].[LITA Capstone Project csv]
GROUP BY Region
ORDER BY PercentageOfTotalSales DESC
```
![image](https://github.com/user-attachments/assets/c6db7d57-afed-46a2-8475-f7507bcfd97c)

- Products with no sales in last quarter:
```sql
SELECT Product FROM[dbo].[LITA Capstone Project csv] 
GROUP BY Product
HAVING SUM(CASE 
WHEN OrderDate BETWEEN '2024-06-01' AND '2024-08-31' 
THEN 1 ELSE 0 END) = 0
```
---
#### Excel EDA for customer subscription data
- Pivot table summary
- ![Screenshot (16)](https://github.com/user-attachments/assets/4d7a17bb-0a6f-4789-9bdb-c5110bfed022)

#### SQL EDA FOR  customer subscription data 
- Total customers per region
```sql
SELECT Region, COUNT(CustomerId) AS TotalCustomers
FROM [dbo].[LITA Capstone Project]
GROUP BY Region
```
(18750 CUSTOMERS PER REGION) 
- Most popular subscription type:
```sql
SELECT SubscriptionType, COUNT(CustomerId) AS TotalCustomer
FROM [dbo].[LITA Capstone Project]
GROUP BY SubscriptionType 
ORDER BY Totalcustomer DESC
```
(most popular is Basic) 
- Customer who canceled within 6 months
```sql
SELECT COUNT(CustomerID) AS TotalCancelledWithinSixMonths
FROM [dbo].[LITA Capstone Project]
WHERE Canceled = 'TRUE' 
AND DATEDIFF(month, SubscriptionStart, SubscriptionEnd) <= 6; 
```
- Average subscription duration
```sql
SELECT AVG(DATEDIFF(day, SubscriptionStart, SubscriptionEnd)) AS AverageSubscriptionDuration
FROM [dbo].[LITA Capstone Project];
```
- Customer with subscription longer than 12 months
```sql
SELECT CustomerID, CustomerName, SubscriptionType, SubscriptionStart, SubscriptionEnd, Subscription_Duration
FROM [dbo].[LITA Capstone Project]
WHERE Subscription_Duration > 365;
```
- total revenue by subscription																																																																																												![image](https://github.com/user-attachments/assets/7a72e269-4586-4bc1-b653-f3407d317c74)

- Top 3 regions by subscription cancellations
![image](https://github.com/user-attachments/assets/e5353957-0775-459e-a76b-53de1080d85f)

- total number of active and canceled subscriptions
![image](https://github.com/user-attachments/assets/646f8783-be79-4ab1-8806-5e1b0dbcdb44)

### DATA VISUALISATION 
##### Using Power bi, dashboards were created to visualise the insights found in Excel and SQL including the report of some additional data summary 
---
Data visualisation for sales performance analysis 

![image](https://github.com/user-attachments/assets/b6300dea-7f90-4153-9d52-ee24ff9703e9) 

Map Visualisation of Products per Region 

![image](https://github.com/user-attachments/assets/9994addb-2228-4b94-94a7-72756e1d8825)



Data visualisation for Customer subscription trends 
																																																																											





