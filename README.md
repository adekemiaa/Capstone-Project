# Capstone-Project
This is where i documented my analysis of the sales data in the CAPSTONE PROJECT given during my training with the Incubator Hub

### Project Title: SALES DATA and CUSTOMER SUBSCRIPTION DATA
---

### Project Overview
---
This analysis is based on sales data and Customer Data with the aim to generate an insight into the performance of the sales over within year 2023 and 2024. By the analysis of various 
parameter, we get a reasonable decision which enable us to tell a compelling stories around the data in terms of products, region, subscription trens, subscription type, and year of sales.

### Data Source
---
The main source of the data is through online (an open source) freely downloaded on kaggle

### Tools Used
---
1. Microsoft Excel 
  - For data cleaning, Analysis and Visualization
2. Structured Query Language (SQL server)
  - For data queries
3. Microsoft Power BI for
  - Data Cleaning, Analysis and Visualization

### Data Cleaning and Preparations
---
In the initial phase of Data Cleaning and preparations. This was done on the data from Microsoft excel and Microsoft power BI, we perform the following 
action;
1.	Data loading and Inspection
2.	Handling missing variables
3.	Data Cleaning and formatting

 ![SALES CLEANING](https://github.com/user-attachments/assets/e3feffd0-743c-4f2d-8823-75c85c926ba4)

 ![CUSTOMER CLEANING](https://github.com/user-attachments/assets/5665ef20-7f91-4579-95f5-8e5d6a1ca9d2)

### Data Analysis
---
Microsoft Excel and Microsoft power BI was used for the analysis
![Customer Analysis](https://github.com/user-attachments/assets/4e8e7f84-b0c8-4ea6-b6ab-33e2761d80cf)

![Sales Analysis](https://github.com/user-attachments/assets/ab804993-d4c6-4522-810a-1a72a6736056)

### Data Queries For Customer Data
We query the data using SQL server to discover some analysis about the data for effective decision making after importi ng the csv excel file into the sql server, For example
```SQL
SELECT * FROM [dbo].[LITA_CustomerData_TB]

-----NO 1: retrieve the total number of customers from each region.
SELECT Region, count(customerID) AS TotalCustomerByRegion 
FROM [dbo].[LITA_CustomerData_TB]
GROUP BY Region

-----NO 2: find the most popular subscription type by the number of customers.---
SELECT SubscriptionType, count(customerID) AS NoOfCustomerBySType
FROM [dbo].[LITA_CustomerData_TB]
GROUP BY SubscriptionType

----NO 3: find customers who canceled their subscription within 6 months. ----
SELECT CustomerName, SubscriptionType, Canceled FROM [dbo].[LITA_CustomerData_TB]
WHERE Canceled = 1 AND MONTH(SubscriptionStart) <= 6

SELECT CustomerName, SubscriptionType, Canceled FROM [dbo].[LITA_CustomerData_TB]
WHERE Canceled = 1 AND DATEDIFF(MONTH,SubscriptionStart, SubscriptionEnd) <= 6

-----NO 4: calculate the average subscription duration for all customers. ----
SELECT count(CustomerId),avg(datediff(DAY, SubscriptionStart, SubscriptionEnd))
AS AVG_SubscDate FROM [dbo].[LITA_CustomerData_TB]
WHERE SubscriptionEnd IS NOT NULL

-----NO 5: Find customers with subscriptions longer than 12 months.-----
SELECT CustomerName, SubscriptionType, SubscriptionStart, SubscriptionEnd
FROM [dbo].[LITA_CustomerData_TB]
WHERE DATEDIFF(MONTH,SubscriptionStart, SubscriptionEnd)>=12

-----NO 6: calculate total revenue by subscription type.------
SELECT SubscriptionType, Sum(Revenue) AS TOTALRevenue_byST 
FROM [dbo].[LITA_CustomerData_TB]
GROUP BY SubscriptionType
ORDER BY SUM(Revenue) desc

-----NO 7: Find the top 3 regions by subscription cancellations.----
SELECT TOP 3 REGION, Canceled
FROM [dbo].[LITA_CustomerData_TB]
ORDER BY Canceled

----NO 8: Find the total number of active and canceled subscriptions.----
SELECT SUM(CASE WHEN  Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
SUM(CASE WHEN  Canceled = 1 THEN 1 ELSE 0 END) AS CnceledSubscriptions
FROM [dbo].[LITA_CustomerData_TB]
GROUP BY CustomerID

### 
