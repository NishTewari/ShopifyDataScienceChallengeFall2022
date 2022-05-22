# Shopify Data Science Challenge Fall 2022

Fall 2022 Data Science Intern Challenge can be found here: https://docs.google.com/document/d/1JxYz-VZHIctOQcw1PIUvCuYouxDWnew5yzBhluVwbso/edit#

This repo is my submission for Shopify Data Science Intern Application for Fall 2022


### Question 1




### Question 2
a. How many orders were shipped by Speedy Express in total?
```
SELECT COUNT(OrderID) FROM Orders Orders
LEFT JOIN Shippers Ship ON Orders.ShipperID = Ship.ShipperID
WHERE Ship.ShipperName = 'Speedy Express';
```

[Result:](https://github.com/NishTewari/ShopifyDataScienceChallengeFall2022/blob/main/Shopify%20Data%20Science%20Challenge/Question%202%20-%20Part%201.png) 54 Orders were shipped by Speedy Express!  

b. What is the last name of the employee with the most orders? 
```
SELECT Employees.LastName, Count(Orders.OrderID) As NumberOfOrders FROM Orders
LEFT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY LastName
ORDER BY NumberOfOrders Desc
limit 1;
```

[Result:](https://github.com/NishTewari/ShopifyDataScienceChallengeFall2022/blob/main/Shopify%20Data%20Science%20Challenge/Question%202%20-%20Part%202.png) Last Name, "Peacock" has the most orders of 40!

c. What product was ordered the most by customers in Germany?
```

```
Result: 
