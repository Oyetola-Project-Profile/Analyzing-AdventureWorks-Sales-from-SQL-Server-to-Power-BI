

use AdventureWorks2017;
go


/*The following objects were created in the scripts below and used for the analysis in Power BI*/
select  * from Person.CityStateProviceCountry
Select  * from Sales.SalesDetailsSalesPerson
Select  * from Sales.SalesDetailsOnlineSales
select  * from Sales.IndividualCustomer
select  * from Production.VwProduct
select  * from Sales.VwSalesDetails
select  * from sales.vSalesPerson --This View comes with AdventureWorks 2017 


/*Sales.SalesDetailsSalesPerson
  Sales.SalesDetailsOnlineSales   
  

I Created a fact VIEW for Sales details. This is later split into sales from SalesPerson
(Sales.SalesDetailsSalesPerson) and Online Sales (Sales.SalesDetailsOnlineSales) using CTEs*/

create View Sales.VwSalesDetails
as
select sod.SalesOrderID,soh.CustomerID, sc.PersonID, soh.SalesPersonID, soh.TerritoryID,pa.PostalCode, 
sod.ProductID, sod.OrderQty, sod.UnitPrice, sod.LineTotal, soh.TaxAmt, soh.Freight,soh.SubTotal, 
soh.TotalDue, soh.[Status], soh.OrderDate, soh.DueDate, soh.ShipDate
from sales.SalesOrderDetail as sod
join sales.SalesOrderHeader as soh 
on sod.SalesOrderID = soh.SalesOrderID
join sales.customer as sc
on sc.customerid = soh.customerid
join Person.[Address] as pa
on pa.AddressID = soh.ShipToAddressID;
go


/*Below is a table created from the output of a CTE for sales created by SalesPersons,
Totalling 60,919 records   */

With CTE_SalesPerson as(
select sod.SalesOrderID,soh.CustomerID, sc.PersonID, soh.SalesPersonID, soh.TerritoryID,pa.PostalCode, 
sod.ProductID, sod.OrderQty, sod.UnitPrice, sod.LineTotal, soh.TaxAmt, soh.Freight,soh.SubTotal, 
soh.TotalDue, soh.[Status], soh.OrderDate, soh.DueDate, soh.ShipDate
from sales.SalesOrderDetail as sod
join sales.SalesOrderHeader as soh 
on sod.SalesOrderID = soh.SalesOrderID
join sales.customer as sc
on sc.customerid = soh.customerid
join Person.[Address] as pa
on pa.AddressID = soh.ShipToAddressID
where soh.salespersonid is not null)
Select * into Sales.SalesDetailsSalesPerson from CTE_SalesPerson;
go


/*Below is a table created using the result of a CTE for sales created without any SalesPersons,
Totalling 60,398 records suggestive online transactions */

with CTE_OnlineSales AS(
select sod.SalesOrderID,soh.CustomerID, sc.PersonID, soh.SalesPersonID, soh.TerritoryID,pa.PostalCode, 
sod.ProductID, sod.OrderQty, sod.UnitPrice, sod.LineTotal, soh.TaxAmt, soh.Freight,soh.SubTotal, 
soh.TotalDue, soh.[Status], soh.OrderDate, soh.DueDate, soh.ShipDate
from sales.SalesOrderDetail as sod
join sales.SalesOrderHeader as soh 
on sod.SalesOrderID = soh.SalesOrderID
join sales.customer as sc
on sc.customerid = soh.customerid
join Person.[Address] as pa
on pa.AddressID = soh.ShipToAddressID
where soh.salespersonid is null)
Select * into Sales.SalesDetailsOnlineSales from CTE_OnlineSales;
go


/*NOTE about the two tables below:
SalesOrderHeader contains unique saleorderID which appears once in the table (totalling 31,465).
However, these SalesOrderIDs appear multiple times in SalesOrderDetail (totalling 121,317)*/

select * from Sales.SalesOrderDetail --This View comes with AdventureWorks 2017
select * from Sales.SalesOrderHeader --This View comes with AdventureWorks 2017


/*Person.CityStateProviceCountry 

-The table Person.CityStateProviceCountry was created from the view Person.VwCityStateProviceCountry.
-The view was created to have postal code, city, stateProviceName and CountryRegionName.
-It returned 683 records, but had 23 duplicate records based on the PostalCode.
-UPDATE on the view is impossible because it is a mulitple-table View, 
-Now it has been persisted by creating a table from the view using the SELECT INTO statement as seen below*/

Create view  Person.VwCityStateProviceCountry
AS
Select distinct (pa.PostalCode),pa.StateProvinceID, pa.City,  ps.StateProvinceName, 
ps.StateProvinceCode,ps.CountryRegionName, ps.CountryRegionCode, ps.TerritoryID
from Person.[Address] as pa
join Person.vStateProvinceCountryRegion as ps
on pa.StateProvinceID = ps.StateProvinceID;
go


select * into Person.CityStateProviceCountry from Person.VwCityStateProviceCountry;
go


/*
-The underlisted 23 update statements are to edit (add an extra character) 
 duplicate PostalCode.
-This is necessary in order to have unique values and create a one to many relationship*/

update	Person.CityStateProviceCountry
set Postalcode = '2036a' where Postalcode='2036' and City= 'Matraville '	
	
update	Person.CityStateProviceCountry
set Postalcode = '2113a' where Postalcode='2113' and City= 'North Ryde'	
	
update	Person.CityStateProviceCountry
set Postalcode = '12171a' where Postalcode='12171' and StateProvinceName= 'Saarland'	
	
update	Person.CityStateProviceCountry
set Postalcode = '12311a' where Postalcode='12311' and StateProvinceName= 'Saarland'	
	
update	Person.CityStateProviceCountry
set Postalcode = '14111a' where Postalcode='14111' and StateProvinceName= 'Hamburg'	
	
update	Person.CityStateProviceCountry
set Postalcode = '14197a' where Postalcode='14197' and StateProvinceName= 'Saarland'	
	
update	Person.CityStateProviceCountry
set Postalcode = '14197b' where Postalcode='14197' and StateProvinceName= 'Brandenburg'	
	
update	Person.CityStateProviceCountry
set Postalcode = '48001a' where Postalcode='48001' and City= 'Münster'	
	
update	Person.CityStateProviceCountry
set Postalcode = '53131a' where Postalcode='53131' and StateProvinceName= 'Nordrhein-Westfalen'	
	
update	Person.CityStateProviceCountry
set Postalcode = '63103a' where Postalcode='63103' and City= 'St. Louis'	
	
update	Person.CityStateProviceCountry
set Postalcode = '63151a' where Postalcode='63151' and City= 'Mühlheim'	
	
update	Person.CityStateProviceCountry
set Postalcode = '75006a' where Postalcode='75006' and City= 'Carrollton'	
	
update	Person.CityStateProviceCountry
set Postalcode = '80074a' where Postalcode='80074' and StateProvinceName= 'Hessen'	
	
update	Person.CityStateProviceCountry
set Postalcode = '80074b' where Postalcode='80074' and StateProvinceName= 'Hamburg'	
	
update	Person.CityStateProviceCountry
set Postalcode = '86171a' where Postalcode='86171' and City= 'Ascheim'	
	
update	Person.CityStateProviceCountry
set Postalcode = '91941a' where Postalcode='91941' and City= 'Grossmont'	
	
update	Person.CityStateProviceCountry
set Postalcode = '91950a' where Postalcode='91950' and City= 'National City'	
	
update	Person.CityStateProviceCountry
set Postalcode = '98201a' where Postalcode='98201' and StateProvinceName = 'Montana'

update	Person.CityStateProviceCountry
set Postalcode = '98272a' where Postalcode='98272' and StateProvinceName= 'Washington'	

update	Person.CityStateProviceCountry
set Postalcode = 'OX14 4SEa' where Postalcode='OX14 4SE' and City= 'Oxford'	
	
update	Person.tblCityStateProviceCountry
set Postalcode = 'V6B 3P7a' where Postalcode='V6B 3P7' and City= 'Port Hammond'	
	
update	Person.CityStateProviceCountry
set Postalcode = 'V7L 4J4a' where Postalcode='V7L 4J4' and City= 'N. Vancouver'	
	

update	Person.CityStateProviceCountry
set Postalcode = 'V9a' where Postalcode='V9' and City= 'Langford'	
	
	
--Checking the update was sucessful 	
select  * from Person.CityStateProviceCountry 	
where postalcode like  '982%'		
	
--Checking the update was sucessful 	
select  * from Person.CityStateProviceCountry 	
where postalcode like '1217%'	




/*Sales.IndividualCustomer

-The table Sales.IndividualCustomer was created from the view Sales.vIndividualCustomer 
(which comes with AdventureWorks2017) using the 'Select Into'.

-It was necessary to take out duplicate record. There were 24 duplicated records
with same customers appearing in both 'home' and 'shipping' ADDRESSTYPE, now removed.

-While attempting to update the view the message below came up thus necessitating
the creation of the table Sales.IndividualCustomer.

Msg 4405, Level 16, State 1, Line 126
View or function 'Sales.vIndividualCustomer' 
is not updatable because the modification affects multiple base tables.*/

select * into Sales.IndividualCustomer from Sales.vIndividualCustomer;
go


--Below are the duplicated customers deleted
delete from Sales.IndividualCustomer				
where BusinessEntityID = 2996 and  AddressLine1 = '9187 Vista Del Sol'				
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 4073 and  AddressLine1 = '4293 Concord Ct.'				
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 4388	and  AddressLine1 = '3858 Vista Diablo'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 5124	and  AddressLine1 = '4039 Elkwood Dr.'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 5479	and  AddressLine1 = '3993 Jabber Place'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 5561	and  AddressLine1 = '1261 Viking Drive'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 5668	and  AddressLine1 = '3141 Jabber Place'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 5976	and  AddressLine1 = '2238 Pine Street'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 8892	and  AddressLine1 = '7779 Merry Drive'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 9196	and  AddressLine1 = '5509 Newcastle Road'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 10781	and  AddressLine1 = '5165 Cambridge Drive'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 11072	and  AddressLine1 = '3443 Centennial Way'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 11625	and  AddressLine1 = '6437 Brookview Dr.'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 15073	and  AddressLine1 = '6900 Bellord Ct.'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 16746	and  AddressLine1 = '8486 Hazelwood Lane'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 17243	and  AddressLine1 = '521 Hermosa'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 17298	and  AddressLine1 = '1946 Bayside Way'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 17400	and  AddressLine1 = '7057 Striped Maple Court'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 17691	and  AddressLine1 = '769 Algiers Drive'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 20099	and  AddressLine1 = '7432 Corte Valencia'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 20305	and  AddressLine1 = '3175 Olivera Rd.'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 20419	and  AddressLine1 = '2701 Sierra Rd'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 20550	and  AddressLine1 = '6036 Park Glenn'			
				
delete from Sales.IndividualCustomer				
where BusinessEntityID = 20759	and  AddressLine1 = '6351 22nd Ave.'			




/*Production.VwProduct 

Create a VIEW for Product*/
Create View Production.VwProduct

As

select ProductID,[name],StandardCost, ListPrice, Color, ProductLine,
Case 
	when MakeFlag = 0
	then 'Purchased Material'
	else 'Manufactured in House'
End as MaterialMakeFlag, 
Case 
	when FinishedGoodsFlag = 0 
	then 'Product Not Saleable' 
	else 'Product is Saleable' 
End as finishGoodStatus
from Production.Product;
go


/* OTHER NOTES ON THE DATABASE ARE BELOW */

/*Need to make a nested CASE statement for ProductLine column in
Production.VwProduct or it can be done in Power Query using 
"Replace Values"*/
R = Road, M = Mountain, T = Touring, S = [Standard]



/*There is a link between Sales.SalesOrderHeader and Sales.SalesOrderID. 
Not just in terms of the key, but also the summation of 'Sales.SalesOrderID.LineTotal' 
is in 'Sales.SalesOrderHeader.SubTotal'*/
Declare @orderID as int 
set @orderID = 43664 --get figure from Sales.SalesOrderHeader.SalesOrderID
select  * from Sales.SalesOrderDetail where SalesOrderID = @orderID
select CONCAT('OrderID',' ', @orderID,' ', 'has',' ', COUNT(salesorderID),' ', 
	'transactions totalling',' ',ROUND(sum(LineTotal),2),' ','as seen in SubTotal column') 
from Sales.SalesOrderDetail 
where SalesOrderID = @orderID 
select SalesOrderID,SubTotal,TaxAmt,Freight,TotalDue 
from Sales.SalesOrderHeader where SalesOrderID = @orderID;
go


--Decoding the meaning PersonType CHECK constraint in Person.Person
Primary type of person: 
SC = Store Contact, 
IN = Individual (retail) customer, 
SP = Sales person, 
EM = Employee (non-sales), 
VC = Vendor contact, 
GC = General contact



--Decoding the STATUS column on the sales.salesOrderHeader is as follows:
Order current status. 
1 = In process; 
2 = Approved; 
3 = Backordered; 
4 = Rejected; 
5 = Shipped; 
6 = Cancelled


--Decoding the OnlineOrderFlag column in sales.SalesOrderHeader
sales.SalesOrderHeader.OnlineOrderFlag
0 = [Order] placed [by] sales person. 
1 = [Order] placed [online by] customer.
