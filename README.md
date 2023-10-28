# task_3
SELECT C.FirstName, C.LastName
FROM Customers C
JOIN (
    SELECT o.CustomerID
    FROM Orders o
    GROUP BY o.CustomerID
    ORDER BY SUM(o.TotalAmount)     
    LIMIT 1
) top ON C.CustomerID = top.CustomerID;

select c.CustomerID, c.FirstName, c.LastName, c.Email, o.OrderID, sum(o.TotalAmount) as TotalAmount
from customers c
left join Orders o on c.CustomerID = o.CustomerID
group by c.CustomerID, c.FirstName, c.LastName, c.Email, o.OrderID
order by TotalAmount desc;

SELECT c.CustomerID, c.FirstName, c.LastName, c.Email, SUM(o.TotalAmount) AS TotalOrderAmount
FROM customers c
JOIN orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.FirstName, c.LastName, c.Email
HAVING SUM(o.TotalAmount) > (
    SELECT AVG(TotalAmount)
    FROM orders
);
