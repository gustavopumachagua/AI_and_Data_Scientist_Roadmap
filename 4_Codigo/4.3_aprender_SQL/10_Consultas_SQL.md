| **Inicio**            | **atrás 9**                | **Siguiente 11**            |
| --------------------- | -------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./9_Consultas_SQL.md) | [⏩](./11_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                        |
| -------------------------------------------------------------------------------------------------------------- |
| [91. Programando Subconsultas y uso de Alias de Tablas](#91-programando-subconsultas-y-uso-de-alias-de-tablas) |
| [92. Conclusión Stored Procedures](#92-conclusión-stored-procedures)                                           |
| [93. Estructuras de Control](#93-estructuras-de-control)                                                       |
| [94. El condicional IF ELSE y estructura BEGIN END](#94-el-condicional-if-else-y-estructura-begin-end)         |
| [95. La función EXISTS](#95-la-función-exists)                                                                 |
| [96. El bucle WHILE](#96-el-bucle-while)                                                                       |
| [97. El condicional CASE](#97-el-condicional-case)                                                             |
| [98. Las instrucciones RETURN y BREAK](#98-las-instrucciones-return-y-break)                                   |
| [99. La estructura TRY CATCH](#99-la-estructura-try-catch)                                                     |
| [100. Conclusión estructuras de control](#100-conclusión-estructuras-de-control)                               |

---

# **Tutorial de SQL**

## **91. Programando Subconsultas y uso de Alias de Tablas**

La programación de subconsultas y el uso de alias de tablas son técnicas muy útiles en SQL Server para realizar consultas más complejas y obtener resultados más específicos. Las subconsultas permiten realizar consultas dentro de otras consultas, mientras que los alias de tablas proporcionan nombres alternativos a las tablas para simplificar la escritura de consultas.

Aquí tienes una explicación detallada de cómo programar subconsultas y utilizar alias de tablas en SQL Server, utilizando la base de datos Northwind:

1. **Subconsultas:**

Una subconsulta es una consulta que se incluye dentro de otra consulta. Puedes utilizar una subconsulta en diferentes partes de una consulta, como en la cláusula `SELECT`, `FROM`, `WHERE` o `HAVING`. La subconsulta se resuelve primero y luego se utiliza como parte de la consulta principal.

Por ejemplo, supongamos que deseas obtener el nombre de la categoría de cada producto en la tabla "`Products`". Puedes utilizar una subconsulta para obtener el nombre de la categoría a partir del campo "`CategoryID`" de la tabla "`Categories`". El siguiente ejemplo muestra cómo realizar esto:

```
SELECT ProductName,
       (SELECT CategoryName
        FROM Categories
        WHERE Categories.CategoryID = Products.CategoryID) AS CategoryName
FROM Products;
```

En este ejemplo, la subconsulta (`SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID`) se utiliza en la cláusula `SELECT` para obtener el nombre de la categoría para cada producto.

2. **Alias de tablas:**

Un alias de tabla es un nombre alternativo que se utiliza para hacer referencia a una tabla en una consulta. Los alias de tablas son útiles para simplificar la escritura de consultas, especialmente cuando se involucran múltiples tablas o se utilizan subconsultas.

Para asignar un alias a una tabla, simplemente utiliza la palabra clave `AS` seguida del alias deseado después del nombre de la tabla. Por ejemplo:

```
SELECT p.ProductName, c.CategoryName
FROM Products AS p
JOIN Categories AS c ON p.CategoryID = c.CategoryID;
```

En este ejemplo, utilizamos los alias de tabla "`p`" para la tabla "`Products`" y "`c`" para la tabla "`Categories`". Luego, utilizamos los alias en la cláusula `SELECT` y en la cláusula `JOIN` para hacer referencia a las columnas correspondientes.

Los alias de tabla también pueden ser útiles cuando se utilizan subconsultas. Por ejemplo:

```
SELECT p.ProductName, p.UnitPrice
FROM (SELECT * FROM Products WHERE Discontinued = 1) AS p;
```

En este ejemplo, la subconsulta (`SELECT * FROM Products WHERE Discontinued = 1`) se asigna al alias de tabla "`p`". Luego, utilizamos el alias en la cláusula `SELECT` para seleccionar las columnas deseadas.

En resumen, la programación de subconsultas y el uso de alias de tablas en SQL Server son técnicas poderosas para realizar consultas más complejas y obtener resultados más específicos. Las subconsultas permiten realizar consultas dentro de otras consultas, mientras que los alias de tablas proporcionan nombres alternativos a las tablas para simplificar la escritura de consultas. Estas técnicas son útiles para manipular y combinar datos de manera eficiente en la base de datos Northwind.

La programación de subconsultas y el uso de alias de tablas también se pueden aplicar en combinación con `Stored Procedures` en SQL Server. Los `Stored Procedures` permiten encapsular lógica de negocio y consultas complejas en un solo objeto, lo que facilita su reutilización y mantenimiento. Aquí tienes una explicación detallada de cómo programar subconsultas y utilizar alias de tablas con `Stored Procedures` en SQL Server, utilizando la base de datos Northwind:

1. **Creación de un Stored Procedure:**

Para comenzar, puedes crear un `Stored Procedure` que incluya subconsultas y alias de tablas. Puedes utilizar la declaración `CREATE PROCEDURE` para crear el `Stored Procedure` y definir los parámetros necesarios. Por ejemplo:

```
CREATE PROCEDURE ObtenerProductosPorCategoria
    @CategoriaID int
AS
BEGIN
    SELECT p.ProductName, c.CategoryName
    FROM Products AS p
    JOIN Categories AS c ON p.CategoryID = c.CategoryID
    WHERE c.CategoryID = @CategoriaID;
END;
```

En este ejemplo, creamos un `Stored Procedure` llamado "`ObtenerProductosPorCategoria`" que recibe un parámetro "`@CategoriaID`". La consulta dentro del `Stored Procedure` utiliza un alias de tabla "`p`" para la tabla "`Products`" y "`c`" para la tabla "`Categories`". También utiliza una subconsulta para obtener los productos de una categoría específica.

2. **Ejecución del Stored Procedure:**

Una vez que hayas creado el `Stored Procedure`, puedes ejecutarlo utilizando la instrucción `EXEC`. Puedes pasar los parámetros requeridos al `Stored Procedure` al ejecutarlo. Por ejemplo:

`EXEC ObtenerProductosPorCategoria @CategoriaID = 1;`

En este ejemplo, ejecutamos el `Stored Procedure` "`ObtenerProductosPorCategoria`" y pasamos el valor `1` al parámetro "`@CategoriaID`" para obtener los productos de la categoría correspondiente.

3. **Manipulación de los resultados del Stored Procedure:**

Puedes manipular los resultados del `Stored Procedure` utilizando variables en combinación con la cláusula `INTO`. Por ejemplo:

```
DECLARE @NombreProducto nvarchar(50);
DECLARE @NombreCategoria nvarchar(50);

EXEC ObtenerProductosPorCategoria @CategoriaID = 1
INTO @NombreProducto, @NombreCategoria;

SELECT @NombreProducto AS ProductName, @NombreCategoria AS CategoryName;
```

En este ejemplo, declaramos variables "`@NombreProducto`" y "`@NombreCategoria`" con los tipos de datos adecuados. Luego, ejecutamos el `Stored Procedure` y guardamos los resultados en las variables correspondientes utilizando la cláusula `INTO`. Finalmente, seleccionamos y mostramos los valores de las variables.

En resumen, puedes programar subconsultas y utilizar alias de tablas tanto en las consultas dentro de los `Stored Procedures` como en la manipulación de resultados. Los `Stored Procedures` encapsulan la lógica de negocio y las consultas complejas, mientras que las subconsultas y los alias de tablas permiten realizar consultas más complejas y obtener resultados más específicos. Puedes crear, ejecutar y manipular los resultados de los `Stored Procedures` utilizando estas técnicas en combinación con la base de datos Northwind.

[🔼](#índice)

---

## **92. Conclusión Stored Procedures**

En conclusión, los `Stored Procedures` en SQL Server son objetos de base de datos que contienen una o varias instrucciones SQL y se almacenan en el servidor de base de datos para su reutilización. Son una parte fundamental del lenguaje de programación Transact-SQL (`T-SQL`) y ofrecen numerosas ventajas en el desarrollo de aplicaciones y la administración de bases de datos.

Algunas de las ventajas clave de los `Stored Procedures` son:

1. **Modularidad y reutilización de código:** Los Stored Procedures permiten encapsular lógica de negocio compleja en un objeto reutilizable. Esto mejora la mantenibilidad del código y reduce la duplicación.

2. **Mejor rendimiento:** Al ejecutar un Stored Procedure, el motor de base de datos SQL Server compila y almacena en caché su plan de ejecución, lo que puede resultar en un rendimiento más rápido en comparación con las consultas ad hoc.

3. **Seguridad:** Los Stored Procedures pueden limitar el acceso a los datos y proporcionar una capa adicional de seguridad. Los usuarios pueden tener permisos para ejecutar Stored Procedures sin necesidad de acceder directamente a las tablas subyacentes.

4. **Control de transacciones:** Los Stored Procedures pueden agrupar múltiples instrucciones SQL en una transacción, lo que garantiza la consistencia de los datos y facilita el manejo de errores.

5. **Abstracción de la estructura de la base de datos:** Los Stored Procedures permiten ocultar los detalles de la estructura de la base de datos al separar la lógica de la aplicación de los detalles de implementación de la base de datos.

En resumen, los Stored Procedures en SQL Server ofrecen una forma poderosa de organizar y ejecutar lógica de negocio en la base de datos. Proporcionan modularidad, reutilización de código, mejor rendimiento, seguridad y control de transacciones. Su uso adecuado puede mejorar la eficiencia del desarrollo de aplicaciones y la administración de bases de datos, al tiempo que brinda un nivel adicional de seguridad y control sobre los datos.

[🔼](#índice)

---

## **93. Estructuras de Control**

En SQL Server, las estructuras de control son utilizadas para tomar decisiones y controlar el flujo de ejecución de las consultas y scripts. Permiten realizar acciones condicionales o repetitivas en función de ciertas condiciones. Las estructuras de control más comunes en SQL Server son las siguientes:

1. **Estructura IF:** La estructura `IF` permite ejecutar un bloque de código SQL si se cumple una condición especificada. El formato básico de la estructura `IF` en SQL Server es el siguiente:

```
IF condición
BEGIN
    -- Código a ejecutar si la condición es verdadera
END
```

Aquí hay un ejemplo utilizando la base de datos Northwind. Supongamos que queremos obtener todos los productos cuyo precio sea mayor que `$20`:

```
USE Northwind;
GO

IF EXISTS (SELECT * FROM Products WHERE UnitPrice > 20)
BEGIN
    SELECT * FROM Products WHERE UnitPrice > 20;
END
ELSE
BEGIN
    PRINT 'No se encontraron productos con un precio mayor a $20.';
END
```

En este ejemplo, la condición `UnitPrice > 20` verifica si hay algún producto en la tabla "`Products`" cuyo precio sea mayor a `$20`. Si se cumple la condición, se ejecuta la consulta `SELECT` para obtener los productos. Si la condición no se cumple, se imprime un mensaje indicando que no se encontraron productos con ese criterio.

2. **Estructura CASE:** La estructura `CASE` permite realizar múltiples evaluaciones y ejecutar diferentes bloques de código dependiendo de los resultados. Hay dos formas de escribir una estructura `CASE`: la forma simple y la forma buscada.

- **Forma simple:**

```
CASE expresión
    WHEN valor1 THEN resultado1
    WHEN valor2 THEN resultado2
    ...
    ELSE resultado_final
END
```

- **Forma buscada:**

```
CASE
    WHEN condición1 THEN resultado1
    WHEN condición2 THEN resultado2
    ...
    ELSE resultado_final
END
```

Veamos un ejemplo utilizando la base de datos Northwind. Supongamos que queremos clasificar los productos de acuerdo a su precio en tres categorías: "`Bajo`", "`Medio`" y "`Alto`":

```
USE Northwind;
GO

SELECT ProductName,
    CASE
        WHEN UnitPrice < 10 THEN 'Bajo'
        WHEN UnitPrice >= 10 AND UnitPrice <= 20 THEN 'Medio'
        ELSE 'Alto'
    END AS 'Categoría Precio'
FROM Products;
```

En este ejemplo, utilizamos la estructura `CASE` para evaluar el precio de cada producto y asignar una categoría en función de su valor. Si el precio es menor a `10`, se clasifica como "`Bajo`". Si está entre `10` y `20`, se clasifica como "`Medio`". De lo contrario, se clasifica como "`Alto`".

Estas son solo algunas de las estructuras de control disponibles en SQL Server. Puedes combinarlas y utilizarlas de diferentes formas para controlar el flujo de ejecución y realizar acciones condicionales o repetitivas en tus consultas y scripts.

[🔼](#índice)

---

## **94. El condicional IF ELSE y estructura BEGIN END**

En SQL Server, el condicional `IF ELSE` junto con la estructura `BEGIN END` se utiliza para realizar acciones condicionales en función de una condición especificada. Permite ejecutar un bloque de código si la condición es verdadera (`IF`) y otro bloque de código si la condición es falsa (`ELSE`). La estructura `BEGIN END` se utiliza para agrupar múltiples declaraciones SQL dentro de un bloque, lo que permite ejecutar varias instrucciones en cada rama del condicional.

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos verificar si hay algún producto en la tabla "`Products`" cuyo precio sea mayor a `$20`. Si es así, mostraremos los detalles de esos productos, de lo contrario, mostraremos un mensaje indicando que no se encontraron productos con un precio mayor a `$20`.

```
USE Northwind;
GO

IF EXISTS (SELECT * FROM Products WHERE UnitPrice > 20)
BEGIN
    SELECT ProductName, UnitPrice
    FROM Products
    WHERE UnitPrice > 20;
END
ELSE
BEGIN
    PRINT 'No se encontraron productos con un precio mayor a $20.';
END
```

En este ejemplo, utilizamos el condicional `IF ELSE` para verificar la existencia de productos cuyo precio sea mayor a `$20`. Si la condición `EXISTS` (`SELECT * FROM Products WHERE UnitPrice > 20`) es verdadera, se ejecuta el bloque de código dentro del primer `BEGIN` y se muestra la información de los productos que cumplen la condición. Si la condición es falsa, se ejecuta el bloque de código dentro del segundo `BEGIN` y se imprime el mensaje indicando que no se encontraron productos con un precio mayor a `$20`.

La estructura `BEGIN END` se utiliza para agrupar las instrucciones SQL dentro de cada rama del condicional. Esto permite ejecutar múltiples instrucciones en cada caso (`IF` y `ELSE`) y mantener el control del flujo de ejecución.

Es importante destacar que la estructura `IF ELSE` se puede anidar, es decir, puedes tener un condicional `IF` dentro de otro condicional `IF` o dentro de la rama `ELSE`. Esto te permite realizar evaluaciones más complejas y tomar decisiones en función de múltiples condiciones.

Recuerda que el uso de `BEGIN` y `END` es opcional si solo tienes una instrucción dentro de cada rama del condicional. Sin embargo, si deseas ejecutar múltiples instrucciones, es necesario utilizar estas estructuras para agruparlas correctamente.

[🔼](#índice)

---

## **95. La función EXISTS**

En SQL Server, la función `EXISTS` se utiliza para verificar si existe al menos un registro que cumpla una determinada condición en una consulta. Retorna un valor booleano (verdadero o falso) en función de si se encuentra o no algún registro que cumpla la condición especificada.

La función `EXISTS` se utiliza comúnmente junto con el condicional `IF` para realizar acciones condicionales en función de la existencia de registros. También se puede utilizar en subconsultas para filtrar los resultados en función de una condición.

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos verificar si existen pedidos para un cliente específico con el identificador "`ALFKI`":

```
USE Northwind;
GO

IF EXISTS (SELECT * FROM Orders WHERE CustomerID = 'ALFKI')
BEGIN
    PRINT 'El cliente ALFKI tiene pedidos.';
END
ELSE
BEGIN
    PRINT 'El cliente ALFKI no tiene pedidos.';
END
```

En este ejemplo, utilizamos la función `EXISTS` en la subconsulta (`SELECT * FROM Orders WHERE CustomerID = 'ALFKI'`). La condición `CustomerID = 'ALFKI'` verifica si hay algún pedido en la tabla "`Orders`" asociado al cliente con el identificador "`ALFKI`". Si la función `EXISTS` retorna verdadero, se ejecuta el bloque de código dentro del primer `BEGIN` y se imprime el mensaje indicando que el cliente tiene pedidos. Si la función `EXISTS` retorna falso, se ejecuta el bloque de código dentro del segundo `BEGIN` y se imprime el mensaje indicando que el cliente no tiene pedidos.

Es importante destacar que la función `EXISTS` se evalúa de manera eficiente, ya que devuelve un valor tan pronto como se encuentra un registro que cumple la condición. Esto significa que no se realiza una búsqueda completa en la tabla, sino que se detiene tan pronto como se encuentra un registro válido. Esto puede mejorar el rendimiento de la consulta, especialmente cuando se trabaja con grandes conjuntos de datos.

En resumen, la función `EXISTS` es utilizada en SQL Server para verificar la existencia de registros que cumplan una condición específica en una consulta. Es comúnmente utilizada en combinación con el condicional `IF` para realizar acciones condicionales en función de la presencia o ausencia de registros.

[🔼](#índice)

---

## **96. El bucle WHILE**

En SQL Server, el bucle `WHILE` se utiliza para repetir un bloque de código SQL mientras se cumpla una condición específica. El bloque de código se ejecuta repetidamente hasta que la condición se evalúa como falsa. Esto permite realizar iteraciones basadas en una condición y controlar el flujo de ejecución de manera repetitiva.

El bucle `WHILE` se compone de dos elementos principales: la condición y el bloque de código a repetir. La condición se evalúa antes de cada iteración. Si la condición es verdadera, se ejecuta el bloque de código. Después de la ejecución del bloque, la condición se vuelve a evaluar. Si la condición es falsa, el bucle se detiene y la ejecución continúa con la siguiente instrucción después del bucle.

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos imprimir los nombres de los productos cuyos precios sean mayores a `$50`. Utilizaremos el bucle `WHILE` para iterar sobre la tabla "`Products`" y realizar la verificación de cada producto:

```
USE Northwind;
GO

DECLARE @ProductName NVARCHAR(50);
DECLARE @Price MONEY;

DECLARE @Counter INT = 1;
DECLARE @TotalProducts INT;

SELECT @TotalProducts = COUNT(*) FROM Products;

WHILE @Counter <= @TotalProducts
BEGIN
    SELECT @ProductName = ProductName, @Price = UnitPrice
    FROM (
        SELECT ROW_NUMBER() OVER (ORDER BY ProductID) AS RowNum, ProductName, UnitPrice
        FROM Products
    ) AS ProductsWithRowNum
    WHERE RowNum = @Counter;

    IF @Price > 50
    BEGIN
        PRINT @ProductName;
    END

    SET @Counter = @Counter + 1;
END
```

En este ejemplo, declaramos variables para almacenar el nombre del producto y el precio. También inicializamos una variable de contador (`@Counter`) con `1` y obtenemos el número total de productos en la tabla "`Products`" en la variable `@TotalProducts`.

Dentro del bucle `WHILE`, utilizamos una consulta con `ROW_NUMBER()` para asignar un número de fila a cada producto en orden ascendente por el identificador del producto (`ProductID`). Luego, filtramos la consulta para obtener el producto correspondiente al valor actual del contador (`@Counter`).

Si el precio del producto es mayor a `$50`, imprimimos su nombre utilizando la instrucción `PRINT`.

Después de cada iteración, incrementamos el contador (`@Counter`) en `1` para pasar al siguiente producto en la tabla. El bucle continúa hasta que el contador alcance el número total de productos y la condición `@Counter <= @TotalProducts` se evalúe como falsa.

El bucle `WHILE` es útil cuando se requiere realizar una acción repetitiva basada en una condición que no se puede lograr con una consulta única. Sin embargo, es importante tener cuidado al utilizar bucles en consultas SQL, ya que pueden tener un impacto en el rendimiento si no se manejan correctamente.

[🔼](#índice)

---

## **97. El condicional CASE**

En SQL Server, el condicional `CASE` se utiliza para realizar evaluaciones condicionales y ejecutar diferentes bloques de código en función de los resultados. Puede ser utilizado tanto en consultas `SELECT` como en instrucciones `UPDATE` o `INSERT`.

El condicional `CASE` tiene dos formas principales: la forma simple y la forma buscada.

1. **Forma simple del condicional CASE:**

La forma simple del condicional `CASE` se utiliza para evaluar una expresión y ejecutar diferentes bloques de código en función de los valores posibles de la expresión. El formato básico es el siguiente:

```
CASE expresión
    WHEN valor1 THEN resultado1
    WHEN valor2 THEN resultado2
    ...
    ELSE resultado_final
END
```

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos clasificar los productos según su unidad de existencia. Si la unidad de existencia es menor o igual a `10`, la clasificaremos como "`Baja`"; si es mayor a `10` y menor o igual a `20`, la clasificaremos como "`Media`"; de lo contrario, la clasificaremos como "`Alta`":

```
USE Northwind;
GO

SELECT ProductName, UnitsInStock,
    CASE
        WHEN UnitsInStock <= 10 THEN 'Baja'
        WHEN UnitsInStock > 10 AND UnitsInStock <= 20 THEN 'Media'
        ELSE 'Alta'
    END AS 'Clasificación'
FROM Products;
```

En este ejemplo, utilizamos el condicional `CASE` para evaluar el valor de la columna "`UnitsInStock`" de la tabla "`Products`". Según el valor de "`UnitsInStock`", asignamos una clasificación específica a cada producto. Si el valor es menor o igual a `10`, la clasificación será "`Baja`". Si el valor está entre `10` y `20` (incluyendo ambos extremos), la clasificación será "`Media`". De lo contrario, la clasificación será "`Alta`".

2. **Forma buscada del condicional CASE:**

La forma buscada del condicional `CASE` se utiliza cuando se requieren evaluaciones más complejas y no se basan en valores específicos. En lugar de especificar valores, se especifican condiciones dentro del condicional `CASE`. El formato es el siguiente:

```
CASE
    WHEN condición1 THEN resultado1
    WHEN condición2 THEN resultado2
    ...
    ELSE resultado_final
END
```

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos clasificar los empleados en función de su país de origen. Si son de Estados Unidos, los clasificaremos como "`Nacional`"; si son de Reino Unido, los clasificaremos como "`Internacional`"; de lo contrario, los clasificaremos como "`Desconocido`":

```
USE Northwind;
GO

SELECT EmployeeID, FirstName, LastName, Country,
    CASE
        WHEN Country = 'USA' THEN 'Nacional'
        WHEN Country = 'UK' THEN 'Internacional'
        ELSE 'Desconocido'
    END AS 'Clasificación'
FROM Employees;
```

En este ejemplo, utilizamos el condicional `CASE` para evaluar el valor de la columna "`Country`" de la tabla "`Employees`". Según el valor de "`Country`", asignamos una clasificación específica a cada empleado. Si el país es "`USA`", la clasificación será "`Nacional`". Si el país es "`UK`", la clasificación será "`Internacional`". De lo contrario, la clasificación será "`Desconocido`".

En resumen, el condicional `CASE` en SQL Server es utilizado para realizar evaluaciones condicionales y ejecutar diferentes bloques de código en función de los resultados. Puede ser utilizado tanto en consultas `SELECT` como en instrucciones `UPDATE` o `INSERT`. Existen dos formas principales: la forma simple, que evalúa valores específicos, y la forma buscada, que evalúa condiciones más complejas. El condicional `CASE` es una herramienta útil para realizar transformaciones y clasificaciones en base a condiciones específicas en los datos.

[🔼](#índice)

---

## **98. Las instrucciones RETURN y BREAK**

En SQL Server, las instrucciones `RETURN` y `BREAK` se utilizan para controlar el flujo de ejecución en bloques de código, como procedimientos almacenados, funciones y bucles. Cada una tiene un propósito específico y se utiliza en diferentes contextos.

1. **Instrucción RETURN:**

La instrucción `RETURN` se utiliza para finalizar la ejecución de un procedimiento almacenado o una función y devolver un valor opcional. Cuando se encuentra una instrucción `RETURN`, se sale inmediatamente del bloque de código actual y se devuelve el control al punto de llamada.
Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos crear una función que reciba el identificador de un cliente y devuelva su nombre. Si el cliente no existe, queremos que la función devuelva un mensaje indicando que el cliente no fue encontrado:

```
USE Northwind;
GO

CREATE FUNCTION ObtenerNombreCliente (@CustomerID nvarchar(5))
RETURNS nvarchar(40)
AS
BEGIN
    DECLARE @NombreCliente nvarchar(40);

    SELECT @NombreCliente = ContactName
    FROM Customers
    WHERE CustomerID = @CustomerID;

    IF @NombreCliente IS NULL
    BEGIN
        RETURN 'Cliente no encontrado.';
    END

    RETURN @NombreCliente;
END
```

En este ejemplo, creamos una función llamada "`ObtenerNombreCliente`" que recibe el identificador de un cliente como parámetro. Dentro de la función, realizamos una consulta para obtener el nombre del cliente asociado al identificador proporcionado.

Si el nombre del cliente es nulo, utilizamos la instrucción `RETURN` para salir de la función y devolver el mensaje "`Cliente no encontrado.`". Si el nombre del cliente existe, utilizamos la instrucción `RETURN` para devolver el nombre del cliente.

2. **Instrucción BREAK:**

La instrucción `BREAK` se utiliza en bucles (como `WHILE` y `FOR`) para salir inmediatamente del bucle y continuar con la ejecución de la siguiente instrucción fuera del bucle.
Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos imprimir los nombres de los productos hasta que se encuentre un producto con un precio mayor a `$100`:

```
USE Northwind;
GO

DECLARE @ProductName nvarchar(50);
DECLARE @Price money;

DECLARE @Counter INT = 1;
DECLARE @TotalProducts INT;

SELECT @TotalProducts = COUNT(*) FROM Products;

WHILE @Counter <= @TotalProducts
BEGIN
    SELECT @ProductName = ProductName, @Price = UnitPrice
    FROM (
        SELECT ROW_NUMBER() OVER (ORDER BY ProductID) AS RowNum, ProductName, UnitPrice
        FROM Products
    ) AS ProductsWithRowNum
    WHERE RowNum = @Counter;

    IF @Price > 100
    BEGIN
        PRINT 'Se encontró un producto con precio mayor a $100.';
        BREAK;
    END

    PRINT @ProductName;

    SET @Counter = @Counter + 1;
END
```

En este ejemplo, utilizamos el bucle `WHILE` para iterar sobre la tabla "`Products`" y verificar el precio de cada producto. Si encontramos un producto con un precio mayor a `$100`, utilizamos la instrucción `BREAK` para salir del bucle y mostrar un mensaje indicando que se encontró un producto con precio mayor a `$100`. De lo contrario, imprimimos el nombre del producto y continuamos con la siguiente iteración del bucle.

La instrucción `BREAK` es útil cuando se necesita terminar prematuramente un bucle en función de una condición específica. Permite salir del bucle antes de que se haya completado la iteración completa.

En resumen, las instrucciones `RETURN` y `BREAK` son utilizadas en SQL Server para controlar el flujo de ejecución en bloques de código. `RETURN` se utiliza para finalizar la ejecución de un procedimiento almacenado o una función y devolver un valor opcional, mientras que `BREAK` se utiliza en bucles para salir del bucle de manera prematura. Ambas instrucciones son herramientas importantes para el control del flujo de ejecución y permiten personalizar el comportamiento de los bloques de código en función de condiciones específicas.

[🔼](#índice)

---

## **99. La estructura TRY CATCH**

En SQL Server, la estructura `TRY CATCH` se utiliza para capturar y manejar errores que pueden ocurrir durante la ejecución de un bloque de código. Permite gestionar de manera controlada las excepciones y tomar acciones específicas en caso de producirse un error.

La estructura `TRY CATCH` consta de dos partes principales: el bloque `TRY` y el bloque `CATCH`.

El bloque `TRY` es el bloque de código donde se ejecutan las instrucciones que pueden generar una excepción. Dentro de este bloque, se incluye el código que se desea proteger y controlar en caso de que se produzca un error.

El bloque `CATCH` es el bloque donde se manejan las excepciones capturadas. Si ocurre una excepción dentro del bloque `TRY`, el control se transfiere automáticamente al bloque `CATCH` correspondiente, donde se pueden realizar acciones de manejo de errores, como registrar el error, enviar notificaciones, realizar operaciones de limpieza, etc.

Aquí tienes un ejemplo utilizando la base de datos Northwind. Supongamos que queremos insertar un nuevo registro en la tabla "`Customers`", pero también queremos manejar cualquier excepción que pueda ocurrir durante la inserción:

```
USE Northwind;
GO

BEGIN TRY
    INSERT INTO Customers (CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Country)
    VALUES ('CUSTOMER1', 'Customer One', 'John Doe', 'Manager', '123 Main St', 'Seattle', 'USA');

    PRINT 'Registro insertado correctamente.';
END TRY
BEGIN CATCH
    PRINT 'Error al insertar el registro:';
    PRINT ERROR_MESSAGE();
END CATCH
```

En este ejemplo, utilizamos la estructura `TRY CATCH` para intentar realizar una inserción en la tabla "`Customers`". Dentro del bloque `TRY`, realizamos la inserción con los valores especificados.

Si la inserción tiene éxito, se imprime un mensaje indicando que el registro se insertó correctamente.

Si ocurre un error durante la inserción, el control se transfiere al bloque `CATCH` correspondiente. Dentro del bloque `CATCH`, se imprime un mensaje de error, que incluye el mensaje de error específico devuelto por SQL Server, obtenido a través de la función `ERROR_MESSAGE()`.

La estructura `TRY CATCH` es útil para gestionar errores y evitar que un error detenga por completo la ejecución de un bloque de código. Permite capturar las excepciones, realizar acciones específicas en función del tipo de error y mantener el control del flujo de ejecución en situaciones de error.

Es importante destacar que la estructura `TRY CATCH` no puede capturar todos los errores, como aquellos que ocurren fuera del alcance del bloque `TRY`. Sin embargo, es una herramienta valiosa para manejar la mayoría de los errores que pueden ocurrir dentro del bloque protegido.

[🔼](#índice)

---

## **100. Conclusión estructuras de control**

En conclusión, las estructuras de control en SQL Server son herramientas poderosas que permiten controlar el flujo de ejecución de un programa, realizar evaluaciones condicionales y manejar excepciones. Estas estructuras proporcionan la capacidad de personalizar el comportamiento de un bloque de código en función de condiciones específicas y manejar errores de manera controlada.

Aquí hay un resumen de las estructuras de control mencionadas y su uso en SQL Server con un ejemplo utilizando la base de datos Northwind:

1. **Estructura IF-ELSE:** Permite realizar evaluaciones condicionales y ejecutar diferentes bloques de código según el resultado de la evaluación. Por ejemplo, clasificar productos según su unidad de existencia.

2. **Estructura BEGIN-END:** Agrupa múltiples instrucciones en un bloque de código para que se ejecuten como una unidad. Es utilizado en combinación con otras estructuras de control. Por ejemplo, en un procedimiento almacenado.

3. **Función EXISTS:** Se utiliza para verificar la existencia de registros en una tabla o subconsulta. Puede ser útil para realizar operaciones condicionales en base a la presencia o ausencia de datos. Por ejemplo, verificar si hay productos en la tabla "`Products`".

4. **Bucle WHILE:** Se utiliza para repetir un bloque de código mientras se cumple una condición específica. Es útil cuando se necesita ejecutar una serie de instrucciones varias veces. Por ejemplo, imprimir los nombres de los productos hasta encontrar uno con un precio mayor a `$100`.

5. **Condicional CASE:** Permite realizar evaluaciones condicionales más complejas y ejecutar diferentes bloques de código según los valores o condiciones especificadas. Puede ser utilizado para transformar datos o asignar categorías. Por ejemplo, clasificar empleados según su país de origen.

6. **Estructura TRY CATCH:** Permite capturar y manejar excepciones que ocurren durante la ejecución de un bloque de código. Permite controlar de manera controlada las excepciones y tomar acciones específicas en caso de errores. Por ejemplo, realizar una inserción en la tabla "`Customers`" y manejar cualquier excepción que pueda ocurrir.

En general, estas estructuras de control brindan flexibilidad y poder para escribir consultas y procedimientos más robustos y eficientes en SQL Server. Su comprensión y uso adecuado son fundamentales para lograr un código SQL efectivo y manejar situaciones excepcionales de manera controlada.

[🔼](#índice)

---

| **Inicio**            | **atrás 9**                | **Siguiente 11**            |
| --------------------- | -------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./9_Consultas_SQL.md) | [⏩](./11_Consultas_SQL.md) |
