| **Inicio**            | **atrás 18**                | **Siguiente 20**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./18_Consultas_SQL.md) | [⏩](./20_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------- |
| [181. Lenguaje SQL y T-SQL](#181-lenguaje-sql-y-t-sql)                                                                                        |
| [182. Crear tablas, columnas, llaves primarias y foráneas](#182-crear-tablas-columnas-llaves-primarias-y-foráneas)                            |
| [183. Relacionamiento entre tablas](#183-relacionamiento-entre-tablas)                                                                        |
| [184. Funciones básicas SQL: Select, Where, Order By](#184-funciones-básicas-sql-select-where-order-by)                                       |
| [185. Funciones agregación Group By: Count, Sum, Max](#185-funciones-agregación-group-by-count-sum-max)                                       |
| [186. Funciones filtro Where y operadores lógicos: Between, In, Like](#186-funciones-filtro-where-y-operadores-lógicos-between-in-like)       |
| [187. Funciones para la manipulación de texto y fechas](#187-funciones-para-la-manipulación-de-texto-y-fechas)                                |
| [188. Funciones avanzadas SQL: Subquerys, Having, consultas multi tabla](#188-funciones-avanzadas-sql-subquerys-having-consultas-multi-tabla) |
| [189. Creación de vistas](#189-creación-de-vistas)                                                                                            |
| [190. Procedimientos almacenados](#190-procedimientos-almacenados)                                                                            |

---

# **Tutorial de SQL**

## **181. Lenguaje SQL y T-SQL**

El lenguaje SQL (Structured Query Language) es un lenguaje de programación utilizado para administrar y manipular bases de datos relacionales. Proporciona un conjunto de comandos y operaciones que permiten realizar consultas, inserciones, actualizaciones y eliminaciones de datos en una base de datos. SQL es un estándar reconocido por la mayoría de los sistemas de gestión de bases de datos relacionales (`RDBMS`), lo que significa que se puede utilizar en diferentes plataformas y sistemas.

Por otro lado, T-SQL (Transact-SQL) es una implementación específica del lenguaje SQL que se utiliza en los sistemas de gestión de bases de datos de Microsoft, como Microsoft SQL Server. T-SQL extiende el estándar SQL al agregar características y funcionalidades adicionales para el desarrollo de aplicaciones y la administración de bases de datos.

A continuación, te proporcionaré una explicación detallada de ambos lenguajes con ejemplos:

1. **Lenguaje SQL:**

El lenguaje SQL se utiliza para realizar operaciones en bases de datos relacionales. Algunos de los comandos más comunes en SQL incluyen:

- **SELECT:** Se utiliza para realizar consultas y recuperar datos de una o varias tablas.

**Ejemplo:**

`SELECT * FROM Customers;`

- **INSERT:** Se utiliza para insertar nuevos registros en una tabla.

**Ejemplo:**

`INSERT INTO Customers (Name, Email) VALUES ('John Doe', 'john@example.com');`

- **UPDATE:** Se utiliza para actualizar registros existentes en una tabla.

**Ejemplo:**

`UPDATE Customers SET Email = 'johndoe@example.com' WHERE ID = 1;`

- **DELETE:** Se utiliza para eliminar registros de una tabla.

**Ejemplo:**

`DELETE FROM Customers WHERE ID = 1;`

2. **T-SQL:**

T-SQL es una extensión del lenguaje SQL que proporciona características adicionales específicas de los sistemas de gestión de bases de datos de Microsoft. Algunas de las características adicionales de T-SQL incluyen:

- **Variables:** Permite declarar y utilizar variables dentro de las consultas.

**Ejemplo:**

```
DECLARE @FirstName VARCHAR(50);
SET @FirstName = 'John';

SELECT * FROM Customers WHERE FirstName = @FirstName;
```

- **Procedimientos almacenados:** Permite definir bloques de código reutilizables que se pueden llamar desde otras partes de la aplicación.

**Ejemplo:**

```
CREATE PROCEDURE GetCustomerByID
    @CustomerID INT
AS
BEGIN
    SELECT * FROM Customers WHERE ID = @CustomerID;
END;
```

- **Funciones:** Permite definir funciones que pueden realizar cálculos y retornar valores.

**Ejemplo:**

```
CREATE FUNCTION CalculateTotalPrice
    (@Price DECIMAL(10, 2), @Quantity INT)
RETURNS DECIMAL(10, 2)
AS
BEGIN
    RETURN @Price * @Quantity;
END;
```

- **Transacciones:** Permite agrupar varias operaciones en una unidad lógica para garantizar la consistencia y la integridad de los datos.

**Ejemplo:**

```
BEGIN TRANSACTION;

UPDATE Customers SET Email = 'johndoe@example.com' WHERE ID = 1;
INSERT INTO Orders (CustomerID, OrderDate) VALUES (1, GETDATE());

COMMIT TRANSACTION;
```

En resumen, el lenguaje SQL es un estándar utilizado para administrar y manipular bases de datos relacionales, mientras que T-SQL es una implementación específica de SQL utilizada en sistemas de gestión de bases de datos de Microsoft. Ambos lenguajes permiten realizar consultas, inserciones, actualizaciones y eliminaciones de datos, pero T-SQL agrega características adicionales como variables, procedimientos almacenados, funciones y transacciones específicas de los sistemas de gestión de bases de datos de Microsoft.

[🔼](#índice)

---

## **182. Crear tablas, columnas, llaves primarias y foráneas**

Para crear tablas, columnas, llaves primarias y llaves foráneas en SQL Server, se utilizan comandos del lenguaje SQL. A continuación, te proporcionaré una explicación detallada de cómo crear estos elementos con ejemplos:

1. **Crear una tabla:**

El comando utilizado para crear una tabla es `CREATE TABLE`. Debes especificar el nombre de la tabla y las columnas junto con sus tipos de datos y restricciones.

**Ejemplo:**

```
CREATE TABLE Customers (
    ID INT,
    Name VARCHAR(50),
    Email VARCHAR(100),
    PRIMARY KEY (ID)
);
```

En este ejemplo, se crea una tabla llamada "`Customers`" con tres columnas: `ID`, `Name` y `Email`. La columna `ID` se define como clave primaria utilizando `PRIMARY KEY`.

2. **Agregar columnas a una tabla existente:**

Si deseas agregar una nueva columna a una tabla existente, se utiliza el comando `ALTER TABLE` junto con el comando `ADD COLUMN`.

**Ejemplo:**

```
ALTER TABLE Customers
ADD PhoneNumber VARCHAR(20);
```

En este ejemplo, se agrega una nueva columna llamada `PhoneNumber` a la tabla `Customers`.

3. **Definir una clave primaria:**

Una clave primaria identifica de manera única cada registro en una tabla. Se utiliza el comando `CONSTRAINT` junto con el comando `PRIMARY KEY` para definir una clave primaria en una columna o un conjunto de columnas.

**Ejemplo:**

```
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE
);
```

En este ejemplo, se crea una tabla llamada "`Orders`" con una columna `OrderID` como clave primaria.

4. **Definir una llave foránea:**

Una llave foránea establece una relación entre dos tablas. Para definir una llave foránea, se utiliza el comando `CONSTRAINT` junto con el comando `FOREIGN KEY`.

**Ejemplo:**

```
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(ID)
);
```

En este ejemplo, se crea una tabla llamada "`Orders`" con una columna `CustomerID` que es una llave foránea que hace referencia a la columna `ID` en la tabla `Customers`.

Es importante tener en cuenta que al definir una llave foránea, la tabla referenciada debe existir previamente.

Recuerda que estos son solo ejemplos básicos de cómo crear tablas, columnas, llaves primarias y llaves foráneas en SQL Server. El lenguaje SQL tiene muchas más funcionalidades y opciones para la definición y modificación de estructuras de bases de datos.

[🔼](#índice)

---

## **183. Relacionamiento entre tablas**

El relacionamiento entre tablas en SQL Server se refiere a establecer relaciones o vínculos entre tablas utilizando claves primarias y claves foráneas. Estas relaciones permiten vincular la información de diferentes tablas en una base de datos relacional, lo que facilita el acceso y la consulta de los datos de manera eficiente. A continuación, te proporcionaré una explicación detallada con ejemplos:

- **Supongamos que tienes dos tablas:** "`Customers`" y "`Orders`". La tabla "`Customers`" contiene información sobre los clientes, mientras que la tabla "`Orders`" almacena los datos de las órdenes realizadas por los clientes.

Tabla "`Customers`":

```
CREATE TABLE Customers (
    ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Email VARCHAR(100)
);
```

Tabla "`Orders`":

```
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(ID)
);
```

En este ejemplo, la tabla "`Customers`" tiene una columna "`ID`" que se define como clave primaria. La tabla "`Orders`" también tiene una columna "`CustomerID`", que se utiliza como llave foránea para establecer una relación con la tabla "`Customers`".

La relación entre estas dos tablas se crea mediante la clave foránea "`CustomerID`" en la tabla "`Orders`", que hace referencia a la columna "`ID`" en la tabla "`Customers`". Esto significa que cada registro en la tabla "`Orders`" debe tener un valor válido en la columna "`CustomerID`" que corresponda a un valor existente en la columna "`ID`" de la tabla "`Customers`".

Esta relación permite acceder a los datos relacionados entre las tablas mediante consultas. Por ejemplo, para obtener todos los pedidos de un cliente específico, se puede realizar una consulta utilizando la relación entre las tablas:

```
SELECT *
FROM Orders
WHERE CustomerID = 1;
```

En esta consulta, se seleccionan todos los registros de la tabla "`Orders`" donde el valor de "`CustomerID`" es igual a 1, lo que corresponde al `ID` del cliente deseado.

El relacionamiento entre tablas en SQL Server es fundamental para organizar y estructurar los datos de manera coherente y eficiente. Permite establecer conexiones lógicas entre entidades relacionadas y facilita el acceso a información relacionada a través de consultas utilizando claves primarias y foráneas.

Es importante tener en cuenta que existen diferentes tipos de relaciones, como relaciones uno a uno, uno a muchos y muchos a muchos, que se pueden establecer en función de las necesidades específicas de los datos y el diseño de la base de datos.

[🔼](#índice)

---

## **184. Funciones básicas SQL: Select, Where, Order By**

Las funciones básicas SQL `SELECT`, `WHERE` y `ORDER BY` son ampliamente utilizadas en SQL Server para consultar y manipular datos en una base de datos. A continuación, te proporcionaré una explicación detallada de cada una de estas funciones junto con ejemplos utilizando la base de datos Northwind.

Antes de comenzar, asumiremos que ya tienes la base de datos Northwind instalada en tu servidor SQL Server.

**SELECT:**

La función `SELECT` se utiliza para recuperar datos de una o varias tablas. Puedes seleccionar columnas específicas o todas las columnas de una tabla.

**Ejemplo 1:** Seleccionar todas las columnas de la tabla "`Customers`".

```
SELECT *
FROM Customers;
```

**Ejemplo 2:** Seleccionar columnas específicas de la tabla "`Orders`".

```
SELECT OrderID, CustomerID, OrderDate
FROM Orders;
```

**WHERE:**

La función `WHERE` se utiliza para filtrar los registros basados en una condición específica. Puedes utilizar operadores lógicos y comparativos para definir la condición de filtrado.

**Ejemplo:** Seleccionar todos los pedidos realizados por el cliente con CustomerID igual a '`VINET`'.

```
SELECT *
FROM Orders
WHERE CustomerID = 'VINET';
```

**ORDER BY:**

La función `ORDER BY` se utiliza para ordenar los resultados de una consulta en un orden específico. Puedes ordenar por una o varias columnas, de forma ascendente (`ASC`) o descendente (`DESC`).

**Ejemplo:** Seleccionar todos los productos de la tabla "`Products`" ordenados por el campo "`ProductName`" de forma descendente.

```
SELECT *
FROM Products
ORDER BY ProductName DESC;
```

Estos ejemplos son solo una muestra básica de cómo se pueden utilizar las funciones `SELECT`, `WHERE` y `ORDER BY` en SQL Server. Puedes combinar estas funciones y agregar más complejidad a tus consultas para obtener resultados más específicos.

Recuerda que debes conectar a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **185. Funciones agregación Group By: Count, Sum, Max**

Las funciones de agregación `GROUP BY` en SQL Server, como `COUNT`, `SUM` y `MAX`, se utilizan para realizar cálculos sobre grupos de datos en una consulta. Estas funciones permiten obtener información resumida y estadísticas sobre conjuntos de datos específicos. A continuación, te proporcionaré una explicación detallada de cada una de estas funciones con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

- **COUNT:**

La función `COUNT` se utiliza para contar el número de filas en un conjunto de datos. Puedes contar todas las filas o filtrar los resultados con una condición específica.

**Ejemplo 1:** Contar el número total de clientes en la tabla "`Customers`".

```
SELECT COUNT(*) AS TotalCustomers
FROM Customers;
```

**Ejemplo 2:** Contar el número de pedidos realizados por cada cliente en la tabla "`Orders`".

```
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY CustomerID;
```

En el segundo ejemplo, utilizamos la cláusula `GROUP BY` para agrupar los resultados por `CustomerID` y luego utilizamos `COUNT(*)` para contar los pedidos realizados por cada cliente.

**SUM:**

La función `SUM` se utiliza para sumar los valores de una columna numérica en un conjunto de datos.

**Ejemplo:** Calcular la suma total de los precios unitarios de todos los productos en la tabla "`Products`".

```
SELECT SUM(UnitPrice) AS TotalPrice
FROM Products;
```

**MAX:**

La función `MAX` se utiliza para obtener el valor máximo de una columna en un conjunto de datos.

**Ejemplo:** Encontrar el precio máximo entre todos los productos en la tabla "`Products`".

```
SELECT MAX(UnitPrice) AS MaxPrice
FROM Products;
```

Estos ejemplos son solo una muestra básica de cómo se pueden utilizar las funciones de agregación `GROUP BY` en SQL Server. Puedes combinar estas funciones con otras cláusulas SQL, como `WHERE` y `JOIN`, para obtener resultados más específicos y personalizados.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **186. Funciones filtro Where y operadores lógicos: Between, In, Like**

Las funciones de filtro `WHERE` y los operadores lógicos `BETWEEN`, `IN` y `LIKE` en SQL Server se utilizan para filtrar y seleccionar datos específicos en una consulta. Estas funciones y operadores te permiten establecer condiciones más complejas para recuperar datos de una base de datos. A continuación, te proporcionaré una explicación detallada de cada uno de ellos con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

**WHERE:**

La función `WHERE` se utiliza para filtrar los registros basados en una o varias condiciones específicas. Puedes utilizar operadores comparativos (como "`=`", "`<>`", "`<`", "`>`", "`<=`", "`>=`") para establecer las condiciones de filtrado.

**Ejemplo 1:** Seleccionar todos los productos de la tabla "`Products`" con un precio unitario superior a `$20`.

```
SELECT *
FROM Products
WHERE UnitPrice > 20;
```

**Ejemplo 2:** Seleccionar todos los empleados de la tabla "`Employees`" que pertenecen al departamento de ventas.

```
SELECT *
FROM Employees
WHERE TitleOfCourtesy = 'Sales Representative';
```

**BETWEEN:**

El operador lógico `BETWEEN` se utiliza para filtrar los registros cuyos valores se encuentran dentro de un rango específico, inclusivo.

**Ejemplo:** Seleccionar todos los productos de la tabla "`Products`" cuyo precio unitario está entre `$10` y `$20`.

```
SELECT *
FROM Products
WHERE UnitPrice BETWEEN 10 AND 20;
```

**IN:**

El operador lógico `IN` se utiliza para filtrar los registros cuyos valores coinciden con uno de los valores proporcionados en una lista.

**Ejemplo:** Seleccionar todos los productos de la tabla "`Products`" cuya categoría es '`Beverages`' o '`Condiments`'.

```
SELECT *
FROM Products
WHERE CategoryID IN (1, 2);
```

**LIKE:**

El operador lógico `LIKE` se utiliza para realizar búsquedas de patrones en una columna de texto. Puedes utilizar los caracteres comodín "`%`" y "`_`" para representar cualquier conjunto de caracteres o un solo carácter, respectivamente.

**Ejemplo:** Seleccionar todos los clientes de la tabla "`Customers`" cuyo nombre comienza con la letra '`A`'.

```
SELECT *
FROM Customers
WHERE ContactName LIKE 'A%';
```

Estos ejemplos son solo una muestra básica de cómo se pueden utilizar las funciones de filtro `WHERE` y los operadores lógicos `BETWEEN`, `IN` y `LIKE` en SQL Server. Puedes combinar estas funciones y operadores para establecer condiciones más complejas y personalizadas en tus consultas.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **187. Funciones para la manipulación de texto y fechas**

En SQL Server, existen funciones específicas para la manipulación de texto y fechas que te permiten realizar operaciones y obtener resultados basados en valores de texto y fechas en tus consultas. A continuación, te proporcionaré una explicación detallada de algunas de estas funciones junto con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

1. **Funciones de manipulación de texto:**

**LEN:** Devuelve la longitud de una cadena de texto.

**Ejemplo:** Obtener la longitud del nombre de todos los empleados de la tabla "`Employees`".

```
SELECT EmployeeID, FirstName, LEN(FirstName) AS NameLength
FROM Employees;
```

**LEFT y RIGHT:** Devuelven una subcadena de texto desde el inicio (`LEFT`) o el final (`RIGHT`) de una cadena.

**Ejemplo:** Obtener los primeros tres caracteres del nombre de todos los productos de la tabla "`Products`".

```
SELECT ProductName, LEFT(ProductName, 3) AS FirstThreeChars
FROM Products;
```

2. **Funciones de manipulación de fechas:**

**GETDATE:** Devuelve la fecha y hora actuales.

**Ejemplo:** Obtener la fecha y hora actuales.

`SELECT GETDATE() AS CurrentDateTime;`

- **DATEPART:** Devuelve una parte específica de una fecha (año, mes, día, hora, minuto, etc.).

**Ejemplo:** Obtener el año y el mes de la fecha de cada pedido en la tabla "`Orders`".

```
SELECT OrderID, DATEPART(Year, OrderDate) AS OrderYear, DATEPART(Month, OrderDate) AS OrderMonth
FROM Orders;
```

- **DATEDIFF:** Calcula la diferencia entre dos fechas en una unidad de tiempo específica (años, meses, días, horas, minutos, etc.).

**Ejemplo:** Calcular la diferencia en días entre la fecha de inicio y la fecha de entrega de cada pedido en la tabla "`Orders`".

```
SELECT OrderID, DATEDIFF(Day, OrderDate, ShippedDate) AS DaysElapsed
FROM Orders;
```

Estos ejemplos representan solo algunas de las funciones disponibles en SQL Server para la manipulación de texto y fechas. Puedes explorar más funciones en la documentación de SQL Server para adaptarlas a tus necesidades específicas.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **188. Funciones avanzadas SQL: Subquerys, Having, consultas multi tabla**

Las funciones avanzadas de SQL, como subconsultas (subqueries), `HAVING` y consultas de múltiples tablas, te permiten realizar consultas más complejas y obtener resultados más específicos en SQL Server. A continuación, te proporcionaré una explicación detallada de cada una de estas funciones junto con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

1. **Subconsultas (Subqueries):**

Las subconsultas son consultas dentro de consultas más grandes. Se utilizan para obtener un conjunto de resultados que se utiliza en otra consulta principal.

**Ejemplo 1:** Obtener todos los clientes de la tabla "`Customers`" que han realizado pedidos.

```
SELECT *
FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

En este ejemplo, la subconsulta (`SELECT CustomerID FROM Orders`) se ejecuta primero para obtener los `CustomerID` de los clientes que han realizado pedidos. Luego, esa lista de `CustomerID` se utiliza en la consulta principal para seleccionar los clientes correspondientes.

**Ejemplo 2:** Obtener todos los productos de la tabla "`Products`" que tienen un precio mayor que el promedio.

```
SELECT *
FROM Products
WHERE UnitPrice > (SELECT AVG(UnitPrice) FROM Products);
```

En este ejemplo, la subconsulta (`SELECT AVG(UnitPrice) FROM Products`) se ejecuta primero para calcular el precio promedio de los productos. Luego, esa cantidad se utiliza en la consulta principal para seleccionar los productos con un precio superior al promedio.

2. **HAVING:**

La cláusula `HAVING` se utiliza para filtrar los resultados de una consulta agregada basada en una condición específica. Se utiliza después de la cláusula `GROUP BY` y permite filtrar los grupos resultantes según una condición de agregación.

**Ejemplo:** Obtener todas las categorías de productos de la tabla "`Products`" junto con el número de productos en cada categoría, pero solo mostrar las categorías que tienen más de 5 productos.

```
SELECT CategoryID, COUNT(*) AS ProductCount
FROM Products
GROUP BY CategoryID
HAVING COUNT(*) > 5;
```

En este ejemplo, la cláusula `HAVING` se utiliza para filtrar los grupos resultantes y mostrar solo aquellos con un recuento de productos superior a 5.

3. **Consultas de múltiples tablas:**

Las consultas de múltiples tablas te permiten combinar información de dos o más tablas utilizando cláusulas `JOIN`.

**Ejemplo:** Obtener todos los pedidos de la tabla "`Orders`" junto con los nombres de los clientes de la tabla "`Customers`".

```
SELECT OrderID, OrderDate, CustomerName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

En este ejemplo, la cláusula `INNER JOIN` se utiliza para combinar los registros de las tablas "`Orders`" y "`Customers`" en función de la coincidencia de `CustomerID`.

Estos ejemplos representan solo algunas de las funciones avanzadas de SQL que puedes utilizar en SQL Server para realizar consultas más complejas y obtener resultados más específicos. Puedes combinar estas funciones y adaptarlas a tus necesidades específicas.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **189. Creación de vistas**

La creación de vistas en SQL Server permite definir consultas predefinidas que se almacenan en la base de datos y se pueden utilizar como tablas virtuales en consultas posteriores. Una vista es una representación lógica de los datos de una o más tablas y proporciona una forma conveniente de acceder a datos específicos sin tener que escribir la consulta completa cada vez. A continuación, te proporcionaré una explicación detallada de cómo crear vistas en SQL Server con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

1. **Sintaxis básica de la creación de vistas:**

La sintaxis básica para crear una vista en SQL Server es la siguiente:

```
CREATE VIEW [NombreVista] AS
SELECT columna1, columna2, ...
FROM tabla1
JOIN tabla2 ON condicion
WHERE condicion;
```

**Ejemplo de creación de vista:**

Supongamos que deseas crear una vista que muestre los nombres y países de los clientes de la tabla "`Customers`" de la base de datos Northwind. Puedes utilizar la siguiente sintaxis:

```
CREATE VIEW VistaClientes AS
SELECT ContactName AS NombreCliente, Country AS Pais
FROM Customers;
```

En este ejemplo, la vista se llama "`VistaClientes`" y se seleccionan las columnas `ContactName` y `Country` de la tabla "`Customers`". Estas columnas se renombran como "`NombreCliente`" y "`Pais`" respectivamente en la vista.

2. **Uso de una vista:**

Una vez que se ha creado una vista, se puede utilizar en consultas posteriores como si fuera una tabla virtual. Por ejemplo, puedes consultar la vista "`VistaClientes`" para obtener los nombres y países de los clientes de la siguiente manera:

```
SELECT *
FROM VistaClientes;
```

Esta consulta seleccionará todos los registros de la vista "`VistaClientes`" y mostrará los nombres y países de los clientes.

3. **Actualización de una vista:**

En SQL Server, las vistas pueden ser actualizables o no actualizables, dependiendo de la forma en que se crean y de las operaciones permitidas en las tablas subyacentes. Las vistas no actualizables se utilizan principalmente para consultas de solo lectura. Las vistas actualizables permiten realizar operaciones de inserción, actualización y eliminación en la vista, y los cambios se reflejan en las tablas subyacentes.
En la base de datos Northwind, algunas tablas están configuradas para admitir actualizaciones, mientras que otras no. Por lo tanto, debes tener en cuenta las restricciones de actualización al trabajar con vistas en esta base de datos.

Estos son solo conceptos básicos sobre la creación y uso de vistas en SQL Server. Puedes explorar más opciones y funcionalidades en la documentación de SQL Server para adaptarlas a tus necesidades específicas.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estas consultas.

[🔼](#índice)

---

## **190. Procedimientos almacenados**

Los procedimientos almacenados en SQL Server son bloques de código SQL predefinidos que se almacenan en la base de datos y se pueden llamar y ejecutar varias veces. Los procedimientos almacenados se utilizan para agrupar una serie de instrucciones SQL en una única unidad lógica, lo que facilita su reutilización, mantenimiento y seguridad. A continuación, te proporcionaré una explicación detallada de cómo crear y utilizar procedimientos almacenados en SQL Server con ejemplos utilizando la base de datos Northwind.

Antes de continuar, asegúrate de tener la base de datos Northwind instalada en tu servidor SQL Server.

1. **Sintaxis básica de creación de procedimientos almacenados:**

La sintaxis básica para crear un procedimiento almacenado en SQL Server es la siguiente:

```
CREATE PROCEDURE [NombreProcedimiento]
AS
BEGIN
    -- Declaraciones y lógica del procedimiento
END;
```

**Ejemplo de creación de un procedimiento almacenado:**

Supongamos que deseas crear un procedimiento almacenado que devuelva todos los pedidos realizados por un cliente específico en la tabla "`Orders`" de la base de datos Northwind. Puedes utilizar la siguiente sintaxis:

```
CREATE PROCEDURE GetCustomerOrders
    @CustomerID nchar(5)
AS
BEGIN
    SELECT *
    FROM Orders
    WHERE CustomerID = @CustomerID;
END;
```

En este ejemplo, el procedimiento almacenado se llama "`GetCustomerOrders`" y toma un parámetro de entrada "`@CustomerID`" que representa el `ID` del cliente. La lógica del procedimiento simplemente selecciona todos los pedidos de la tabla "`Orders`" que coinciden con el `ID` de cliente proporcionado.

2. **Ejecución de un procedimiento almacenado:**

Una vez que se ha creado un procedimiento almacenado, se puede ejecutar utilizando la siguiente sintaxis:

`EXEC [NombreProcedimiento] [Parámetros];`

Para ejecutar el procedimiento almacenado "`GetCustomerOrders`" y obtener los pedidos del cliente con `ID` "`ALFKI`", puedes utilizar el siguiente comando:

`EXEC GetCustomerOrders @CustomerID = 'ALFKI';`

3. **Modificación y eliminación de procedimientos almacenados:**

Para modificar un procedimiento almacenado existente, puedes utilizar la declaración `ALTER PROCEDURE`. Por ejemplo:

```
ALTER PROCEDURE GetCustomerOrders
    @CustomerID nchar(5),
    @OrderDate datetime
AS
BEGIN
    SELECT *
    FROM Orders
    WHERE CustomerID = @CustomerID
    AND OrderDate > @OrderDate;
END;
```

Para eliminar un procedimiento almacenado, puedes utilizar la declaración `DROP PROCEDURE`. Por ejemplo:

`DROP PROCEDURE GetCustomerOrders;`

Estos son solo conceptos básicos sobre la creación y uso de procedimientos almacenados en SQL Server. Puedes explorar más opciones y funcionalidades, como parámetros de salida, transacciones y control de errores, en la documentación de SQL Server para adaptarlos a tus necesidades específicas.

Recuerda que debes conectarte a la base de datos Northwind en tu servidor SQL Server antes de ejecutar estos comandos.

**Automatización a través de procedimientos almacenados, ejecución y administración**

La automatización a través de procedimientos almacenados en SQL Server se refiere al uso de estos objetos para ejecutar tareas y procesos de forma programada y automática. Los procedimientos almacenados permiten centralizar la lógica de negocios y la lógica de procesamiento en la base de datos, lo que facilita su ejecución y administración. A continuación, te proporcionaré una explicación detallada de cómo puedes utilizar la automatización a través de procedimientos almacenados en SQL Server, junto con ejemplos.

1. **Automatización de tareas:**

Los procedimientos almacenados se pueden utilizar para automatizar diversas tareas, como la carga de datos, la generación de informes, la actualización de registros y la programación de tareas recurrentes. Estas tareas se pueden ejecutar de forma programada utilizando un programador de tareas del sistema operativo o mediante eventos específicos en la base de datos.

**Ejemplo 1:** Crear un procedimiento almacenado que actualice el precio de todos los productos en la tabla "`Products`" en un cierto porcentaje.

```
CREATE PROCEDURE UpdateProductPrices
    @Percentage decimal(5,2)
AS
BEGIN
    UPDATE Products
    SET UnitPrice = UnitPrice * (1 + @Percentage);
END;
```

En este ejemplo, el procedimiento almacenado "`UpdateProductPrices`" recibe un parámetro de entrada "`@Percentage`" que representa el porcentaje de aumento. Al ejecutar este procedimiento, se actualizarán los precios de todos los productos en la tabla "`Products`".

**Ejemplo 2:** Crear un procedimiento almacenado que genere un informe de ventas mensuales y lo almacene en una tabla de informes.

```
CREATE PROCEDURE GenerateMonthlySalesReport
AS
BEGIN
    INSERT INTO SalesReports (Month, TotalSales)
    SELECT DATEPART(MONTH, OrderDate), SUM(TotalAmount)
    FROM Orders
    GROUP BY DATEPART(MONTH, OrderDate);
END;
```

En este ejemplo, el procedimiento almacenado "`GenerateMonthlySalesReport`" inserta los datos de ventas mensuales en una tabla "`SalesReports`". Al ejecutar este procedimiento, se generará un informe de ventas mensuales basado en los datos de la tabla "`Orders`".

2. **Ejecución de procedimientos almacenados:**

Para ejecutar un procedimiento almacenado de forma manual, puedes utilizar la siguiente sintaxis:

`EXEC [NombreProcedimiento] [Parámetros];`

Por ejemplo, para ejecutar el procedimiento almacenado "`UpdateProductPrices`" con un aumento del 10% en los precios de los productos, puedes utilizar el siguiente comando:

`EXEC UpdateProductPrices @Percentage = 0.10;`

3. **Administración de procedimientos almacenados:**

Los procedimientos almacenados se pueden administrar en SQL Server mediante la creación, modificación y eliminación de los mismos. También puedes utilizar herramientas de administración y monitoreo para realizar un seguimiento de la ejecución de los procedimientos almacenados, analizar su rendimiento y optimizar su código.

**Ejemplo:** Utilizar la vista del catálogo del sistema "`sys.procedures`" para obtener información sobre los procedimientos almacenados en la base de datos.

```
SELECT name, create_date, modify_date
FROM sys.procedures;
```

En este ejemplo, la consulta devuelve el nombre, la fecha de creación y la fecha de modificación de todos los procedimientos almacenados en la base de datos.

Recuerda que la automatización a través de procedimientos almacenados puede ayudar a mejorar la eficiencia y consistencia de las tareas en la base de datos. Sin embargo, es importante planificar y probar adecuadamente los procedimientos almacenados antes de implementarlos en un entorno de producción.

Espero que esta explicación te haya sido útil. Si tienes más preguntas, no dudes en hacerlas.

**Revisión de modelamiento de datos bajo un enfoque de inteligencia de negocios**

La revisión de modelamiento de datos bajo un enfoque de inteligencia de negocios se refiere al análisis crítico y mejora de la estructura y diseño de las bases de datos utilizadas en proyectos de inteligencia de negocios. El objetivo principal de esta revisión es asegurar que el modelamiento de datos sea óptimo para el análisis y la generación de información relevante para la toma de decisiones. A continuación, te proporcionaré una explicación detallada de la revisión de modelamiento de datos en el contexto de la inteligencia de negocios, junto con ejemplos.

1. **Identificación de los requerimientos de información:**

El primer paso en la revisión de modelamiento de datos es comprender los requerimientos de información de la organización. Esto implica identificar qué tipo de datos son necesarios para el análisis de negocios, qué preguntas se deben responder y qué información es relevante para la toma de decisiones. Estos requerimientos se traducen en dimensiones, métricas y relaciones que se deben considerar en el modelamiento de datos.

**Ejemplo:** Supongamos que una empresa de comercio electrónico desea analizar las ventas por categoría de producto, región y período de tiempo. Los requerimientos de información incluirían las dimensiones "`Categoría`", "`Región`" y "`Fecha`" y las métricas como "`Ventas totales`" y "`Cantidad de pedidos`".

2. **Evaluación del modelo de datos existente:**

Una vez que se comprenden los requerimientos de información, se debe evaluar el modelo de datos existente para determinar si cumple con esos requerimientos de manera eficiente y efectiva. Se analizan las tablas, relaciones, atributos y restricciones del modelo de datos para identificar posibles problemas o áreas de mejora.

**Ejemplo:** En un modelo de datos existente, se puede identificar que la información de ventas se encuentra dispersa en varias tablas y no existe una estructura consolidada para el análisis. Esto puede dificultar el proceso de extracción de información relevante y afectar la eficiencia del análisis.

2. **Diseño de un modelo de datos optimizado:**

Una vez identificados los problemas o áreas de mejora en el modelo de datos existente, se procede a diseñar un modelo de datos optimizado que cumpla con los requerimientos de información de manera más efectiva. Esto implica realizar cambios en la estructura, relaciones y atributos del modelo de datos para facilitar el análisis y la generación de información relevante.

**Ejemplo:** En el ejemplo anterior, se podría diseñar un modelo de datos optimizado que tenga una tabla central de ventas que contenga la información relevante para el análisis, incluyendo las dimensiones "`Categoría`", "`Región`" y "`Fecha`", así como las métricas de ventas. Esto simplificaría el proceso de análisis y mejoraría la eficiencia del mismo.

3. **Validación y ajuste del modelo de datos:**

Una vez diseñado el modelo de datos optimizado, se realiza una validación exhaustiva del mismo para asegurar que cumpla con los requerimientos de información y que los resultados obtenidos sean consistentes y confiables. Se realizan pruebas y ajustes adicionales en caso de ser necesario.

**Ejemplo:** En el ejemplo mencionado, se realizarían pruebas para verificar que el modelo de datos optimizado permite obtener información precisa y coherente sobre las ventas por categoría de producto, región y período de tiempo.

La revisión de modelamiento de datos bajo un enfoque de inteligencia de negocios es un proceso iterativo y continuo. A medida que evolucionan los requerimientos de información y cambian las necesidades de análisis, es necesario revisar y ajustar el modelo de datos para garantizar su relevancia y eficacia.

Espero que esta explicación te haya sido útil. Si tienes más preguntas, no dudes en hacerlas.

[🔼](#índice)

---

| **Inicio**            | **atrás 18**                | **Siguiente 20**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./18_Consultas_SQL.md) | [⏩](./20_Consultas_SQL.md) |
