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





