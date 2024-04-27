| **Inicio**            | **atrás 21**                |
| --------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./21_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                              |
| ------------------------------------------------------------------------------------ |
| [211. Ejercicio de SQL Server Basico](#211-ejercicio-de-sql-server-basico)           |
| [212. Ejercicios de SQL Server Intermedio](#212-ejercicios-de-sql-server-intermedio) |
| [213. Ejercicios de SQL Server Avanzado](#213-ejercicios-de-sql-server-avanzado)     |

---

# **Tutorial de SQL**

Ejemplo con la base de datos SQL llamado [northwind](../../Data/northwind.sql)

## **211. Ejercicio de SQL Server Basico**

1. **Obtén una lista de todos los productos de la tabla "Products".**

`SELECT * FROM Products;`

2. **Obtén una lista de todos los clientes de la tabla "Customers" que se encuentren en el país 'Germany'.**

`SELECT * FROM Customers WHERE Country = 'Germany';`

3. **Obtén la cantidad total de productos en stock de la tabla "Products".**

`SELECT SUM(UnitsInStock) AS TotalStock FROM Products;`

4. **Obtén una lista de todos los empleados de la tabla "Employees" que hayan nacido antes del 1 de enero de 1970.**

`SELECT * FROM Employees WHERE BirthDate < '1970-01-01';`

5. **Obtén la cantidad total de pedidos de la tabla "Orders".**

`SELECT COUNT(*) AS TotalOrders FROM Orders;`

6. **Obtén una lista de todos los productos de la tabla "Products" ordenados de forma descendente por su precio.**

`SELECT * FROM Products ORDER BY UnitPrice DESC;`

7. **Obtén la suma total de los valores de los pedidos de la tabla "Orders".**

`SELECT SUM(OrderID) AS TotalValue FROM Orders;`

8. **Obtén una lista de todos los clientes de la tabla "Customers" que tengan un cargo de contacto.**

`SELECT * FROM Customers WHERE ContactTitle LIKE '%Marketing%';`

9. **Obtén la cantidad total de productos agrupados por categoría de la tabla "Products".**

`SELECT CategoryID, COUNT(*) AS TotalProducts FROM Products GROUP BY CategoryID;`

10. **Obtén una lista de todos los empleados de la tabla "Employees" que hayan sido contratados en el año 1992.**

`SELECT * FROM Employees WHERE YEAR(HireDate) = 1992;`

11. **Obtén la cantidad total de productos en stock para cada proveedor de la tabla "Products".**

`SELECT SupplierID, SUM(UnitsInStock) AS TotalStock FROM Products GROUP BY SupplierID;`

12. **Obtén una lista de todos los pedidos de la tabla "Orders" que hayan sido enviados después del 1 de enero de 1998.**

`SELECT * FROM Orders WHERE ShippedDate > '1998-01-01';`

13. **Obtén la cantidad total de productos vendidos para cada empleado de la tabla "OrderDetails".**

`SELECT ProductID, SUM(Quantity) AS TotalSold FROM [Order Details] GROUP BY ProductID;`

14. **Obtén una lista de todos los clientes de la tabla "Customers" cuyo nombre de contacto empiece con la letra 'A'.**

`SELECT * FROM Customers WHERE ContactName LIKE 'A%';`

15. **Obtén la cantidad total de productos agrupados por categoría y proveedor de la tabla "Products".**

`SELECT CategoryID, SupplierID, COUNT(*) AS TotalProducts FROM Products GROUP BY CategoryID, SupplierID;`

16. **Obtén una lista de todos los empleados de la tabla "Employees" que sean hombres y vivan en USA.**

`SELECT * FROM Employees WHERE Gender = 'M' AND Country = 'USA';`

17. **Obtén la cantidad total de pedidos para cada cliente de la tabla "Orders".**

`SELECT CustomerID, COUNT(*) AS TotalOrders FROM Orders GROUP BY CustomerID;`

18. **Obtén una lista de todos los productos de la tabla "Products" cuya unidad de precio sea mayor que el promedio de todos los productos.**

`SELECT * FROM Products WHERE UnitPrice > (SELECT AVG(UnitPrice) FROM Products);`

19. **Obtén la cantidad total de productos vendidos para cada categoría de la tabla "OrderDetails".**

`SELECT ProductID, SUM(Quantity) AS TotalSold FROM [Order Details] GROUP BY ProductID;`

20. **Obtén una lista de todos los pedidos de la tabla "Orders" que hayan sido realizados por el empleado con ID 5.**

`SELECT * FROM Orders WHERE EmployeeID = 5;`

[🔼](#índice)

---

## **212. Ejercicios de SQL Server Intermedio**

---

1. **Encuentra el total de ventas realizadas por cada empleado en el año 1997.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName,
    SUM(od.Quantity * od.UnitPrice) AS TotalSales
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
    INNER JOIN [Order Details] AS od ON o.OrderID = od.OrderID
WHERE
    YEAR(o.OrderDate) = 1997
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName;
```

2. **Encuentra el cliente que ha realizado el mayor número de pedidos en total.**

```
SELECT TOP 1
    c.CustomerID,
    c.CompanyName,
    COUNT(o.OrderID) AS TotalOrders
FROM
    Customers AS c
    INNER JOIN Orders AS o ON c.CustomerID = o.CustomerID
GROUP BY
    c.CustomerID,
    c.CompanyName
ORDER BY
    TotalOrders DESC;

```

3. **Encuentra los cinco productos más vendidos en términos de cantidad y muestra su nombre y cantidad total vendida.**

```
SELECT TOP 5
    p.ProductName,
    SUM(od.Quantity) AS TotalQuantitySold
FROM
    Products AS p
    INNER JOIN [Order Details] AS od ON p.ProductID = od.ProductID
GROUP BY
    p.ProductName
ORDER BY
    TotalQuantitySold DESC;

```

4. **Encuentra los empleados que no han realizado ninguna venta en el año 1992.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName
FROM
    Employees AS e
WHERE
    e.EmployeeID NOT IN (
        SELECT
            o.EmployeeID
        FROM
            Orders AS o
        WHERE
            YEAR(o.OrderDate) = 1992
    );
```

5. **Encuentra los clientes que han realizado al menos un pedido en el año 1997 y al menos un pedido en el año 1998.**

```
SELECT
    c.CustomerID,
    c.CompanyName
FROM
    Customers AS c
    INNER JOIN Orders AS o ON c.CustomerID = o.CustomerID
WHERE
    YEAR(o.OrderDate) = 1997 OR YEAR(o.OrderDate) = 1998
GROUP BY
    c.CustomerID,
    c.CompanyName
HAVING
    COUNT(DISTINCT YEAR(o.OrderDate)) = 2;
```

6. **Encuentra el promedio de tiempo de envío de los pedidos para cada país.**

```
SELECT
    o.ShipCountry,
    AVG(DATEDIFF(DAY, o.OrderDate, o.ShippedDate)) AS AverageShippingTime
FROM
    Orders AS o
GROUP BY
    o.ShipCountry;
```

7. **Encuentra los productos que han sido ordenados pero no han sido enviados.**

```
SELECT
    p.ProductName
FROM
    Products AS p
    INNER JOIN [Order Details] AS od ON p.ProductID = od.ProductID
    INNER JOIN Orders AS o ON od.OrderID = o.OrderID
WHERE
    o.ShippedDate IS NULL;
```

8. **Encuentra los empleados que han atendido a clientes de más de un país y muestra su nombre y los países en los que han atendido clientes.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName,
    COUNT(DISTINCT c.Country) AS NumberOfCountries
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
    INNER JOIN Customers AS c ON o.CustomerID = c.CustomerID
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName
HAVING
    COUNT(DISTINCT c.Country) > 1;
```

9. **Encuentra los clientes que no han realizado ningún pedido.**

```
SELECT
    c.CustomerID,
    c.CompanyName
FROM
    Customers AS c
WHERE
    c.CustomerID NOT IN (
        SELECT
            o.CustomerID
        FROM
            Orders AS o
    );
```

10. **Encuentra los empleados que han realizado al menos un pedido en el año 1997 y han atendido a clientes de más de un país.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
    INNER JOIN Customers AS c ON o.CustomerID = c.CustomerID
WHERE
    YEAR(o.OrderDate) = 1997
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName
HAVING
    COUNT(DISTINCT c.Country) > 1;
```

11. **Encuentra el promedio de unidades vendidas por producto y categoría.**

```
SELECT
    p.CategoryID,
    c.CategoryName,
    AVG(od.Quantity) AS AverageUnitsSold
FROM
    Products AS p
    INNER JOIN [Order Details] AS od ON p.ProductID = od.ProductID
    INNER JOIN Categories AS c ON p.CategoryID = c.CategoryID
GROUP BY
    p.CategoryID,
    c.CategoryName;
```

12. **Encuentra los productos que no han sido vendidos en el año 1997.**

```
SELECT
    p.ProductID,
    p.ProductName
FROM
    Products AS p
    LEFT JOIN [Order Details] AS od ON p.ProductID = od.ProductID
    LEFT JOIN Orders AS o ON od.OrderID = o.OrderID
WHERE
    YEAR(o.OrderDate) <> 1997 OR o.OrderDate IS NULL;
```

13. **Encuentra el cliente que ha realizado el pedido de mayor valor total.**

```
SELECT TOP 1
    c.CustomerID,
    c.CompanyName,
    SUM(od.Quantity * od.UnitPrice) AS TotalOrderValue
FROM
    Customers AS c
    INNER JOIN Orders AS o ON c.CustomerID = o.CustomerID
    INNER JOIN [Order Details] AS od ON o.OrderID = od.OrderID
GROUP BY
    c.CustomerID,
    c.CompanyName
ORDER BY
    TotalOrderValue DESC
LIMIT 1;
```

14. **Encuentra el empleado que ha realizado el mayor número de ventas en términos de cantidad de productos vendidos.**

```
SELECT TOP 1
    e.EmployeeID,
    e.FirstName,
    e.LastName,
    SUM(od.Quantity) AS TotalProductsSold
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
    INNER JOIN [Order Details] AS od ON o.OrderID = od.OrderID
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName
ORDER BY
    TotalProductsSold DESC
```

15. **Encuentra los productos que han sido vendidos más de una vez y muestra su nombre y cantidad total vendida.**

```
SELECT
    p.ProductName,
    SUM(od.Quantity) AS TotalQuantitySold
FROM
    Products AS p
    INNER JOIN [Order Details] AS od ON p.ProductID = od.ProductID
GROUP BY
    p.ProductName
HAVING
    COUNT(od.OrderID) > 1;
```

16. **Encuentra los empleados que han realizado ventas en todos los años disponibles en la base de datos y muestra su nombre.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName
HAVING
    COUNT(DISTINCT YEAR(o.OrderDate)) = (
        SELECT
            COUNT(DISTINCT YEAR(OrderDate))
        FROM
            Orders
    );
```

17. **Encuentra los clientes que han realizado al menos dos pedidos en un mismo día y muestra su nombre.**

```
SELECT
    c.CustomerID,
    c.CompanyName
FROM
    Customers AS c
    INNER JOIN Orders AS o ON c.CustomerID = o.CustomerID
WHERE
    o.OrderDate IN (
        SELECT
            OrderDate
        FROM
            Orders
        GROUP BY
            OrderDate
        HAVING
            COUNT(OrderID) >= 2
    )
GROUP BY
    c.CustomerID,
    c.CompanyName;
```

18. **Encuentra los productos que han sido ordenados más de una vez por el mismo cliente y muestra su nombre y la cantidad total ordenada.**

```
SELECT
    p.ProductName,
    SUM(od.Quantity) AS TotalOrderedQuantity
FROM
    Products AS p
    INNER JOIN [Order Details] AS od ON p.ProductID = od.ProductID
WHERE
    od.OrderID IN (
        SELECT
            OrderID
        FROM
            [Order Details]
        GROUP BY
            OrderID
        HAVING
            COUNT(DISTINCT ProductID) > 1
    )
GROUP BY
    p.ProductName;
```

19. **Encuentra los clientes que han realizado pedidos en todos los países disponibles en la base de datos y muestra su nombre.**

```
SELECT
    c.CustomerID,
    c.CompanyName
FROM
    Customers AS c
    INNER JOIN Orders AS o ON c.CustomerID = o.CustomerID
GROUP BY
    c.CustomerID,
    c.CompanyName
HAVING
    COUNT(DISTINCT o.ShipCountry) = (
        SELECT
            COUNT(DISTINCT ShipCountry)
        FROM
            Orders
    );
```

20. **Encuentra los empleados que han realizado ventas en cada mes del año 1997 y muestra su nombre.**

```
SELECT
    e.EmployeeID,
    e.FirstName,
    e.LastName
FROM
    Employees AS e
    INNER JOIN Orders AS o ON e.EmployeeID = o.EmployeeID
WHERE
    YEAR(o.OrderDate) = 1997
GROUP BY
    e.EmployeeID,
    e.FirstName,
    e.LastName
HAVING
    COUNT(DISTINCT MONTH(o.OrderDate)) = 12;
```

[🔼](#índice)

---

## **213. Ejercicios de SQL Server Avanzado**

---

1. **Encuentra el promedio de las ventas diarias de cada mes en la tabla "Orders". Muestra el resultado ordenado por mes de forma ascendente.**

```
SELECT MONTH(OrderDate) AS Mes, AVG(Freight) AS PromedioVentasDiarias
FROM Orders
GROUP BY MONTH(OrderDate)
ORDER BY Mes ASC;
```

2. **Encuentra el empleado que ha realizado la mayor cantidad de ventas en total. Muestra el resultado con el nombre del empleado y el total de ventas.**

```
SELECT TOP 1 e.FirstName + ' ' + e.LastName AS Empleado, COUNT(*) AS TotalVentas
FROM Orders o
JOIN Employees e ON o.EmployeeID = e.EmployeeID
GROUP BY e.EmployeeID, e.FirstName, e.LastName
ORDER BY TotalVentas DESC;
```

3. **Encuentra el país que ha realizado el mayor número de pedidos. Muestra el resultado con el nombre del país y el total de pedidos.**

```
SELECT TOP 1 c.Country AS Pais, COUNT(*) AS TotalPedidos
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY c.Country
ORDER BY TotalPedidos DESC;
```

4. **Encuentra los cinco productos más vendidos en términos de cantidad. Muestra el resultado con el nombre del producto y la cantidad vendida.**

```
SELECT TOP 5 p.ProductName AS Producto, SUM(od.Quantity) AS CantidadVendida
FROM [Order Details] od
JOIN Products p ON od.ProductID = p.ProductID
GROUP BY p.ProductID, p.ProductName
ORDER BY CantidadVendida DESC;
```

5. **Encuentra el año con el mayor número de pedidos realizados. Muestra el resultado con el año y el total de pedidos.**

```
SELECT YEAR(OrderDate) AS Año, COUNT(*) AS TotalPedidos
FROM Orders
GROUP BY YEAR(OrderDate)
ORDER BY TotalPedidos DESC;
```

6. **Encuentra los clientes que hayan realizado al menos un pedido en cada año. Muestra el resultado con el nombre del cliente y el número de años en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT YEAR(o.OrderDate)) AS AñosPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT YEAR(o.OrderDate)) = (SELECT COUNT(DISTINCT YEAR(OrderDate)) FROM Orders);
```

7. **Encuentra los empleados que hayan realizado al menos un pedido en cada mes. Muestra el resultado con el nombre del empleado y el número de meses en los que ha realizado pedidos.**

```
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS Empleado, COUNT(DISTINCT MONTH(o.OrderDate)) AS MesesPedidos
FROM Employees e
JOIN Orders o ON e.EmployeeID = o.EmployeeID
GROUP BY e.EmployeeID, e.FirstName, e.LastName
HAVING COUNT(DISTINCT MONTH(o.OrderDate)) = 12;
```

8. **Encuentra los clientes que hayan realizado al menos un pedido en cada trimestre. Muestra el resultado con el nombre del cliente y el número de trimestres en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT DATEPART(QUARTER, o.OrderDate)) AS TrimestresPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT DATEPART(QUARTER, o.OrderDate)) = 4;
```

9. **Encuentra los empleados que hayan realizado al menos un pedido en cada ciudad donde hay clientes. Muestra el resultado con el nombre del empleado y el número de ciudades en las que ha realizado pedidos.**

```
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS Empleado, COUNT(DISTINCT c.City) AS CiudadesPedidos
FROM Employees e
JOIN Orders o ON e.EmployeeID = o.EmployeeID
JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY e.EmployeeID, e.FirstName, e.LastName
HAVING COUNT(DISTINCT c.City) = (SELECT COUNT(DISTINCT City) FROM Customers);
```

10. **Encuentra los clientes que hayan realizado pedidos en todos los países donde hay clientes. Muestra el resultado con el nombre del cliente y el número de países en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT co.Country) AS PaisesPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN Customers co ON o.CustomerID = co.CustomerID
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT co.Country) = (SELECT COUNT(DISTINCT Country) FROM Customers);
```

11. **Encuentra los productos que hayan sido pedidos al menos una vez por cada empleado. Muestra el resultado con el nombre del producto y el número de empleados que lo han pedido.**

```
SELECT p.ProductID, p.ProductName AS Producto, COUNT(DISTINCT e.EmployeeID) AS EmpleadosPedidos
FROM Products p
JOIN [Order Details] od ON p.ProductID = od.ProductID
JOIN Orders o ON od.OrderID = o.OrderID
JOIN Employees e ON o.EmployeeID = e.EmployeeID
GROUP BY p.ProductID, p.ProductName
HAVING COUNT(DISTINCT e.EmployeeID) = (SELECT COUNT(*) FROM Employees);
```

12. **Encuentra los clientes que hayan realizado un pedido en todos los años disponibles en la base de datos. Muestra el resultado con el nombre del cliente y el número de años en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT YEAR(o.OrderDate)) AS AñosPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT YEAR(o.OrderDate)) = (SELECT COUNT(DISTINCT YEAR(OrderDate)) FROM Orders);
```

13. **Encuentra los empleados que hayan realizado pedidos en todos los meses del año actual. Muestra el resultado con el nombre del empleado y el número de meses en los que ha realizado pedidos.**

```
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS Empleado, COUNT(DISTINCT MONTH(o.OrderDate)) AS MesesPedidos
FROM Employees e
JOIN Orders o ON e.EmployeeID = o.EmployeeID
WHERE YEAR(o.OrderDate) = YEAR(GETDATE())
GROUP BY e.EmployeeID, e.FirstName, e.LastName
HAVING COUNT(DISTINCT MONTH(o.OrderDate)) = (SELECT COUNT(DISTINCT MONTH(OrderDate)) FROM Orders WHERE YEAR(OrderDate) = YEAR(GETDATE()));
```

14. **Encuentra los clientes que hayan realizado al menos un pedido en cada mes desde que se registraron en la base de datos. Muestra el resultado con el nombre del cliente y el número de meses en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT MONTH(o.OrderDate)) AS MesesPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE YEAR(o.OrderDate) >= YEAR(c.RegisteredDate)
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT MONTH(o.OrderDate)) = (SELECT DATEDIFF(MONTH, RegisteredDate, GETDATE()) + 1 FROM Customers WHERE CustomerID = c.CustomerID);
```

15. **Encuentra los empleados que hayan realizado al menos un pedido en cada año desde que se unieron a la empresa. Muestra el resultado con el nombre del empleado y el número de años en los que ha realizado pedidos.**

```
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS Empleado, COUNT(DISTINCT YEAR(o.OrderDate)) AS AñosPedidos
FROM Employees e
JOIN Orders o ON e.EmployeeID = o.EmployeeID
WHERE YEAR(o.OrderDate) >= YEAR(e.HireDate)
GROUP BY e.EmployeeID, e.FirstName, e.LastName
HAVING COUNT(DISTINCT YEAR(o.OrderDate)) = (SELECT DATEDIFF(YEAR, HireDate, GETDATE()) + 1 FROM Employees WHERE EmployeeID = e.EmployeeID);
```

16. **Encuentra los productos que hayan sido pedidos al menos una vez en cada año disponible en la base de datos. Muestra el resultado con el nombre del producto y el número de años en los que ha sido pedido.**

```
SELECT p.ProductID, p.ProductName AS Producto, COUNT(DISTINCT YEAR(o.OrderDate)) AS AñosPedidos
FROM Products p
JOIN [Order Details] od ON p.ProductID = od.ProductID
JOIN Orders o ON od.OrderID = o.OrderID
GROUP BY p.ProductID, p.ProductName
HAVING COUNT(DISTINCT YEAR(o.OrderDate)) = (SELECT COUNT(DISTINCT YEAR(OrderDate)) FROM Orders);
```

17. **Encuentra los clientes que hayan realizado pedidos en todos los meses del año actual hasta la fecha actual. Muestra el resultado con el nombre del cliente y el número de meses en los que ha realizado pedidos.**

```
SELECT c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT MONTH(o.OrderDate)) AS MesesPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE YEAR(o.OrderDate) = YEAR(GETDATE()) AND o.OrderDate <= GETDATE()
GROUP BY c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT MONTH(o.OrderDate)) = (SELECT COUNT(DISTINCT MONTH(OrderDate)) FROM Orders WHERE YEAR(OrderDate) = YEAR(GETDATE()) AND OrderDate <= GETDATE());
```

18. **Encuentra los empleados que hayan realizado al menos un pedido en todos los trimestres del año actual hasta la fecha actual. Muestra el resultado con el nombre del empleado y el número de trimestres en los que ha realizado pedidos.**

```
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS Empleado, COUNT(DISTINCT DATEPART(QUARTER, o.OrderDate)) AS TrimestresPedidos
FROM Employees e
JOIN Orders o ON e.EmployeeID = o.EmployeeID
WHERE YEAR(o.OrderDate) = YEAR(GETDATE()) AND o.OrderDate <= GETDATE()
GROUP BY e.EmployeeID, e.FirstName, e.LastName
HAVING COUNT(DISTINCT DATEPART(QUARTER, o.OrderDate)) = (SELECT COUNT(DISTINCT DATEPART(QUARTER, OrderDate)) FROM Orders WHERE YEAR(OrderDate) = YEAR(GETDATE()) AND OrderDate <= GETDATE());
```

19. **Encuentra los productos que hayan sido pedidos al menos una vez en cada ciudad donde hay clientes. Muestra el resultado con el nombre del producto y el número de ciudades en las que ha sido pedido.**

```
SELECT p.ProductID, p.ProductName AS Producto, COUNT(DISTINCT c.City) AS CiudadesPedidos
FROM Products p
JOIN [Order Details] od ON p.ProductID = od.ProductID
JOIN Orders o ON od.OrderID = o.OrderID
JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY p.ProductID, p.ProductName
HAVING COUNT(DISTINCT c.City) = (SELECT COUNT(DISTINCT City) FROM Customers);
```

20. **Encuentra los clientes que hayan realizado pedidos en todos los países donde hay clientes, agrupados por continente. Muestra el resultado con el nombre del continente, el nombre del cliente y el número de países en los que ha realizado pedidos.**

```
SELECT co.ContinentName AS Continente, c.CustomerID, c.CompanyName AS Cliente, COUNT(DISTINCT co.Country) AS PaisesPedidos
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN Customers co ON o.CustomerID = co.CustomerID
JOIN Countries cou ON co.Country = cou.CountryName
GROUP BY co.ContinentName, c.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT co.Country) = (SELECT COUNT(DISTINCT Country) FROM Customers WHERE Country IN (SELECT CountryName FROM Countries WHERE ContinentName = co.ContinentName));
```

[🔼](#índice)

---

| **Inicio**            | **atrás 21**                |
| --------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./21_Consultas_SQL.md) |
