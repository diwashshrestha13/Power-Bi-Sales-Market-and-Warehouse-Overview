# Power-Bi-Sales-Market-and-Warehouse-Overview
This is a small project in which I build dashboard for various groups of team in a business environment. The dashboard are based on metrics that I assume would be helpful for strategic decision making.   
📊 Power BI Dashboard Documentation  
Author: Diwash Shrestha  
Created Date: 02/03/2025  
________________________________________  
🔹 Overview  
•	Purpose: The purpose of this dashboard is to analyze sales by region and product, understand the performance of product and warehouse, order fulfillment rate, and gain customer insights.   
•	Target Audience: The dashboard is suitable for all the stakeholders including senior management, logistic team, marketing team, and financial team.   
•	Business Problem: The dashboard helps understand the top product category, profit from fulfilled orders, order fulfilment rate, market insights, customer insights, and geographical insights.   
•	Key Metrics: Key metrics include, not limited to, total revenue, total profit, average profit per order, percentage of order fulfilled, categorical bucked of customer based on credit limit, Units Sold and more. 
    
________________________________________  
📂 Dataset Information  
Source	Description	Format  
ML-Dataset.csv	Contains order details (RegionName, CountryName, State, City, PostalCode, WarehouseAddress, WarehouseName, EmployeeName, EmployeeEmail, EmployeePhone, EmployeeHireDate, EmployeeJobTitle, CategoryName, ProductName, ProductDescription, ProductStandardCost, Profit, ProductListPrice, CustomerName, CustomerAddress, CustomerCreditLimit, CustomerEmail, CustomerPhone, Status, OrderDate, OrderItemQuantity, PerUnitPrice, TotalItemQuantity)	CSV  
________________________________________
📊 Dashboard Features  
Visual	Description  
📌 KPI Cards	Displays: total revenue, orders, and supplier performance.  
📊 Bar Chart:	Count of Customer based on Credit Limit, Top 10 Products delivered, Top Categories  
📈 Line Chart:	Total Revenue by Month overall, Total Profit by month (filtered with category)  
📍 Map Visual	Displays: Sales by region, Display Order fulfilled by Region  
📂 Table:	Product Description and Units Sold, Warehouse Performance Table,  
Dax Measures Used: 
Average Order Value = [Total Revenue] / [Total Units]  
Average Revenue per Order = [Total Revenue] / COUNTROWS('ML-Dataset')  
AvgProfitPerOrder = 
VAR TotalProfit =  
SUMX(
      FILTER('ML-Dataset', 'ML-Dataset'[Status] = "Shipped"),
      'ML-Dataset'[Profit] * 'ML-Dataset'[TotalItemQuantity]
                       )
      VAR TotalOrders = COUNTROWS('ML-Dataset')

   RETURN 
   DIVIDE(TotalProfit, TotalOrders, 0)  
    
  (calculated column) Credit_Limit_Bucket =   
  SWITCH(   
    TRUE(),       
    'ML-Dataset'[CustomerCreditLimit] <= 1000, "0-1000",       
    'ML-Dataset'[CustomerCreditLimit] <= 2000, "1001-2000",     
    'ML-Dataset'[CustomerCreditLimit] <= 3000, "2001-3000",     
    'ML-Dataset'[CustomerCreditLimit] <= 4000, "3001-4000",       
    'ML-Dataset'[CustomerCreditLimit] <= 5000, "4001-5000",    
    "Above 5000"    
)          
Number of Order = COUNTROWS('ML-Dataset')    
StatusPercentage =   
DIVIDE(  
    COUNT('ML-Dataset'[Status]),   
    CALCULATE(COUNT('ML-Dataset'[Status]), ALL('ML-Dataset'[Status]))   
) * 100     
Total Profit =    
SUMX(   
    FILTER('ML-Dataset', 'ML-Dataset'[Status] = "Shipped"),      
    'ML-Dataset'[Profit] * 'ML-Dataset'[TotalItemQuantity]     
)       
Total Revenue = SUMX('ML-Dataset', 'ML-Dataset'[OrderItemQuantity] * 'ML-Dataset'[PerUnitPrice])    
Total Revenue (Only Delivered) =    
CALCULATE(   
    SUM('ML-Dataset'[TotalItemQuantity]) * SUM('ML-Dataset'[PerUnitPrice]),    
    'ML-Dataset'[Status] <> "Pending",      
    'ML-Dataset'[Status] <> "Not Delivered"     
)  
Total Units = SUM('ML-Dataset'[OrderItemQuantity])     


________________________________________  
  
⚙️ How to Use  
Instructions on how to interact with the dashboard:  
•	Filters & Slicers: Users can filter by year, region, status, etc.  
•	Exporting Data: Users can download reports in Excel or CSV format.  
________________________________________  
🚀 Installation & Setup  
Steps to run the Power BI file locally:  
1.	Download the .pbix file from this repository.  
2.	Install Power BI Desktop (if not already installed).  
3.	Open the .pbix file in Power BI.  
4.	Update the data source settings to connect to your local database or sample dataset.  
________________________________________  

