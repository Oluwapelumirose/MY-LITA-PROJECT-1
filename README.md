# MY-LITA-PROJECT-1 (SALES DATA)

[Project Overview](#project-overview)

[Objective](#objective)

[Tools Used](#tools-used)

[Pivot Tables for Each Dataset](#pivot-tables-for-each-dataset)

[PowerBi Data Visualization](powerBi-data-visualization)

### Project Overview 
A sales performance analysis typically aims to evealuate and understand key sales trends, identify top-performing products and pinpoint areas for improvement. Here's an overview to guide through structuring a sales performance analysis project;

### Objective
To assess the store's sales performance to inform better business decisions
To identify top-performing products, peak sales periods, and underperforming areas
To analyze customer buying patterns, and regional trends on sales.
Data Collection The main data sources for this analysis is the "Data Sales" file, which are open-source datasets available

### Tools Used

- Excel: for data cleaning and visualization
- SQL: Utilized for data cleaning through queries
- PowerBI: Used for both data cleaning and visualization
- Data Cleaning and Preparations In the initial phase of Data Cleaning and Preparations, we perform the following actions;
- Data loading and inspection
- Handling missing variables
- Data Cleaning and Formatting
  
1. Excel: This is a popular spreadsheet software developed by Microsoft.
### Steps taken in excel
1. Load the data
2. Cleaned the data
3. Removed duplicate
4. Created pivot table for different visualisation needs
5. create report
  
![SalesData Table](https://github.com/user-attachments/assets/2ff6d740-0809-40df-92da-a5de5735d737)
Sales Data


![CustomerData Table](https://github.com/user-attachments/assets/45b8881d-0c45-470b-ad3e-9291e7d1a944)
Customers Data


### Pivot Tables for Each Dataset
Used of pivot table to summarize total sales by product, region and month

![CustomerData Table](https://github.com/user-attachments/assets/be05aa59-cd67-4d0a-8d6f-25ebc9347d6c)
Sales Data


![CustomerData Table](https://github.com/user-attachments/assets/d14455fb-60f6-4487-a0dc-194be1b44179)
Customers Data

### Calculations in Both Dataset
- Total Sales =   Quantity * Unit price
- Average Total Sales = Total Sales/Quantity
- Overall Total Sales =sum of total sale in each region
- Average sales per product = overall total sales/Total quantity

  
2. SQL: To query and retrieve specific data.

   ```
   CREATE database LITA_Capstone_Project_1
   SELECT * from [dbo].[LITA_Capstone_Project_1]
   ```

Write queries to extract key insights based on the following questions;

- retrieve the total sales for each product category
  
   ```
   SELECT Product,
   SUM(revenue) AS TotalSales
   FROM [dbo].[LITA Capstone SalesData]
   GROUP BY Product;
   ```
  
![SD Query 1](https://github.com/user-attachments/assets/2f16b1bd-7d50-44f9-bf0c-22d7c720c480)

- find the number of sales transactions in each region
  
   ```
   SELECT Region,
   COUNT(*) AS NumberofTransaction
   FROM [dbo].[LITA Capstone SalesData]
   GROUP BY Region;
   ```
![SD 2](https://github.com/user-attachments/assets/52558fb3-cb05-400c-aca3-dfd2bdf4f452)


- find the highest-selling product by total sales value
  
  ```
  SELECT TOP 1 Product,
  SUM(revenue) AS TotalSales
  FROM [dbo].[LITA Capstone SalesData]
  GROUP BY Product
  ORDER BY TotalSales DESC;
  ```
![SD 3](https://github.com/user-attachments/assets/8268c0b0-c4f6-44f5-9b88-68e2bedb2630)

  
- calculate total revenue per product
  
 ```
 SELECT Product,
 SUM(revenue) AS TotalRevenue
 FROM [dbo].[LITA Capstone SalesData]
 GROUP BY Product
 ORDER BY Product DESC;
 ```
![SD 4](https://github.com/user-attachments/assets/0020fe00-af8e-4b0a-8bbd-c95d2bd104e1)


- calculate monthly sales totals for the current year
  
 ```
 SELECT Month(OrderDate) AS SalesMonth,
 SUM(revenue) AS Monthly_Sales
 FROM [dbo].[LITA Capstone SalesData]
 WHERE year(orderdate) = year(GETDATE())
 GROUP BY Month(OrderDate)
 ORDER BY SalesMonth;
 ```
![SD 5](https://github.com/user-attachments/assets/7100d2fe-dae9-42f2-a80a-f28ace74d795)



- find the top 5 customers by total purchase amount
  
 ```
 SELECT TOP 5 Customer_Id,
 SUM(revenue) AS TotalPurchaseAmount
 FROM [dbo].[LITA Capstone SalesData]
 GROUP BY Customer_Id
 ORDER BY TotalPurchaseAmount DESC;
 ```
![SD 6](https://github.com/user-attachments/assets/2f81a108-ebc7-421f-adea-75cdfe893605)


- calculate the percentage of total sales contributed by each region
  
 ```
 WITH TotalSales AS(
 SELECT sum(revenue) AS TotalSalesAmount
 FROM [dbo].[LITA Capstone SalesData])
 SELECT Region, 
 sum(revenue) AS RegionSales, 
 (sum(revenue) * 100.0)/ts.TotalSalesAmount AS PercentageContribution
 FROM [dbo].[LITA Capstone SalesData]
 CROSS JOIN TotalSales ts
 GROUP BY Region, 
 ts.TotalSalesAmount;
```
![SD 7](https://github.com/user-attachments/assets/5e01f98e-5c63-45f0-bbc8-db8aa055fad0)


- identify products with no sales in the last quarter
  
 ```
 SELECT Product
 FROM [dbo].[LITA Capstone SalesData]
 WHERE OrderDate<
 DATEADD(QUARTER,-1,GETDATE())
 GROUP BY Product
 HAVING SUM(Quantity)=0;
 ```
![SD 8](https://github.com/user-attachments/assets/e6885d9e-0d53-43d8-9765-120ad5057517)


### PowerBi Data Visualization

![SalesData Dashboard 1](https://github.com/user-attachments/assets/fabd8aff-61d4-44c6-8007-7323eeaf4fec)


  





