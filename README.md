# Shopify Data Science Challenge Fall 2022

Fall 2022 Data Science Intern Challenge can be found here: https://docs.google.com/document/d/1JxYz-VZHIctOQcw1PIUvCuYouxDWnew5yzBhluVwbso/edit#

This repo is my submission for Shopify Data Science Intern Application for Fall 2022


### Question 1 - a
Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

Basically what shopify has done here is taken the total sum of all order_amounts and divided by 5000. 
The reason its being divided by 5000 is because that is the total number of rows within the dataset.

The problem with doing this is that orders can have multiple items. For example, lets take a closer look at row 60 below
```
print(dataset.loc[[60]])

    order_id  shop_id  user_id  order_amount  total_items payment_method  \
60        61       42      607        704000         2000    credit_card   

            created_at  
60  2017-03-04 4:00:00  
```
It is clear that this order_id contains 2000 items. Shopify has assumed that each order_id contains a single item which led 
to them calculating the AOV. However, there are 2000 items within a single order of this order_id

### Question 1 - b
What metric would you report for this dataset?

We know that AOV = Total Revenue / Total Orders
The optimal solution for this would be to calculate the Average Revenue Per Item (ARI)

ARI = Total order amount / Total items 

We can take a look at the first 2 rows in the dataset to see what shopify did vs the metric i will be using 
```
How shopify calcuated their AOV?
(224 + 90) / 2 = 157 (AOV)

ARI Metric Calculation 
(224 + 90) / 3 = 104.67 (ARI)

This is because we have to take in consideration of the 2 items within order_id 1 

print(dataset.loc[[0]])
print(dataset.loc[[1]])

  order_id  shop_id  user_id  order_amount  total_items payment_method  \
0         1       53      746           224            2           cash   

            created_at  
0  2017-03-13 12:36:56  
   order_id  shop_id  user_id  order_amount  total_items payment_method  \
1         2       92      925            90            1           cash   

            created_at  
1  2017-03-03 17:38:52  
```
### Question 1 - c
What is its value?

Let's calculate the Avg Revenue Per Item (ARI) for the entire dataset provided.

ARI = Total order amount / Total items

```
print("Average Revenue Per Item (ARI):", dataset['order_amount'].sum()/dataset['total_items'].sum())

Average Revenue Per Item (ARI): 357.92152221412965
```
Therefore, the ARI for the dataset is $357.92


### Question 2 - a
How many orders were shipped by Speedy Express in total?
```
SELECT COUNT(OrderID) FROM Orders Orders
LEFT JOIN Shippers Ship ON Orders.ShipperID = Ship.ShipperID
WHERE Ship.ShipperName = 'Speedy Express';
```

[Result:](https://github.com/NishTewari/ShopifyDataScienceChallengeFall2022/blob/main/Shopify%20Data%20Science%20Challenge/Question%202%20-%20Part%201.png) 54 Orders were shipped by Speedy Express!  

### Question 2 - b
What is the last name of the employee with the most orders? 
```
SELECT Employees.LastName, Count(Orders.OrderID) As NumberOfOrders FROM Orders
LEFT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY LastName
ORDER BY NumberOfOrders Desc
limit 1;
```

[Result:](https://github.com/NishTewari/ShopifyDataScienceChallengeFall2022/blob/main/Shopify%20Data%20Science%20Challenge/Question%202%20-%20Part%202.png) Last Name, "Peacock" has the most orders of 40!

### Question 2 - c
What product was ordered the most by customers in Germany?
```
SELECT sum(Quantity) AS TotalOrders, ProductName
FROM OrderDetails
JOIN Orders ON OrderDetails.OrderID = Orders.OrderID
JOIN Customers ON Orders.CustomerID = Customers.CustomerID
JOIN Products ON OrderDetails.ProductID = Products.ProductID
WHERE Customers.Country = 'Germany'
GROUP BY OrderDetails.ProductID
ORDER BY sum(OrderDetails.Quantity) DESC
limit 1;
```
[Result:](https://github.com/NishTewari/ShopifyDataScienceChallengeFall2022/blob/main/Shopify%20Data%20Science%20Challenge/Question%202%20-%20Part%203.png) Boston Crab Meat was ordered the most by Customers in Germany at a total of 160 Orders! 
