# Analyzing-AdventureWorks-Sales-from-SQL-Server-to-Power-BI
This project demonstrates the use of SQL and Power BI to gain insight into microsoft AdventureWorks sales.

The script folder in this repository holds all the t-sql code written to create the follwing charts in Power BI


Tools:  T-SQL, Views & CTEs, Data Cleaning, Power BI, Data Modeling
Key achievements:
•	Designed an end-to-end analytics report using SQL Server and Power BI to analyze 120K+ sales transaction records.
•	Built a fact view (Sales.VwSalesDetails) by joining SalesOrderHeader, SalesOrderDetail, Customer, and Address tables.
•	Split fact data into SalesDetailsSalesPerson (60,919 rows) and SalesDetailsOnlineSales (60,398 rows) using CTEs.
•	Created and persisted supporting dimension tables including:
o	Person.CityStateProvinceCountry (cleaned 23 duplicate postal codes using update statement)
o	Sales.IndividualCustomer (removed 24 duplicate records caused by multi-address entries)
o	Production.VwProduct (added CASE logic for material and finished-goods classification)
•	Modeled the data in Power BI and built dashboards to track:
o	Sales by channel (Salesperson vs. Online)
o	Sales by product, region, and salesperson
o	Order status breakdown (In Process, Approved, Backordered, Shipped, etc.)
•	Ensured referential integrity between location, product, customer, and sales tables by resolving duplicated and mismatched keys.  

Skills demonstrated:
SQL data modeling, view creation, CTE design, data cleaning, dimension/fact structuring, handling duplicates, building relational models, Power BI report development, KPI creation.

![Decompose tree](https://github.com/Oyetola-Project-Profile/Analyzing-AdventureWorks-Sales-from-SQL-Server-to-Power-BI/blob/main/images/AdventureWorks%20decompose%20tree.PNG)

![Bar chart](https://github.com/Oyetola-Project-Profile/Analyzing-AdventureWorks-Sales-from-SQL-Server-to-Power-BI/blob/main/images/AdventureWorks%20bar%20chart.PNG) 

![Pie chatt](https://github.com/Oyetola-Project-Profile/Analyzing-AdventureWorks-Sales-from-SQL-Server-to-Power-BI/blob/main/images/AdventureWorks%20piechart.PNG)




<details>
<summary>Click to expand</summary>
[This project was done in 2022](https://github.com/OyetolaAppdb/datasharing/tree/master)
</details>
