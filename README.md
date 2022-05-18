## Fall 2022 Data Science Intern Challenge 
Kaye Thinh-To
### Question 1: <br>
<br>

*[link](https://docs.google.com/spreadsheets/d/1ZIxs0CQS_7St7su8PKI7G-wd7cq8ktT8j4Jq55s_piU/edit?usp=sharing) to modified excel spreadsheet (calculations on lines 5003-5007).*<br>

**a.** In the initial analysis of average order value (AOV), the average amount was computed to be $3145.13. This was calculated by simply taking the sum of all orders and dividing it by the number of orders. 
<br><br>
*These are the hypothesized Excel Formulas used to compute the initial AOV:*
> =SUM(D2:D5001) <br> =DIVIDE(D5003, 5000), which calculated $3145.128

<br>

However, this amount does not take into account the value of each shoe sold at a given store along with the quantity of shoes purchased per order. This results in outliers that ultimately skew the data. 

<br>

For example, order #4869 on row 4870 purchased 2000 shoes resulting in an order costing 704000. Not normalizing these values and taking into account the number of shoes is my hypothesized thought as to why the initial AOV calculation was larger than expected. 

<br>

Therefore, a better way to evaluate this data would be to normalize the data by calculating average value of each order by dividing order total by total items, and then taking the average of all averaged order amounts. 

<br>

*This is more accurate way of calculating AOV:*

> I created a new column, G for avg_amt_per_item and applied <br>
=DIVIDE(Dxxx, Exxx)<br>
=AVERAGE(G2:G5001), which calculated $387.7428 as the new AOV 

<br>

**b.** A better metric to determine Average Order Value would be to take the average cost of a shoe per order 

<br>

**c.** Therefore, the new calculated AOV is **$387.74**

<br>

### Question 2: <br>
<br>

*Answers based on [this](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) dataset.*

**a.** 54 orders were shipped by Speedy Express in total 
```SQL
SELECT COUNT(*)
FROM Orders
LEFT JOIN Shippers 
ON Orders.ShipperID = Shippers.ShipperID 
WHERE Shippers.SHipperName = "Speedy Express"
```
<br>

**b.** The last name of the employee with the most orders is Peacock
```SQL
SELECT Orders.EmployeeID,Employees.LastName, COUNT(*) as Total_Orders
FROM Orders
LEFT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID 
GROUP BY Orders.EmployeeID, Employees.LastName
ORDER BY Total_Orders DESC
LIMIT 1;
```
<br>

**c.** The product that was ordered by the most customers was Gorgonzola Telino
```SQL
SELECT Products.ProductID,Products.ProductName, COUNT(*) total_orders
FROM Orders, OrderDetails, Products, Customers 
WHERE (Orders.OrderID = OrderDetails.OrderID) AND
(OrderDetails.ProductID = Products.ProductID) AND 
(Orders.CustomerID = Customers.CustomerID) AND 
(Customers.Country = "Germany")
GROUP BY Products.ProductID, Products.ProductName 
ORDER BY total_orders DESC
LIMIT 1
```
