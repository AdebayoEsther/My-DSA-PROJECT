# My-DSA-PROJECT

Hi there, I'm Esther, I'm an entry-level Data Analyst with a growing passion for uncovering insight from data. Eager to learn and take on new challenges, I enjoy turning numbers into meaningful stories that support smart business decisions. Here are a few of my recently completed analysis.
## AMAZON PRODUCT REVIEW ANALYSIS - Case Study 1
A detailed analysis of Amazon product and customer review data to find useful insights for improving products, marketing and customer experience. It includes a clear and interactive Excel dashboard.
### Project Overview
 The Amazon product review analysis question was solved through the use of pivot tables and calculated columns, An excel dashboard was also employed to summarize the whole pivot tables.

 ### Skills and Tools Employed
 - Ms Excel for data cleaning
- Pivot tables for analysing data
- Pivot chart for interpretation of data
 
## KMS SQL CASE STUDY - Case study 2

The Kultra Mega Stores (KMS) Sales Analysis shows a clear analysis of sales and order data for a retail company. It highlighted key trends, best and worst-performing products, and ways to improve operations through the use of SQL

### Skills and Tools Employed
- Ms Excel for data set cleaning
- SQL Server was used to analyse the dataset of the retail company.

Here are some of the queries used to analyse and interprete the questions.
SELECT * from KMS_SQL_CASE_STUDY;

------1. Which Product Category has the Highest sales?------

 SELECT Product_category, Sum(sales) as total_sales
from KMS_SQL_CASE_STUDY
group by product_category
order by total_sales desc

------2. What are the top 3 and bottom 3 region in terms of sales?------

---For Top 3 Regions
SELECT Region, Sum(sales) as Top_sales
From KMS_SQL_CASE_STUDY 
group by region
order by Top_sales DESC
Offset 0 rows fetch next 3 rows only;

---For Bottom 3 Regions
SELECT Region, Sum(sales) as Bottom_sales
From KMS_SQL_CASE_STUDY 
group by region
order by Bottom_sales
Offset 0 rows fetch next 3 rows only;


------3. What are the total sales of appliances in Ontario?-----
SELECT Region, Sum(sales) as Ontario_total_sales
From KMS_SQL_CASE_STUDY
where region = 'Ontario'
Group by Region

------4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customer?-----
SELECT Customer_Name, Sum(sales) as Customer_bottom_sales
From KMS_SQL_CASE_STUDY
Group by Customer_Name
Order by Customer_bottom_sales
Offset 0 rows fetch next 10 rows only;

NOTE TO MANAGEMENT: After analyzing the bottom 10 customers, i recommend segmenting them based on potential and engagement.
1.----For dormant accounts, implement targeted reactivation campaigns and account reviews. For price sensitive customers, introduce bundled offerings tied to volume commitments.
2.----For new customers, strengthen onboarding and upselling efforts. 
3.----For low fit customers, focus on efficient servicing rather than growth. Progress should be tracked montyly to assess impact on revenue and profitability.

------5. KMS incurred the most shipping cost using which shipping method?-----
SELECT Ship_Mode, sum(Shipping_cost) as Total_Shipping_Cost
From  KMS_SQL_CASE_STUDY
Group by Ship_Mode
Order by Total_Shipping_Cost DESC
Offset 0 rows fetch next 1 rows only;


------6.Who are the most valuable customers,and what products or services do they typically purchased?-----
-----For most valuable customer------
SELECT Customer_segment, Customer_Name, Sum(Order_Quantity * Unit_Price) as Total_Revenue
From KMS_SQL_CASE_STUDY
Group by Customer_Segment, Customer_Name
Order by Total_Revenue DESC
Offset 0 rows fetch next 3 rows only;

-----For products or services they purchased------
SELECT Customer_Name,Product_Name, Sum(Order_Quantity) as Total_Quantity_Purchased, Sum(Order_Quantity * Unit_Price) as Total_Spent
From KMS_SQL_CASE_STUDY
Group by Customer_Name, Product_Name
Order by Total_Quantity_Purchased DESC
Offset 0 rows fetch next 3 rows only;

------7.Which small business customer has the hihest sales?-----
SELECT Customer_Name, Sum(sales) as Total_Sales
From KMS_SQL_CASE_STUDY
Where Customer_segment = 'small business'
Group by Customer_Name
Order by Total_sales DESC
Offset 0 rows fetch next 3 rows only;

------8.Which corporate customer placed the most numbers of order in 2009-2012?-----

SELECT Customer_Name, Count(Order_ID) as Order_Count
From KMS_SQL_CASE_STUDY
Where Customer_segment = 'Corporate' AND Order_Date BETWEEN '2009-01-01' AND '2012-12-31'
Group by Customer_Name
Order by Order_Count DESC
Offset 0 rows fetch next 1 rows only;


------9.Which consumer customer was the most profitable one?-----
SELECT Customer_Name, Sum(Profit) as Total_Profit
From KMS_SQL_CASE_STUDY
Where Customer_segment = 'Consumer' 
Group by Customer_Name
Order by Total_Profit DESC
Offset 0 rows fetch next 1 rows only;

------10.Which customer returned items and what segment do they belong to?-----
SELECT k. Order_ID, Customer_Name, Customer_Segment 
From KMS_SQL_CASE_STUDY k
Join ORDER_STATUS o ON k.Order_ID = o. Order_ID 
Where Status = 'Returned'


------11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer-------
SELECT Order_Priority, Ship_Mode, 
COUNT(Order_ID) as Order_Count, ROUND(SUM(Sales-Profit),2) as Estimated_shipping_cost,
AvG(Datediff(day,(order_date),(ship_date))) as Average_Ship_Days
From KMS_SQL_CASE_STUDY
Group by Order_Priority, Ship_Mode 
Order by Order_Priority, Ship_Mode DESC

