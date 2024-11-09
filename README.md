# Capstone-Project--Customer-Data

![image](https://github.com/user-attachments/assets/19456c49-8b24-4fa1-b780-a1ce177d70aa)

Year/Quarter	Number of Subscriptions	Total Revenue
2022		
Qtr1	5076	10151946
Jan	1693	3378897
John	1693	3378897
Basic	1693	3378897
Feb	1693	3395374
Jane	1693	3395374
Premium	1693	3395374
Mar	1690	3377675
Alex	1690	3377675
Basic	1690	3377675
Qtr2	5014	10018882
Apr	1662	3326162
Maria	1662	3326162
Standard	1662	3326162
May	1673	3345833
James	1673	3345833
Basic	1673	3345833
Jun	1679	3346887
Ella	1679	3346887
Premium	1679	3346887
Qtr3	5075	10147339
Jul	1714	3427436
Mike	1714	3427436
Basic	1714	3427436
Aug	1676	3354682
Sara	1676	3354682
Standard	1676	3354682
Sep	1685	3365221
Tom	1685	3365221
Basic	1685	3365221
Qtr4	5110	10220271
Oct	1692	3384539
Eva	1692	3384539
Premium	1692	3384539
Nov	1718	3437444
Liam	1718	3437444
Basic	1718	3437444
Dec	1700	3398288
Anna	1700	3398288
Standard	1700	3398288
2023		
Qtr1	5061	10069844
Jan	1692	3351225
Chris	1692	3351225
Basic	1692	3351225
Feb	1683	3357269
Zoe	1683	3357269
Premium	1683	3357269
Mar	1686	3361350
Paul	1686	3361350
Basic	1686	3361350
Qtr2	5076	10177140
Apr	1687	3385349
Grace	1687	3385349
Standard	1687	3385349
May	1690	3376796
Rob	1690	3376796
Basic	1690	3376796
Jun	1699	3414995
Sophia	1699	3414995
Premium	1699	3414995
Qtr3	3375	6754753
Jul	1680	3354858
Dan	1680	3354858
Basic	1680	3354858
Aug	1695	3399895
Nina	1695	3399895
Standard	1695	3399895
Grand Total	33787	67540175
![image](https://github.com/user-attachments/assets/46874bcd-d739-4b04-bddb-19f7b20b32f8)


![image](https://github.com/user-attachments/assets/3fc4d345-fb9f-41ce-958f-d56241807919)

Period	Customer ID
Qtr1	208
Jan	207
Basic	207
Feb	208
Premium	208
Mar	209
Basic	209
Qtr2	211
Apr	210
Standard	210
May	211
Basic	211
Jun	212
Premium	212
Qtr3	213
Jul	213
Basic	213
Aug	214
Standard	214
Sep	209
Basic	209
Qtr4	211
Oct	210
Premium	210
Nov	211
Basic	211
Dec	212
Standard	212
Grand Total	211
![image](https://github.com/user-attachments/assets/8397f2fe-3578-41ca-8753-484a8bb60f19)


# Using Structured Query Language

***Total Sales for Each Product Category***

Select Product, SUM (Total_Sales) AS [Total Sales]
FROM dbo.Sales_Data
GROUP BY Product

Product Total Sales
Shoes	613380
Jacket	208230
Hat	    316195
Socks	180785
Shirt	485600
Gloves	296900

select * from dbo.Sales_Data


***Number of Sales Transaction In Each Region***

SELECT Region, COUNT(*) AS [Sales Transaction]
FROM dbo.Sales_Data
GROUP BY Region

Region  Sales Transaction
North	2481
East	2483
South	2480
West	2477

select * from dbo.Sales_Data


***Highest-Selling Product By Total Sales Value***

Select TOP 1 Product, SUM (Total_Sales) AS [Total Sales]
FROM dbo.Sales_Data
GROUP BY Product
ORDER BY [TOTAL SALES] DESC

Product Total Sales
Shoes	613380

select * from dbo.Sales_Data


***Total Revenue Per Product***

Select Product, SUM(Quantity*UnitPrice) AS [Total Revenue]
FROM dbo.Sales_Data
GROUP BY Product
ORDER BY [TOTAL REVENUE] DESC

Product Total Revenue
Shoes	613380
Shirt	485600
Hat	    316195
Gloves	296900
Jacket	208230
Socks	180785

select * from dbo.Sales_Data


***Calculate Monthly Sales Total For The Current Year***

SELECT MONTH(OrderDate) AS MONTH,
SUM(Quantity*UnitPrice) AS [Total Sales]
FROM dbo.Sales_Data
WHERE YEAR(OrderDate) = YEAR(2024)
GROUP BY MONTH(OrderDate)
ORDER BY MONTH

select * from dbo.Sales_Data


***Top 5 Customers By Total Purchase Amount***

SELECT TOP 5 Customer_Id,
SUM (Total_Sales) AS [Total Purchase Amount]
FROM dbo.Sales_Data
GROUP BY Customer_Id
ORDER BY [TOTAL PURCHASE AMOUNT] DESC

Customer_Id   Total Purchase Amount
Cus1431	      4235
Cus1495	      4235
Cus1005	      4235
Cus1115	      4235
Cus1302	      4235

select * from dbo.Sales_Data


***Percentage of Total Sales Contributed By Each Region***

SELECT Region,
SUM (Total_Sales) AS [Total Sales],
(SUM (Total_Sales) * 100.0)/ (SELECT SUM(Total_Sales) 
FROM dbo.Sales_Data) AS [Sales Percentage]
FROM dbo.Sales_Data
GROUP BY Region
ORDER BY [Sales Percentage] DESC

Region  Total Sales  Sales Percentage
South	927820	     44.158984146324
East	485925	     23.127281553860
North	387000	     18.419011084722
West	300345	     14.294723215093

select * from dbo.Sales_Data

***Identifying Products With No Sales In The Last Quarter***

SELECT Product,
SUM(TOTAL_SALES) AS [Total Sales]
FROM dbo.Sales_Data
WHERE Product NOT IN ('quarter')
  AND OrderDate >= DATEADD(quarter,-3,GETDATE()) -- 3 quarters ago
  AND OrderDate >= DATEADD(quarter,-1,GETDATE()) -- Last quarter
GROUP BY Product
ORDER BY [Total Sales] DESC;


select * from dbo.Sales_Data


********PROJECT 2********

***Total Number of Customers From Each Region***

SELECT Region,
COUNT(distinct CustomerID) AS [Total Customers]
FROM dbo.Customer_Data2
GROUP BY Region

Region  Total Customers
East	5
North	5
South	5
West	5

select * from dbo.Customer_Data2



***Most Popular Subscription Type By The Number of Customers***

SELECT TOP 1 SubscriptionType,
COUNT(distinct CustomerID) AS [Total Customers]
FROM dbo.Customer_Data2
GROUP BY SubscriptionType
ORDER BY [Total Customers] DESC;


SubscriptionType  Total Customers
Basic	           10


select * from dbo.Customer_Data2


***Customers Who Cancelled Their Subscription Within 6Months***

SELECT CustomerID
FROM dbo.Customer_Data2
Where datediff(month,subscriptionstart,subscriptionend)<=6


CustomerID
None


select * from dbo.Customer_Data2


***Average Subscription Duration For All Customers***

SELECT AVG(datediff(day,subscriptionstart,subscriptionend))
AS [Avg Subscription Duration]
FROM dbo.Customer_Data2

Avg Subscription Duration
365

select * from dbo.Customer_Data2



***Customers With Subscription Longer Than 12Months***

SELECT CustomerID
From dbo.Customer_Data2
Where DATEDIFF(month,subscriptionstart,subscriptionend)>12

CustomerID
None

select * from dbo.Customer_Data2



***Total Revenue By Subscription Type***

Select SubscriptionType,
SUM (Revenue) AS [Total Revenue]
From dbo.Customer_Data2
Group By SubscriptionType


SubscriptionType	Total Revenue
Basic	            33776735
Premium	            16899064
Standard	        16864376


select * from dbo.Customer_Data2


***Top 3 Regions By Subcription Cancelation***

Select TOP 3 Region,
Count(*) AS [Subscription Canceled]
From dbo.Customer_Data2
Where Canceled = 'TRUE'
Group By Region
Order By [Subscription Canceled] DESC;


Region	Subscription Canceled
North	5067
South	5064
West	5044

select * from dbo.Customer_Data2


***Total Number of Active and Canceled Subscriptions***

Select Canceled, COUNT(*) AS [Total Subscriptions]
From dbo.Customer_Data2
Group By Canceled

select * from dbo.Customer_Data2



# Further Analysis Using PowerBI

![Customer Data--Capstone](https://github.com/user-attachments/assets/c37845d1-91b9-47c4-b8ac-f1531b3cd8e0)













