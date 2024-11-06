# ~ Lita-Capstone- Sales Data Analysis
---

[PROJECT OVERVIEW](#PROJECT-OVERVIEW)

[DATA DESCRIPTION](#data-description)

 [DashBoard Review](#DashBoard-Review)

 [DATA SOURCES](data-sources)

 [TOOLS USED](#tools-used)

 [DATA CLEANING AND PREPARATION](#data-cleaning-and-preparation)

 [EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)
 
## ~ PROJECT OVERVIEW:
---
 This project analyses the sales record of a Retail Store, and it requests for cleaning and removing duplicates for proper exploration of sales Data to uncover key insights such as 
 . Top-selling products, 
 . Regional Perfomances and 
 . Monthly Sales Trend. 
 The goal is to create an interactive dashboard in power BI that shows the findings in the sales data cleaning.

## ~ DATA DESCRIPTION:
---
 This datasets includes the following Columns:
 1. OrderID
 2. Customer ID
 3.Region
 4. Products
 5. Quantity
 6. Unit Price
 7. Total Sales

## ~ DashBoard Review:
---
 . Products: The goods sold in the store
 . Region: The Regional branches of the store  (North, East, South, West) 
 . Unit Price: The Cost Per unit of the products
 . Quantity: The number of unit of the product ordered in each transaction

## ~ DATA SOURCES:
---
 The Primary sources of the data used is the Sales data Provided by the sales department of the Company, Forwarded to Our Lms/Canvas by the Incubator Hub. The data given has a table array of column with customerID, orderID, region, Quantity, Unit price, Products, order Date.

## ~ TOOLS USED
---
 The tools used in the sales Data thus:
 - Microsoft excel [Download Here](https://www.Microsoft.com)
   1. for Data cleaning
   2. For Visualization
   3. for reporting with Pivotable
   
- SQL - Structured Query Language [Download Here](https://www.Microsoft.com)
  1. for Query of Data
  2. for extracting from a query
 
  - Power BI
    1. For Interaction of data [Download Here](https://www.Microsoft.com)
    2. for Visualization
   
       GitHub
       1. For Porfolio Building [Download Here](https://github.com)

      ## ~ DATA CLEANING AND PREPARATION
    ---
     Key components includes:
 1. Data Cleaning and preparation: Ensuring data quality
    through cleaning techniques in SQL and Excel
 2. Sales Analysis: Utilizing SQL queries to 
    extract insights such as Best-Selling products and Sales trends over time.
 3. Visualization: creatiing interactive Dashboards in Power  BI 
    to present findings, including sales by product category and customer demorgraphics.
 4. Reporting: Generating reports that summarize key metrics to 
    inform business decisions and marketing strategies

## ~ EXPLORATORY DATA ANALYSIS
---
The analysis will involve deep exploration of the data to evaluate keys questions 
that are useful for effective decision-making, these includes:
retrieve the total sales for each product category.
 o finding the number of sales transactions in each region.
 o finding the highest-selling product by total sales value.
 o calculating total revenue per product.
 o summarizing monthly sales totals for the current year.
 o finding the top 5 customers by total purchase amount.
 o calculating the percentage of total sales contributed by each region.
 o identifying products with no sales in the last quarter.

### SQL
```
select *
from [dbo].[Book4]
```
--Retrieving the total sales for each categories
```
select Product, sum(Quantity) as Total_sales
from [dbo].[Book4]
Group by Product
```

--Numbers Of Sales Per region
```
Select Region, Count(*) as Total_Transaction
From [dbo].[Book4]
Group By Region
```
--The Highest_selling of Total Sales Value(Revenue)
```
Select Top 1 Product, sum(Quantity * UnitPrice) As Total_Revenue
From [dbo].[Book4]
Group By Product
```
--Calculate Total Revenue per Product
```
Select product, sum(Total_Sales) as Total_Revenue
from [dbo].[Book4]
Group By 
product
```
--Calculate Monthly sales Total for the Current Year
```
select 
month(OrderDate) as Month,
sum(Total_Sales) as Monthly_Total_Sales
From [dbo].[Book4]
where
Year(OrderDate) = 2023
group by
Month(OrderDate)
Order By
Month(OrderDate)
```

--The Top 5 Customers By Purchase Amount
```
 Select Top 5
Customer_id, Sum(Total_Sales) as Total_Purchase_Amount
From[dbo].[Book4]
Group By
Customer_Id
order by
Total_Purchase_Amount Desc
```

--Calculating The percentage of Total Sales Contributed by each Region

```Select Region, 
sum(Total_Sales) as Region_Sales,
sum(Total_Sales) * 100.0/ (Select sum(Total_Sales) 
from [dbo].[Book4])
as Percentage_of_TotalSales
from [dbo].[Book4]
group by Region
order by percentage_Of_TotalSales desc ```

--identifying products with no sales in the Last quarter
```
Select Distinct product
From [dbo].[Book4]
where product Not In(select product
from [dbo].[Book4]
where OrderDate>= DateAdd(quarter,-1,GetDate()) and OrderDate< GetDate()); ```

       



