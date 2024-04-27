| **Inicio**            | **atrás 7**                | **Siguiente 9**            |
| --------------------- | -------------------------- | -------------------------- |
| [🏠](../../README.md) | [⏪](./7_Consultas_SQL.md) | [⏩](./9_Consultas_SQL.md) |

---

## **Índice**

| Temario                                              |
| ---------------------------------------------------- |
| [71. La cláusula WHERE](#71-la-cláusula-where)       |
| [72. La cláusula TOP](#72-la-cláusula-top)           |
| [73. La cláusula ORDER BY](#73-la-cláusula-order-by) |
| [74. La Cláusula DISTINCT](#74-la-cláusula-distinct) |
| [75. La Cláusula GROUP BY](#75-la-cláusula-group-by) |
| [76. Función MAX y MIN](#76-función-max-y-min)       |
| [77. Función SUM](#77-función-sum)                   |
| [78. Función AVG](#78-función-avg)                   |
| [79. Función COUNT](#79-función-count)               |
| [80. Función HAVING](#80-función-having)             |

---

# **Tutorial de SQL**

## **71. La cláusula WHERE**

En SQL Server, la cláusula `WHERE` se utiliza para filtrar los datos en una consulta `SELECT`, `UPDATE` o `DELETE`. Permite especificar una condición que debe cumplirse para que se seleccionen, actualicen o eliminen los registros deseados.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `WHERE` en SQL Server con la base de datos Northwind:

La cláusula `WHERE` se coloca después del nombre de la tabla en una consulta y antes de cualquier otra cláusula, como `ORDER BY` o `GROUP BY`. Permite aplicar una condición lógica a las filas de la tabla y seleccionar solo aquellas que cumplan con la condición especificada.

La sintaxis básica de la cláusula `WHERE` es la siguiente:

```
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

En el caso de una consulta `SELECT`, la cláusula `WHERE` se utiliza para filtrar los registros que se devolverán en el resultado. Por ejemplo, si deseas obtener todos los productos de la tabla "`Products`" con un precio mayor a `10`, la consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice > 10;
```

En esta consulta, la cláusula `WHERE` se utiliza para especificar la condición de que solo se seleccionarán los productos con un precio (`UnitPrice`) mayor a `10`.

La cláusula `WHERE` también se utiliza en comandos `UPDATE` y `DELETE` para especificar la condición que debe cumplirse para actualizar o eliminar registros, respectivamente.

Por ejemplo, si deseas actualizar el precio de los productos de una categoría específica utilizando el comando `UPDATE`, puedes utilizar la siguiente consulta:

```
UPDATE Products
SET UnitPrice = UnitPrice * 1.1
WHERE CategoryID = 1;
```

En esta consulta, la cláusula `WHERE` se utiliza para especificar que solo se actualizarán los productos que pertenezcan a la categoría con el `ID` igual a `1`.

De manera similar, si deseas eliminar todos los productos que están agotados (con unidades en stock igual a cero) utilizando el comando `DELETE`, puedes utilizar la siguiente consulta:

```
DELETE FROM Products
WHERE UnitsInStock = 0;
```

En esta consulta, la cláusula `WHERE` se utiliza para especificar la condición de que solo se eliminarán los productos con unidades en stock igual a cero.

En resumen, la cláusula `WHERE` en SQL Server se utiliza para filtrar los datos en una consulta `SELECT`, `UPDATE` o `DELETE`. Permite especificar una condición que debe cumplirse para que se seleccionen, actualicen o eliminen los registros deseados. La cláusula `WHERE` te permite realizar consultas más precisas y controladas al trabajar con bases de datos.

[🔼](#índice)

---

## **72. La cláusula TOP**

En SQL Server, la cláusula `TOP` se utiliza para limitar el número de filas que se devuelven en una consulta `SELECT`. Permite especificar la cantidad exacta de filas que se desean obtener desde el inicio del conjunto de resultados.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `TOP` en SQL Server con la base de datos Northwind:

La cláusula `TOP` se coloca después de la cláusula `SELECT` en una consulta y antes de las columnas o la expresión que se desea seleccionar. Permite especificar el número exacto de filas que se deben devolver en el resultado.

La sintaxis básica de la cláusula `TOP` es la siguiente:

```
SELECT TOP (number) column1, column2, ...
FROM table_name;
```

En el caso de una consulta `SELECT`, la cláusula `TOP` se utiliza para limitar el número de filas que se devolverán en el resultado. Por ejemplo, si deseas obtener los `5` productos más caros de la tabla "`Products`" en la base de datos Northwind, la consulta sería similar a esto:

```
SELECT TOP (5) ProductName, UnitPrice
FROM Products
ORDER BY UnitPrice DESC;
```

En esta consulta, la cláusula `TOP` se establece en `5` para especificar que solo se deben devolver las primeras `5` filas del conjunto de resultados. Además, se utiliza la cláusula `ORDER BY` para ordenar los productos por precio (`UnitPrice`) en orden descendente, de modo que los productos más caros aparezcan primero.

La cláusula `TOP` también se puede utilizar junto con la cláusula `PERCENT` para obtener un porcentaje específico de filas. Por ejemplo, si deseas obtener el `10%` de los productos más caros, la consulta se vería así:

```
SELECT TOP (10) PERCENT ProductName, UnitPrice
FROM Products
ORDER BY UnitPrice DESC;
```

En esta consulta, la cláusula `TOP` se establece en `10 PERCENT` para obtener el `10%` de las filas del conjunto de resultados, en este caso, los productos más caros.

Es importante tener en cuenta que si hay filas con el mismo valor en la columna utilizada para ordenar, no hay garantía de que siempre se devuelvan exactamente el número de filas especificado por la cláusula `TOP`. Si se necesita un resultado consistente y predecible, se debe especificar una columna adicional para la ordenación que garantice el ordenamiento consistente de las filas.

En resumen, la cláusula `TOP` en SQL Server se utiliza para limitar el número de filas que se devuelven en una consulta `SELECT`. Permite especificar la cantidad exacta de filas que se desean obtener desde el inicio del conjunto de resultados. La cláusula `TOP` es útil para realizar consultas con una limitación en el número de filas y obtener resultados más precisos y eficientes.

[🔼](#índice)

---

## **73. La cláusula ORDER BY**

En SQL Server, la cláusula `ORDER BY` se utiliza para ordenar los resultados de una consulta en función de uno o varios campos de una tabla. Permite especificar el orden ascendente o descendente en el que se deben presentar los datos.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `ORDER BY` en SQL Server con la base de datos Northwind:

La cláusula `ORDER BY` se coloca al final de una consulta `SELECT` y se utiliza para ordenar los registros en base a una o varias columnas. Puedes ordenar los resultados en orden ascendente (`asc`) o descendente (`desc`) según tus necesidades.

La sintaxis básica de la cláusula `ORDER BY` es la siguiente:

```
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...;
```

En el caso de una consulta `SELECT`, la cláusula `ORDER BY` se utiliza para ordenar los registros devueltos por la consulta. Por ejemplo, si deseas obtener los productos de la tabla "`Products`" en la base de datos Northwind ordenados por su precio (`UnitPrice`) de manera descendente, la consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
ORDER BY UnitPrice DESC;
```

En esta consulta, se utiliza la cláusula `ORDER BY` con el campo `UnitPrice` para ordenar los productos según su precio de manera descendente. Los productos más caros aparecerán primero en el resultado.

También puedes ordenar los resultados utilizando múltiples columnas en la cláusula `ORDER BY`. Por ejemplo, si deseas obtener los productos de la tabla "`Products`" ordenados primero por su categoría (`CategoryID`) de manera ascendente y luego por su precio (`UnitPrice`) de manera descendente, la consulta se vería así:

```
SELECT ProductName, UnitPrice
FROM Products
ORDER BY CategoryID ASC, UnitPrice DESC;
```

En esta consulta, se utiliza la cláusula `ORDER BY` con los campos `CategoryID` y `UnitPrice`. Los productos se ordenarán primero por su categoría de manera ascendente y, en caso de que haya productos con la misma categoría, se ordenarán por su precio de manera descendente.

Es importante tener en cuenta que la cláusula `ORDER BY` se aplica después de que se hayan seleccionado y filtrado los registros con otras cláusulas, como `WHERE`. Esto significa que puedes utilizar la cláusula `ORDER BY` junto con otras cláusulas para obtener resultados más específicos y ordenados.

En resumen, la cláusula `ORDER BY` en SQL Server se utiliza para ordenar los resultados de una consulta en función de uno o varios campos de una tabla. Permite especificar el orden ascendente o descendente en el que se deben presentar los datos. La cláusula `ORDER BY` es útil para obtener resultados ordenados y organizados en base a criterios específicos.

[🔼](#índice)

---

## **74. La Cláusula DISTINCT**

En SQL Server, la cláusula `DISTINCT` se utiliza para eliminar duplicados de los resultados de una consulta `SELECT`. Permite obtener valores únicos de una columna o conjunto de columnas seleccionadas en base a la condición especificada.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `DISTINCT` en SQL Server con la base de datos Northwind:

La cláusula `DISTINCT` se coloca después de la palabra clave `SELECT` y se utiliza para seleccionar valores únicos de una columna o conjunto de columnas en una consulta. Elimina las filas duplicadas del conjunto de resultados devuelto.

La sintaxis básica de la cláusula `DISTINCT` es la siguiente:

```
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

En el caso de una consulta `SELECT`, la cláusula `DISTINCT` se utiliza para seleccionar valores únicos de una columna o conjunto de columnas. Por ejemplo, si deseas obtener una lista de todas las categorías únicas de productos en la tabla "`Products`" de la base de datos Northwind, la consulta sería similar a esto:

```
SELECT DISTINCT CategoryName
FROM Categories;
```

En esta consulta, se utiliza la cláusula `DISTINCT` con la columna `CategoryName` para obtener una lista de categorías únicas de productos. Esto asegura que no se repitan las categorías en el resultado.

La cláusula `DISTINCT` también se puede utilizar con múltiples columnas. Por ejemplo, si deseas obtener una lista de combinaciones únicas de categorías y proveedores en la tabla "`Products`", la consulta se vería así:

```
SELECT DISTINCT CompanyName, SupplierID
FROM Suppliers;
```

En esta consulta, se utiliza la cláusula `DISTINCT` con las columnas `CategoryName` y `SupplierID` para obtener combinaciones únicas de categorías y proveedores de productos.

Es importante tener en cuenta que la cláusula `DISTINCT` se aplica a todas las columnas especificadas en la lista de selección. Esto significa que si utilizas la cláusula `DISTINCT` con varias columnas, se considerarán combinaciones únicas de valores en esas columnas, no solo valores únicos en cada columna por separado.

En resumen, la cláusula `DISTINCT` en SQL Server se utiliza para eliminar duplicados de los resultados de una consulta `SELECT`. Permite obtener valores únicos de una columna o conjunto de columnas seleccionadas en base a la condición especificada. La cláusula `DISTINCT` es útil para obtener resultados sin repeticiones y realizar consultas más específicas y limpias en base de datos.

[🔼](#índice)

---

## **75. La Cláusula GROUP BY**

En SQL Server, la cláusula `GROUP BY` se utiliza para agrupar filas en base a un conjunto de columnas y realizar cálculos o resúmenes sobre esos grupos. Permite agrupar los resultados de una consulta y aplicar funciones de agregación, como `SUM`, `COUNT`, `AVG`, `MAX`, `MIN`, entre otras, a cada grupo de filas.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `GROUP BY` en SQL Server con la base de datos Northwind:

La cláusula `GROUP BY` se coloca al final de una consulta `SELECT` y se utiliza para agrupar los registros en base a una o varias columnas. Esto permite realizar operaciones de agregación en cada grupo.

La sintaxis básica de la cláusula `GROUP BY` es la siguiente:

```
SELECT column1, column2, ..., aggregate_function(column)
FROM table_name
WHERE condition
GROUP BY column1, column2, ...;
```

En el caso de una consulta `SELECT` con la cláusula `GROUP BY`, primero se especifican las columnas que deseas seleccionar. Luego, se pueden aplicar funciones de agregación, como `SUM`, `COUNT`, `AVG`, `MAX`, `MIN`, entre otras, a cada grupo de filas.

Por ejemplo, supongamos que deseas obtener la cantidad total de productos vendidos en cada categoría de la tabla "`Order Details`" en la base de datos Northwind. La consulta sería similar a esto:

```
SELECT ProductID, SUM(Quantity) AS TotalQuantity
FROM [Order Details]
GROUP BY ProductID;
```

En esta consulta, se utiliza la cláusula `GROUP BY` con la columna `CategoryID` para agrupar los registros según la categoría. Luego, se aplica la función de agregación `SUM` a la columna `Quantity` para obtener la suma total de productos vendidos en cada categoría. El resultado mostrará la categoría y la cantidad total de productos vendidos en cada una.

Además de la columna utilizada para agrupar, también se pueden incluir otras columnas en la cláusula `GROUP BY`. Esto permite realizar agrupaciones más específicas y obtener resultados más detallados.

Es importante tener en cuenta que, al utilizar la cláusula `GROUP BY`, solo se pueden seleccionar columnas que estén incluidas en la cláusula `GROUP BY` o sean funciones de agregación. Si se intenta seleccionar una columna que no esté en la cláusula `GROUP BY` ni sea una función de agregación, se producirá un error.

En resumen, la cláusula `GROUP BY` en SQL Server se utiliza para agrupar filas en base a un conjunto de columnas y realizar cálculos o resúmenes sobre esos grupos. Permite aplicar funciones de agregación a cada grupo y obtener resultados agrupados y resumidos. La cláusula `GROUP BY` es útil para realizar análisis de datos y obtener información agregada en base de datos.

[🔼](#índice)

---

## **76. Función MAX y MIN**

En SQL Server, las funciones `MAX` y `MIN` se utilizan para obtener el valor máximo y mínimo de una columna numérica o alfabética, respectivamente. Estas funciones son funciones de agregación que se pueden aplicar en una consulta `SELECT` para obtener el valor máximo o mínimo de una columna en un conjunto de registros.

Aquí tienes una explicación detallada de cómo utilizar las funciones `MAX` y `MIN` en SQL Server con la base de datos Northwind:

La función `MAX` se utiliza para obtener el valor máximo de una columna en un conjunto de registros. Puede ser utilizado en columnas numéricas y alfabéticas. La sintaxis básica de la función `MAX` es la siguiente:

```
SELECT MAX(column_name)
FROM table_name;
```

Por ejemplo, si deseas obtener el precio máximo de los productos en la tabla "`Products`" de la base de datos Northwind, la consulta sería similar a esto:

```
SELECT MAX(UnitPrice) AS MaxPrice
FROM Products;
```

En esta consulta, se utiliza la función `MAX` para obtener el precio máximo (`UnitPrice`) de los productos. El resultado mostrará el valor máximo de la columna `UnitPrice`.

La función `MIN` se utiliza de manera similar a la función `MAX`, pero en lugar de obtener el valor máximo, se obtiene el valor mínimo de una columna en un conjunto de registros. La sintaxis básica de la función `MIN` es la siguiente:

```
SELECT MIN(column_name)
FROM table_name;
```

Por ejemplo, si deseas obtener el precio mínimo de los productos en la tabla "`Products`", la consulta sería similar a esto:

```
SELECT MIN(UnitPrice) AS MinPrice
FROM Products;
```

En esta consulta, se utiliza la función `MIN` para obtener el precio mínimo (`UnitPrice`) de los productos. El resultado mostrará el valor mínimo de la columna `UnitPrice`.

Es importante tener en cuenta que las funciones `MAX` y `MIN` pueden combinarse con otras cláusulas, como `WHERE` o `GROUP BY`, para obtener el valor máximo o mínimo dentro de un conjunto específico de registros o grupos.

Por ejemplo, si deseas obtener el precio máximo de los productos de una categoría específica, puedes combinar la función `MAX` con la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT MAX(UnitPrice) AS MaxPrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, se utiliza la función `MAX` para obtener el precio máximo de los productos de la categoría con el `ID` igual a `1`.

En resumen, las funciones `MAX` y `MIN` en SQL Server se utilizan para obtener el valor máximo y mínimo de una columna en un conjunto de registros. La función `MAX` se utiliza para columnas numéricas o alfabéticas y devuelve el valor máximo, mientras que la función `MIN` se utiliza para obtener el valor mínimo. Estas funciones son útiles para realizar análisis de datos y obtener información sobre los valores extremos en una base de datos.

[🔼](#índice)

---

## **77. Función SUM**

En SQL Server, la función `SUM` se utiliza para calcular la suma de los valores numéricos de una columna en un conjunto de registros. Permite obtener el total de los valores de una columna numérica en una consulta.

Aquí tienes una explicación detallada de cómo utilizar la función `SUM` en SQL Server con la base de datos Northwind:

La función `SUM` se utiliza en una consulta `SELECT` para calcular la suma de los valores de una columna específica. La sintaxis básica de la función `SUM` es la siguiente:

```
SELECT SUM(column_name)
FROM table_name;
```

Por ejemplo, si deseas obtener la suma total de los precios de los productos en la tabla "`Products`" de la base de datos Northwind, la consulta sería similar a esto:

```
SELECT SUM(UnitPrice) AS TotalPrice
FROM Products;
```

En esta consulta, se utiliza la función `SUM` para obtener la suma total de los precios de los productos (columna `UnitPrice`). El resultado mostrará el valor total de la suma de los precios.

La función `SUM` también se puede combinar con otras cláusulas, como `WHERE` o `GROUP BY`, para realizar cálculos más específicos. Por ejemplo, si deseas obtener la suma total de los precios de los productos de una categoría específica, puedes combinar la función `SUM` con la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT SUM(UnitPrice) AS TotalPrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, se utiliza la función `SUM` para obtener la suma total de los precios de los productos de la categoría con el `ID` igual a `1`.

Además, es posible utilizar la función `SUM` en combinación con otras funciones de agregación, como `COUNT`, para obtener cálculos más complejos. Por ejemplo, si deseas obtener el número de productos y la suma total de sus precios en una categoría específica, puedes combinar las funciones `SUM` y `COUNT`. La consulta sería similar a esto:

```
SELECT COUNT(*) AS TotalProducts, SUM(UnitPrice) AS TotalPrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, la función `COUNT` se utiliza para obtener el número de productos y la función `SUM` se utiliza para obtener la suma total de los precios de los productos de la categoría con el `ID` igual a `1`.

En resumen, la función `SUM` en SQL Server se utiliza para calcular la suma de los valores numéricos de una columna en un conjunto de registros. Permite obtener el total de los valores de una columna numérica en una consulta. La función `SUM` es útil para realizar cálculos de totales y realizar análisis numéricos en una base de datos.

[🔼](#índice)

---

## **78. Función AVG**

En SQL Server, la función `AVG` se utiliza para calcular el promedio de los valores numéricos de una columna en un conjunto de registros. Permite obtener el valor promedio de una columna numérica en una consulta.

Aquí tienes una explicación detallada de cómo utilizar la función `AVG` en SQL Server con la base de datos Northwind:

La función `AVG` se utiliza en una consulta `SELECT` para calcular el promedio de los valores de una columna específica. La sintaxis básica de la función `AVG` es la siguiente:

```
SELECT AVG(column_name)
FROM table_name;
```

Por ejemplo, si deseas obtener el promedio de los precios de los productos en la tabla "`Products`" de la base de datos Northwind, la consulta sería similar a esto:

```
SELECT AVG(UnitPrice) AS AveragePrice
FROM Products;
```

En esta consulta, se utiliza la función `AVG` para obtener el promedio de los precios de los productos (columna `UnitPrice`). El resultado mostrará el valor promedio de los precios.

La función `AVG` también se puede combinar con otras cláusulas, como `WHERE` o `GROUP BY`, para realizar cálculos más específicos. Por ejemplo, si deseas obtener el promedio de los precios de los productos de una categoría específica, puedes combinar la función `AVG` con la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT AVG(UnitPrice) AS AveragePrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, se utiliza la función `AVG` para obtener el promedio de los precios de los productos de la categoría con el `ID` igual a `1`.

Al igual que otras funciones de agregación, la función `AVG` también puede ser utilizada en combinación con otras funciones. Por ejemplo, si deseas obtener el número de productos y el promedio de sus precios en una categoría específica, puedes combinar las funciones `AVG` y `COUNT`. La consulta sería similar a esto:

```
SELECT COUNT(*) AS TotalProducts, AVG(UnitPrice) AS AveragePrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, la función `COUNT` se utiliza para obtener el número de productos y la función `AVG` se utiliza para obtener el promedio de los precios de los productos de la categoría con el `ID` igual a `1`.

En resumen, la función `AVG` en SQL Server se utiliza para calcular el promedio de los valores numéricos de una columna en un conjunto de registros. Permite obtener el valor promedio de una columna numérica en una consulta. La función `AVG` es útil para realizar cálculos de promedios y análisis estadísticos en una base de datos.

[🔼](#índice)

---

## **79. Función COUNT**

En SQL Server, la función `COUNT` se utiliza para contar el número de filas en una columna o el número de registros que cumplen una condición específica en una tabla. La función `COUNT` es una función de agregación que permite realizar cálculos de conteo en una consulta.

Aquí tienes una explicación detallada de cómo utilizar la función `COUNT` en SQL Server con la base de datos Northwind:

La función `COUNT` se utiliza en una consulta `SELECT` para contar el número de filas en una columna o el número de registros que cumplen una condición específica. La sintaxis básica de la función `COUNT` es la siguiente:

```
SELECT COUNT(column_name)
FROM table_name;
```

Por ejemplo, si deseas contar el número de productos en la tabla "`Products`" de la base de datos Northwind, la consulta sería similar a esto:

```
SELECT COUNT(ProductID) AS TotalProducts
FROM Products;
```

En esta consulta, se utiliza la función `COUNT` para contar el número de filas en la columna `ProductID` de la tabla `Products`. El resultado mostrará el total de productos.

La función `COUNT` también se puede combinar con otras cláusulas, como `WHERE` o `GROUP BY`, para realizar cálculos de conteo más específicos. Por ejemplo, si deseas contar el número de productos de una categoría específica, puedes combinar la función `COUNT` con la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT COUNT(ProductID) AS TotalProducts
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, se utiliza la función `COUNT` para contar el número de productos que tienen un `CategoryID` igual a `1`.

Además, la función `COUNT` también se puede utilizar en combinación con otras funciones de agregación. Por ejemplo, si deseas obtener el número de productos y la suma total de sus precios en una categoría específica, puedes combinar las funciones `COUNT` y `SUM`. La consulta sería similar a esto:

```
SELECT COUNT(ProductID) AS TotalProducts, SUM(UnitPrice) AS TotalPrice
FROM Products
WHERE CategoryID = 1;
```

En esta consulta, la función `COUNT` se utiliza para contar el número de productos y la función `SUM` se utiliza para obtener la suma total de los precios de los productos de la categoría con el `ID` igual a `1`.

Es importante tener en cuenta que la función `COUNT` puede contar todas las filas de una columna, incluyendo los valores nulos, a menos que se especifique lo contrario utilizando la cláusula `WHERE` para filtrar los registros nulos.

En resumen, la función `COUNT` en SQL Server se utiliza para contar el número de filas en una columna o el número de registros que cumplen una condición específica en una tabla. Permite realizar cálculos de conteo en una consulta. La función `COUNT` es útil para obtener información sobre la cantidad de registros en una tabla y realizar análisis de datos en una base de datos.

[🔼](#índice)

---

## **80. Función HAVING**

En SQL Server, la cláusula `HAVING` se utiliza en combinación con la cláusula `GROUP BY` para filtrar los resultados de una consulta basados en una condición que involucra agregaciones. La cláusula `HAVING` permite aplicar condiciones a los grupos resultantes de la agrupación, a diferencia de la cláusula `WHERE` que se utiliza para filtrar filas individuales.

Aquí tienes una explicación detallada de cómo utilizar la cláusula `HAVING` en SQL Server con la base de datos Northwind:

La cláusula `HAVING` se utiliza después de la cláusula `GROUP BY` para aplicar condiciones a los grupos resultantes. La sintaxis básica de la cláusula `HAVING` es la siguiente:

```
SELECT column_name(s)
FROM table_name
GROUP BY column_name(s)
HAVING condition;
```

Por ejemplo, supongamos que deseas obtener las categorías de productos junto con la cantidad total de productos en cada categoría, pero solo quieres mostrar las categorías que tienen más de `10` productos. Puedes usar la cláusula `HAVING` para aplicar esta condición de filtrado. La consulta sería similar a esto:

```
SELECT CategoryID, COUNT(ProductID) AS TotalProducts
FROM Products
GROUP BY CategoryID
HAVING COUNT(ProductID) > 10;
```

En esta consulta, se utiliza la cláusula `GROUP BY` para agrupar los productos por `CategoryID` y la función `COUNT` para obtener la cantidad total de productos en cada categoría. Luego, la cláusula `HAVING` se utiliza para filtrar los grupos y mostrar solo aquellos que tienen más de `10` productos.

Otro ejemplo sería si deseas obtener las categorías de productos junto con el precio promedio de los productos en cada categoría, pero solo quieres mostrar las categorías cuyo precio promedio sea superior a `50`. Puedes usar la cláusula `HAVING` para aplicar esta condición de filtrado. La consulta sería similar a esto:

```
SELECT CategoryID, AVG(UnitPrice) AS AveragePrice
FROM Products
GROUP BY CategoryID
HAVING AVG(UnitPrice) > 50;
```

En esta consulta, se utiliza la cláusula `GROUP BY` para agrupar los productos por `CategoryID` y la función `AVG` para obtener el precio promedio de los productos en cada categoría. Luego, la cláusula `HAVING` se utiliza para filtrar los grupos y mostrar solo aquellos cuyo precio promedio sea superior a `50`.

Es importante tener en cuenta que la cláusula `HAVING` se aplica después de la agrupación, por lo que solo puede hacer referencia a columnas agregadas o funciones de agregación en la condición.

En resumen, la cláusula `HAVING` en SQL Server se utiliza en combinación con la cláusula `GROUP BY` para filtrar los resultados de una consulta basados en una condición que involucra agregaciones. Permite aplicar condiciones a los grupos resultantes y filtrar grupos basados en condiciones específicas. La cláusula `HAVING` es útil cuando se desea aplicar condiciones a grupos después de la agrupación en una consulta.

[🔼](#índice)

---

| **Inicio**            | **atrás 7**                | **Siguiente 9**            |
| --------------------- | -------------------------- | -------------------------- |
| [🏠](../../README.md) | [⏪](./7_Consultas_SQL.md) | [⏩](./9_Consultas_SQL.md) |
