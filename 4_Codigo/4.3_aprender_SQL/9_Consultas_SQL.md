| **Inicio**            | **atrás 8**                | **Siguiente 10**            |
| --------------------- | -------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./8_Consultas_SQL.md) | [⏩](./10_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------------- |
| [81. Operador AND](#81-operador-and)                                                                                        |
| [82. Operador OR](#82-operador-or)                                                                                          |
| [83. Operador IN](#83-operador-in)                                                                                          |
| [84. Operador LIKE](#84-operador-like)                                                                                      |
| [85. Operador NOT](#85-operador-not)                                                                                        |
| [86. Operador BETWEEN](#86-operador-between)                                                                                |
| [87. Combinando Operadores](#87-combinando-operadores)                                                                      |
| [88. Stored Procedures](#88-stored-procedures)                                                                              |
| [89. ¿Qué es un Stored Procedure? Estructura y manipulación](#89-¿qué-es-un-stored-procedure-estructura-y-manipulación)     |
| [90. ¿Qué es una variable? Uso de ISNULL para evaluar valores](#90-¿qué-es-una-variable-uso-de-isnull-para-evaluar-valores) |

---

# **Tutorial de SQL**

## **81. Operador AND**

En SQL Server, el operador lógico `AND` se utiliza para combinar dos o más condiciones en una consulta, y devuelve `true` si todas las condiciones son verdaderas. El operador `AND` se utiliza para filtrar los registros que cumplen todas las condiciones especificadas en una consulta.

Aquí tienes una explicación detallada de cómo utilizar el operador `AND` en SQL Server con la base de datos Northwind:

El operador `AND` se utiliza para combinar condiciones en una cláusula `WHERE` para filtrar los registros de una tabla. La sintaxis básica es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE condition1 AND condition2;
```

Por ejemplo, supongamos que deseas obtener los productos de la categoría "`Beverages`" con un precio mayor a `$10`. Puedes usar el operador `AND` para combinar las condiciones en la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE CategoryID = 1 AND UnitPrice > 10;
```

En esta consulta, se utiliza la cláusula `WHERE` para filtrar los registros de la tabla `Products`. La condición `CategoryID = 1` se evalúa para seleccionar los productos de la categoría "`Beverages`", y la condición `UnitPrice > 10` se evalúa para seleccionar los productos con un precio mayor a `$10`. El operador `AND` se utiliza para combinar ambas condiciones, y solo se seleccionarán los productos que cumplan ambas condiciones.

Es importante tener en cuenta que todas las condiciones separadas por el operador `AND` deben ser verdaderas para que se seleccione un registro. Si alguna de las condiciones es falsa, el registro no será seleccionado.

El operador `AND` se puede utilizar con más de dos condiciones. Por ejemplo, si deseas obtener los productos de la categoría "`Beverages`" con un precio mayor a `$10` y con una cantidad en stock mayor a `20`, puedes combinar las condiciones con el operador `AND` de la siguiente manera:

```
SELECT ProductName, UnitPrice, UnitsInStock
FROM Products
WHERE CategoryID = 1 AND UnitPrice > 10 AND UnitsInStock > 20;
```

En esta consulta, se agregó una tercera condición `UnitsInStock > 20` para seleccionar los productos con una cantidad en `stock` mayor a `20`.

En resumen, el operador `AND` en SQL Server se utiliza para combinar dos o más condiciones en una consulta y devuelve `true` si todas las condiciones son verdaderas. Se utiliza para filtrar los registros que cumplen todas las condiciones especificadas. El operador `AND` es útil cuando se desea establecer múltiples condiciones y filtrar registros basados en varias condiciones en una consulta.

[🔼](#índice)

---

## **82. Operador OR**

En SQL Server, el operador lógico `OR` se utiliza para combinar dos o más condiciones en una consulta y devuelve `true` si al menos una de las condiciones es verdadera. El operador `OR` se utiliza para filtrar los registros que cumplen al menos una de las condiciones especificadas en una consulta.

Aquí tienes una explicación detallada de cómo utilizar el operador `OR` en SQL Server con la base de datos Northwind:

El operador `OR` se utiliza para combinar condiciones en una cláusula `WHERE` para filtrar los registros de una tabla. La sintaxis básica es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE condition1 OR condition2;
```

Por ejemplo, supongamos que deseas obtener los productos que sean de la categoría "`Beverages`" o que tengan un precio mayor a `$10`. Puedes usar el operador `OR` para combinar las condiciones en la cláusula `WHERE`. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE CategoryID = 1 OR UnitPrice > 10;
```

En esta consulta, se utiliza la cláusula `WHERE` para filtrar los registros de la tabla `Products`. La condición `CategoryID = 1` se evalúa para seleccionar los productos de la categoría "`Beverages`", y la condición `UnitPrice > 10` se evalúa para seleccionar los productos con un precio mayor a `$10`. El operador `OR` se utiliza para combinar ambas condiciones, y se seleccionarán los productos que cumplan al menos una de las condiciones.

Es importante tener en cuenta que si al menos una de las condiciones separadas por el operador `OR` es verdadera, se seleccionará el registro. Si ambas condiciones son falsas, el registro no será seleccionado.

El operador `OR` se puede utilizar con más de dos condiciones. Por ejemplo, si deseas obtener los productos que sean de la categoría "`Beverages`" o que tengan un precio mayor a `$10` o que tengan una cantidad en stock menor a `10`, puedes combinar las condiciones con el operador `OR` de la siguiente manera:

```
SELECT ProductName, UnitPrice, UnitsInStock
FROM Products
WHERE CategoryID = 1 OR UnitPrice > 10 OR UnitsInStock < 10;
```

En esta consulta, se agregó una tercera condición `UnitsInStock < 10` para seleccionar los productos con una cantidad en stock menor a `10`.

En resumen, el operador `OR` en SQL Server se utiliza para combinar dos o más condiciones en una consulta y devuelve `true` si al menos una de las condiciones es verdadera. Se utiliza para filtrar los registros que cumplen al menos una de las condiciones especificadas. El operador `OR` es útil cuando se desea establecer múltiples condiciones y filtrar registros basados en al menos una de las condiciones en una consulta.

[🔼](#índice)

---

## **83. Operador IN**

En SQL Server, el operador `IN` se utiliza para especificar múltiples valores en una condición y permite verificar si una columna coincide con cualquiera de esos valores. El operador `IN` es útil cuando se desea filtrar registros basados en una lista de valores predefinidos.

Aquí tienes una explicación detallada de cómo utilizar el operador `IN` en SQL Server con la base de datos Northwind:

El operador `IN` se utiliza en una cláusula `WHERE` para verificar si una columna coincide con cualquiera de los valores especificados en una lista. La sintaxis básica es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

Por ejemplo, supongamos que deseas obtener los productos cuyos nombres sean "`Chai`", "`Chang`" o "`Aniseed Syrup`". Puedes utilizar el operador `IN` para especificar los valores en una lista. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE ProductName IN ('Chai', 'Chang', 'Aniseed Syrup');
```

En esta consulta, la cláusula `WHERE` verifica si la columna `ProductName` coincide con cualquiera de los valores especificados en la lista. Los registros que tengan los nombres "`Chai`", "`Chang`" o "`Aniseed Syrup`" serán seleccionados.

El operador `IN` también se puede combinar con subconsultas para obtener los valores de otra tabla. Por ejemplo, si deseas obtener los pedidos realizados por clientes específicos, puedes utilizar el operador `IN` con una subconsulta que devuelva los `IDs` de cliente deseados. La consulta sería similar a esto:

```
SELECT OrderID, OrderDate
FROM Orders
WHERE CustomerID IN (SELECT CustomerID FROM Customers WHERE Country = 'Mexico');
```

En esta consulta, la subconsulta (`SELECT CustomerID FROM Customers WHERE Country = 'Mexico'`) devuelve los `IDs` de cliente para los clientes de México. El operador `IN` verifica si el `CustomerID` de cada pedido se encuentra en la lista de `IDs` de cliente de México. Los pedidos realizados por clientes de México serán seleccionados.

Es importante tener en cuenta que el operador `IN` puede ser más eficiente y legible que utilizar múltiples condiciones `OR`. Además, el operador `IN` puede utilizarse con valores numéricos, cadenas de texto y fechas.

En resumen, el operador `IN` en SQL Server se utiliza para verificar si una columna coincide con cualquiera de los valores especificados en una lista. Se utiliza en una cláusula `WHERE` para filtrar registros basados en una lista predefinida de valores. El operador `IN` es útil cuando se desea establecer múltiples valores en una condición y verificar si una columna coincide con cualquiera de esos valores en una consulta.

[🔼](#índice)

---

## **84. Operador LIKE**

En SQL Server, el operador `LIKE` se utiliza para realizar búsquedas de patrones en una columna de texto. El operador `LIKE` es útil cuando se desea buscar registros que coincidan con un patrón específico utilizando comodines.

Aquí tienes una explicación detallada de cómo utilizar el operador `LIKE` en SQL Server con la base de datos Northwind:

El operador `LIKE` se utiliza en una cláusula `WHERE` para buscar registros que coincidan con un patrón especificado. El operador `LIKE` utiliza comodines para representar caracteres desconocidos o variables en un patrón de búsqueda. Los comodines más comúnmente utilizados son:

- El símbolo `%` representa cualquier secuencia de cero o más caracteres.
- El símbolo `_` representa un único carácter.

La sintaxis básica del operador `LIKE` es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```

Por ejemplo, supongamos que deseas obtener los productos cuyos nombres comiencen con la letra "`C`". Puedes utilizar el operador `LIKE` con el comodín `%` para buscar cualquier secuencia de caracteres después de la letra "`C`". La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE ProductName LIKE 'C%';
```

En esta consulta, la cláusula `WHERE` verifica si la columna `ProductName` comienza con la letra "`C`". Los registros que cumplan esta condición, como "`Chai`", "`Chang`" y "`Chef Anton's Cajun Seasoning`", serán seleccionados.

También puedes utilizar el operador `LIKE` para buscar registros que contengan una secuencia específica de caracteres en cualquier posición. Por ejemplo, si deseas obtener los productos cuyos nombres contengan la subcadena "`an`", puedes utilizar el comodín `%` antes y después de la subcadena. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE ProductName LIKE '%an%';
```

En esta consulta, la cláusula `WHERE` verifica si la columna `ProductName` contiene la subcadena "`an`" en cualquier posición. Los registros que cumplan esta condición, como "`Chai`", "`Tofu Pate`" y "`Aniseed Syrup`", serán seleccionados.

El operador `LIKE` también se puede combinar con otros caracteres y comodines para realizar búsquedas más específicas. Por ejemplo, si deseas obtener los productos cuyos nombres contengan exactamente tres caracteres y comiencen con la letra "`A`", puedes utilizar el comodín `_` junto con el operador `LIKE`. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE ProductName LIKE 'A__';
```

En esta consulta, la cláusula `WHERE` verifica si la columna `ProductName` tiene tres caracteres y comienza con la letra "`A`". Los registros que cumplan esta condición, como "`Aniseed Syrup`" y "`Alice Mutton`", serán seleccionados.

Es importante tener en cuenta que el operador `LIKE` distingue entre mayúsculas y minúsculas a menos que se especifique lo contrario. Además, el operador `LIKE` también se puede utilizar con otros operadores en combinación, como `AND` y `OR`, para crear condiciones de búsqueda más complejas.

En resumen, el operador `LIKE` en SQL Server se utiliza para buscar registros que coincidan con un patrón específico en una columna de texto. Permite utilizar comodines como `%` y `_` para representar caracteres desconocidos o variables en un patrón de búsqueda. El operador `LIKE` es útil cuando se desea buscar registros que cumplan ciertas condiciones basadas en patrones de texto.

[🔼](#índice)

---

## **85. Operador NOT**

En SQL Server, el operador `NOT` se utiliza para negar una condición en una consulta. El operador `NOT` se coloca delante de una condición y devuelve `true` si la condición es falsa, y `false` si la condición es verdadera. Permite realizar operaciones de negación lógica en SQL Server.

Aquí tienes una explicación detallada de cómo utilizar el operador `NOT` en SQL Server con la base de datos Northwind:

El operador `NOT` se utiliza para negar una condición en una cláusula `WHERE`. La sintaxis básica es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE NOT condition;
```

Por ejemplo, supongamos que deseas obtener los productos cuyos precios no sean mayores a `$20`. Puedes utilizar el operador `NOT` para negar la condición `UnitPrice > 20`. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE NOT UnitPrice > 20;
```

En esta consulta, la cláusula `WHERE` verifica si la columna `UnitPrice` no es mayor a `$20`. Los registros que cumplan esta condición, es decir, aquellos cuyo precio no sea mayor a `$20`, serán seleccionados.

El operador `NOT` también se puede utilizar junto con otros operadores lógicos, como `AND` y `OR`, para crear condiciones de negación más complejas. Por ejemplo, si deseas obtener los productos cuyos precios no sean mayores a `$20` y no pertenezcan a la categoría "`Beverages`", puedes combinar las condiciones con los operadores `AND` y `NOT` de la siguiente manera:

```
SELECT column_name(s)
FROM table_name
WHERE NOT condition;
```

Por ejemplo, supongamos que deseas obtener los productos cuyos precios no sean mayores a `$20`. Puedes utilizar el operador `NOT` para negar la condición `UnitPrice > 20`. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE NOT UnitPrice > 20;
```

En esta consulta, la cláusula `WHERE` verifica si la columna `UnitPrice` no es mayor a `$20`. Los registros que cumplan esta condición, es decir, aquellos cuyo precio no sea mayor a `$20`, serán seleccionados.

El operador `NOT` también se puede utilizar junto con otros operadores lógicos, como `AND` y `OR`, para crear condiciones de negación más complejas. Por ejemplo, si deseas obtener los productos cuyos precios no sean mayores a `$20` y no pertenezcan a la categoría "`Beverages`", puedes combinar las condiciones con los operadores `AND` y `NOT` de la siguiente manera:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE NOT (UnitPrice > 20 AND CategoryID = 1);
```

En esta consulta, se utiliza el operador `NOT` junto con el operador `AND` para negar la condición (`UnitPrice > 20 AND CategoryID = 1`). Los registros que no cumplan esta condición, es decir, aquellos cuyo precio no sea mayor a `$20` o no pertenezcan a la categoría "`Beverages`", serán seleccionados.

Es importante tener en cuenta que el operador `NOT` puede utilizarse para negar cualquier condición en una cláusula `WHERE`, lo que permite filtrar registros que no cumplan ciertas condiciones. Además, el operador `NOT` se puede combinar con otros operadores lógicos para crear condiciones más complejas.

En resumen, el operador `NOT` en SQL Server se utiliza para negar una condición en una consulta. Permite realizar operaciones de negación lógica y filtrar registros que no cumplan una condición específica. El operador `NOT` se utiliza en combinación con la cláusula `WHERE` para negar una condición y seleccionar registros que no la cumplan.

[🔼](#índice)

---

## **86. Operador BETWEEN**

En SQL Server, el operador `BETWEEN` se utiliza para verificar si un valor se encuentra dentro de un rango especificado. El operador `BETWEEN` se utiliza en una cláusula `WHERE` para simplificar la verificación de valores que se encuentren entre dos límites, inclusive.

Aquí tienes una explicación detallada de cómo utilizar el operador `BETWEEN` en SQL Server con la base de datos Northwind:

El operador `BETWEEN` se utiliza para verificar si un valor se encuentra dentro de un rango especificado. La sintaxis básica es la siguiente:

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

Por ejemplo, supongamos que deseas obtener los productos cuyos precios estén entre `$10` y `$20`. Puedes utilizar el operador `BETWEEN` para especificar el rango de valores. La consulta sería similar a esto:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice BETWEEN 10 AND 20;
```

En esta consulta, la cláusula `WHERE` verifica si la columna `UnitPrice` se encuentra entre los valores `$10` y `$20`, inclusive. Los registros que cumplan esta condición, es decir, aquellos cuyos precios estén dentro del rango especificado, serán seleccionados.

El operador `BETWEEN` también se puede utilizar con fechas para verificar si una fecha se encuentra dentro de un rango. Por ejemplo, si deseas obtener los pedidos realizados entre el 1 de enero de 1997 y el 31 de diciembre de 1997, puedes utilizar el operador `BETWEEN` con fechas. La consulta sería similar a esto:

```
SELECT OrderID, OrderDate
FROM Orders
WHERE OrderDate BETWEEN '1997-01-01' AND '1997-12-31';
```

En esta consulta, la cláusula `WHERE` verifica si la columna `OrderDate` se encuentra entre las fechas especificadas. Los pedidos que cumplan esta condición, es decir, aquellos que se hayan realizado entre el 1 de enero de 1997 y el 31 de diciembre de 1997, serán seleccionados.

Es importante tener en cuenta que el operador `BETWEEN` incluye los límites especificados en la comparación. Si deseas excluir uno de los límites, puedes utilizar los operadores de comparación `<` y `>` en su lugar.

En resumen, el operador `BETWEEN` en SQL Server se utiliza para verificar si un valor se encuentra dentro de un rango especificado. Se utiliza en una cláusula `WHERE` para simplificar la verificación de valores que estén entre dos límites, inclusivos. El operador `BETWEEN` es útil cuando se desea seleccionar registros que cumplan una condición basada en un rango de valores.

[🔼](#índice)

---

## **87. Combinando Operadores**

En SQL Server, es posible combinar operadores para construir condiciones más complejas en las consultas. Los operadores más comunes que se pueden combinar son `AND`, `OR` y `NOT`. Estos operadores permiten agregar múltiples condiciones a una cláusula `WHERE` y especificar cómo deben combinarse para filtrar los registros de la base de datos.

Aquí tienes una explicación detallada de cómo combinar operadores en SQL Server con la base de datos Northwind:

1. **Operador AND:**

El operador `AND` se utiliza para combinar múltiples condiciones y especificar que ambas condiciones deben ser verdaderas para que se seleccione un registro. En otras palabras, se utiliza para realizar una operación lógica "`Y`". Por ejemplo:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE CategoryID = 1 AND UnitPrice > 20;
```

En esta consulta, se seleccionarán los productos cuya categoría sea igual a `1` y cuyo precio unitario sea mayor a `20`. Ambas condiciones deben cumplirse para que un producto sea incluido en el resultado.

2. **Operador OR:**

El operador `OR` se utiliza para combinar múltiples condiciones y especificar que al menos una de las condiciones debe ser verdadera para que se seleccione un registro. En otras palabras, se utiliza para realizar una operación lógica "`O`". Por ejemplo:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE CategoryID = 1 OR UnitPrice > 20;
```

En esta consulta, se seleccionarán los productos cuya categoría sea igual a `1` o cuyo precio unitario sea mayor a `20`. Si cualquiera de las dos condiciones es verdadera, el producto será incluido en el resultado.

3. **Operador NOT:**

El operador `NOT` se utiliza para negar una condición en una consulta. Se coloca delante de una condición y devuelve `true` si la condición es falsa, y `false` si la condición es verdadera. Por ejemplo:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE NOT CategoryID = 1;
```

En esta consulta, se seleccionarán los productos cuya categoría no sea igual a `1`. La condición se niega con el operador `NOT`, lo que significa que se seleccionarán todos los productos que no cumplan la condición especificada.

Es posible combinar estos operadores para construir condiciones más complejas. Por ejemplo:

```
SELECT ProductName, UnitPrice
FROM Products
WHERE (CategoryID = 1 AND UnitPrice > 20) OR CategoryID = 2;
```

En esta consulta, se seleccionarán los productos cuya categoría sea igual a `1` y cuyo precio unitario sea mayor a `20`, o aquellos cuya categoría sea igual a `2`. La cláusula `WHERE` combina las condiciones utilizando los operadores `AND` y `OR`.

En resumen, combinar operadores en SQL Server permite construir condiciones más complejas en las consultas. Los operadores `AND`, `OR` y `NOT` se utilizan para combinar condiciones y especificar cómo deben evaluarse. Al combinar estos operadores, es posible realizar filtrados más sofisticados y obtener los resultados deseados de la base de datos.

[🔼](#índice)

## **88. Stored Procedures**

En SQL Server, las `Stored Procedures` (Procedimientos almacenados) son un conjunto de instrucciones SQL predefinidas y almacenadas en la base de datos como un objeto. Estas instrucciones pueden ser invocadas y ejecutadas posteriormente utilizando su nombre. Las `Stored Procedures` son muy útiles en el desarrollo de aplicaciones y en la administración de bases de datos, ya que ofrecen ventajas como reutilización de código, seguridad y mejor rendimiento.

Aquí tienes una explicación detallada de las `Stored Procedures` en SQL Server, junto con un ejemplo utilizando la base de datos Northwind:

1. **Creación de una Stored Procedure:**

Para crear una `Stored Procedure` en SQL Server, se utiliza la declaración `CREATE PROCEDURE`, seguida del nombre de la procedimiento y el conjunto de instrucciones SQL que conforman su cuerpo. Por ejemplo, supongamos que deseamos crear una `Stored Procedure` en la base de datos Northwind que recupere los productos de una categoría específica:

```
CREATE PROCEDURE GetProductsByCategory
    @CategoryID INT
AS
BEGIN
    SELECT ProductName, UnitPrice
    FROM Products
    WHERE CategoryID = @CategoryID;
END;
```

En este ejemplo, creamos una `Stored Procedure` llamada "`GetProductsByCategory`" que acepta un parámetro de entrada "`@CategoryID`" de tipo `INT`. Dentro del cuerpo de la procedimiento, utilizamos una consulta `SELECT` para recuperar los productos de la tabla "`Products`" que pertenezcan a la categoría especificada.

2. **Ejecución de una Stored Procedure:**

Una vez creada la `Stored Procedure`, podemos ejecutarla utilizando la declaración `EXEC` o `EXECUTE`, seguida del nombre del procedimiento y los valores de los parámetros necesarios. Por ejemplo, para ejecutar la `Stored Procedure` "`GetProductsByCategory`" y obtener los productos de la categoría `1`, podemos utilizar la siguiente sentencia:

`EXEC GetProductsByCategory @CategoryID = 1;`

Esta sentencia ejecuta la `Stored Procedure` y pasa el valor `1` al parámetro "`@CategoryID`". Como resultado, obtendremos los productos de la categoría `1`.

3. **Beneficios de las Stored Procedures:**

Las `Stored Procedures` ofrecen varios beneficios en SQL Server:

- **Reutilización de código:** Al utilizar `Stored Procedures`, podemos escribir una vez el conjunto de instrucciones SQL y luego invocar la procedimiento en múltiples ocasiones, evitando la necesidad de repetir el mismo código en diferentes lugares.

- **Mejor rendimiento:** Las `Stored Procedures` pueden ser compiladas y almacenadas en caché por el motor de base de datos, lo que puede mejorar el rendimiento al ejecutarlas repetidamente.

- **Seguridad:** Las `Stored Procedures` permiten definir permisos de acceso específicos, lo que ofrece un nivel adicional de seguridad. Los usuarios solo necesitan tener permisos para ejecutar la procedimiento, sin necesidad de acceder directamente a las tablas subyacentes.

- **Mantenibilidad:** Al tener la lógica de negocio encapsulada en `Stored Procedures`, es más fácil realizar cambios y actualizaciones en la base de datos sin afectar el código de las aplicaciones.

En resumen, las `Stored Procedures` en SQL Server son conjuntos de instrucciones SQL predefinidas y almacenadas en la base de datos. Ofrecen ventajas como reutilización de código, mejor rendimiento, seguridad y mantenibilidad. Las `Stored Procedures` se crean utilizando la declaración `CREATE PROCEDURE` y se ejecutan utilizando la declaración `EXEC` o `EXECUTE`. Son una herramienta poderosa en el desarrollo de aplicaciones y la administración de bases de datos.

[🔼](#índice)

---

## **89. ¿Qué es un Stored Procedure? Estructura y manipulación**

Un `Stored Procedure` (Procedimiento Almacenado) en SQL Server es un conjunto de instrucciones SQL predefinidas que se guardan en la base de datos como un objeto. Pueden aceptar parámetros de entrada y devolver resultados o realizar acciones en la base de datos. Los `Stored Procedures` son muy utilizados en el desarrollo de aplicaciones y en la administración de bases de datos, ya que ofrecen ventajas como reutilización de código, mejor rendimiento y seguridad.

Aquí tienes una explicación detallada de la estructura y manipulación de `Stored Procedures` en SQL Server, utilizando la base de datos Northwind:

1. **Estructura de un Stored Procedure:**

La estructura básica de un `Stored Procedure` en SQL Server consta de tres partes principales: la declaración, el cuerpo y las opciones.

- **Declaración:**

La declaración define el nombre del `Stored Procedure` y los parámetros de entrada y salida (opcionales) que puede aceptar. Los parámetros permiten que los valores se pasen al procedimiento y se utilicen en las instrucciones SQL internas. Por ejemplo:

```
CREATE PROCEDURE NombreProcedimiento
    @Parametro1 tipo_dato,
    @Parametro2 tipo_dato OUTPUT
AS
BEGIN
    -- Cuerpo del Stored Procedure
END;
```

En este ejemplo, "`NombreProcedimiento`" es el nombre del `Stored Procedure` y "`@Parametro1`" y "`@Parametro2`" son los parámetros que puede aceptar.

- **Cuerpo:**

El cuerpo del `Stored Procedure` contiene las instrucciones SQL que se ejecutarán cuando se llame al procedimiento. Puedes incluir cualquier instrucción SQL válida en el cuerpo, como `SELECT`, `INSERT`, `UPDATE` o `DELETE`, junto con lógica de control como condicionales (`IF-ELSE`) y bucles (`WHILE`). Por ejemplo:

```
CREATE PROCEDURE GetCustomersByCountry
    @Country VARCHAR(50)
AS
BEGIN
    SELECT CustomerID, CompanyName, ContactName
    FROM Customers
    WHERE Country = @Country;
END;
```

En este ejemplo, creamos un `Stored Procedure` llamado "`GetCustomersByCountry`" que acepta un parámetro de entrada "`@Country`" y selecciona los clientes de la tabla "`Customers`" que se encuentren en el país especificado.

- **Opciones:**

Las opciones son configuraciones adicionales que se pueden especificar al crear un `Stored Procedure`, como opciones de seguridad, opciones de rendimiento o opciones de compatibilidad. Estas opciones son opcionales y dependen de los requisitos específicos de tu aplicación.

2. **Manipulación de un Stored Procedure:**

Una vez creado un `Stored Procedure`, se puede llamar y ejecutar desde otras partes de tu código, como una aplicación o una consulta SQL.

- **Ejecución del Stored Procedure:**

La forma más común de ejecutar un `Stored Procedure` es utilizando la instrucción `EXEC` o `EXECUTE`, seguida del nombre del procedimiento y los valores de los parámetros necesarios. Por ejemplo:

`EXEC NombreProcedimiento @Parametro1 = valor1, @Parametro2 = valor2 OUTPUT;`

En este ejemplo, ejecutamos el `Stored Procedure` "`NombreProcedimiento`" pasando los valores correspondientes para los parámetros "`@Parametro1`" y "`@Parametro2`". Si el `Stored Procedure` tiene parámetros de salida, se pueden utilizar variables para capturar los valores devueltos.

- **Modificación del Stored Procedure:**

Si deseas modificar un `Stored Procedure` existente, puedes utilizar la instrucción `ALTER PROCEDURE`. Esto te permite realizar cambios en la declaración o en el cuerpo del procedimiento. Por ejemplo:

```
ALTER PROCEDURE NombreProcedimiento
    @NuevoParametro tipo_dato
AS
BEGIN
    -- Cuerpo modificado del Stored Procedure
END;
```

En este ejemplo, modificamos el `Stored Procedure` "`NombreProcedimiento`" añadiendo un nuevo parámetro llamado "`@NuevoParametro`".

- **Eliminación del Stored Procedure:**

Si ya no necesitas un `Stored Procedure`, puedes eliminarlo utilizando la instrucción `DROP PROCEDURE`. Esto eliminará completamente el procedimiento almacenado de la base de datos. Por ejemplo:

`DROP PROCEDURE NombreProcedimiento;`

En resumen, un `Stored Procedure` en SQL Server es un conjunto de instrucciones SQL predefinidas y almacenadas en la base de datos como un objeto. Se compone de una declaración, un cuerpo y opciones adicionales. Los `Stored Procedures` se pueden ejecutar utilizando la instrucción `EXEC`, y se pueden modificar o eliminar según sea necesario. Son una herramienta poderosa para organizar y reutilizar lógica de negocio en una base de datos SQL Server.

[🔼](#índice)

---

## **90. ¿Qué es una variable? Uso de ISNULL para evaluar valores**

En SQL Server, una variable es un objeto que se utiliza para almacenar un valor temporalmente durante la ejecución de una consulta o un procedimiento almacenado. Las variables permiten almacenar datos y manipularlos dentro de una consulta, lo que brinda flexibilidad y control sobre los resultados obtenidos.

Una forma común de utilizar variables en SQL Server es con la función `ISNULL`, que se utiliza para evaluar si un valor es nulo y proporcionar un valor alternativo en caso de que lo sea. La función `ISNULL` es útil cuando se desea manejar valores nulos de forma adecuada y evitar errores o resultados inesperados.

Aquí tienes una explicación detallada de las variables y el uso de la función `ISNULL` en SQL Server, utilizando la base de datos Northwind:

1. **Declaración de una variable:**

Antes de utilizar una variable, debes declararla para indicar el tipo de datos que contendrá. Puedes declarar una variable utilizando la declaración `DECLARE`, seguida del nombre de la variable y su tipo de datos. Por ejemplo:

`DECLARE @NombreVariable tipo_dato;`

En este ejemplo, "`@NombreVariable`" es el nombre de la variable y "`tipo_dato`" es el tipo de datos que contendrá, como `VARCHAR`, `INT`, `DATE`, etc.

2. **Asignación de valores a una variable:**

Después de declarar una variable, puedes asignarle un valor utilizando la declaración `SET`. Por ejemplo:

`SET @NombreVariable = valor;`

En este ejemplo, "`@NombreVariable`" es el nombre de la variable y "`valor`" es el valor que deseas asignar.

3. **Uso de la función ISNULL:**

La función `ISNULL` se utiliza para evaluar si un valor es nulo y proporcionar un valor alternativo en caso de que lo sea. La sintaxis de la función `ISNULL` es la siguiente:

`ISNULL(expression, valor_alternativo)`

Donde "`expression`" es la expresión o columna que deseas evaluar y "`valor_alternativo`" es el valor que se utilizará si "`expression`" es nula.

Por ejemplo, supongamos que deseas obtener el nombre de un producto de la tabla "`Products`" en la base de datos Northwind, pero si el nombre del producto es nulo, deseas mostrar el mensaje "`Nombre no disponible`". Puedes utilizar la función `ISNULL` de la siguiente manera:

```
DECLARE @NombreProducto VARCHAR(50);

SELECT @NombreProducto = ISNULL(ProductName, 'Nombre no disponible')
FROM Products
WHERE ProductID = 1;

SELECT @NombreProducto;
```

En este ejemplo, declaramos la variable "`@NombreProducto`" como `VARCHAR(50)` y utilizamos la función `ISNULL` para asignar el valor del nombre del producto. Si el nombre del producto es nulo, se asignará el valor alternativo "`Nombre no disponible`".

4. **Uso de la variable en consultas:**

Una vez que has asignado un valor a una variable, puedes utilizarla en consultas posteriores. Por ejemplo, puedes utilizar la variable en una cláusula `WHERE` para filtrar los resultados de una consulta. Supongamos que deseas obtener todos los pedidos de un cliente específico utilizando la variable "`@CustomerID`":

```
DECLARE @CustomerID VARCHAR(10);
SET @CustomerID = 'ALFKI';

SELECT OrderID, OrderDate
FROM Orders
WHERE CustomerID = @CustomerID;
```

En este ejemplo, declaramos la variable "`@CustomerID`" como `VARCHAR(10)` y asignamos el valor '`ALFKI`'. Luego, utilizamos la variable en la cláusula `WHERE` para filtrar los pedidos del cliente correspondiente.

En resumen, una variable en SQL Server es un objeto utilizado para almacenar valores temporales durante la ejecución de consultas o procedimientos almacenados. Puedes declarar una variable, asignarle un valor y utilizarla en consultas posteriores. La función `ISNULL` es útil para evaluar valores nulos y proporcionar un valor alternativo. Utilizando variables y la función `ISNULL`, puedes manipular datos y controlar los resultados obtenidos en SQL Server.

Una variable en SQL Server es un objeto que se utiliza para almacenar y manipular valores temporales dentro de un contexto específico, como un `Stored Procedure`. Las variables te permiten asignar valores, realizar operaciones y utilizar esos valores en diversas partes de un `Stored Procedure`.

El uso de variables en combinación con el operador `ISNULL` es una técnica común en SQL Server para evaluar y manejar valores nulos. El operador `ISNULL` se utiliza para comprobar si un valor es nulo y proporcionar un valor alternativo en caso de que sea nulo.

Aquí tienes una explicación detallada de cómo utilizar variables y el operador `ISNULL` en un `Stored Procedure` en SQL Server, utilizando la base de datos Northwind:

1. **Declaración de variables:**

Puedes declarar variables en un `Stored Procedure` utilizando la declaración `DECLARE`, especificando el nombre de la variable y el tipo de datos. Por ejemplo:

```
DECLARE @NombreProducto nvarchar(50);
DECLARE @Cantidad int;
```

En este ejemplo, declaramos dos variables: "`@NombreProducto`" como una variable de tipo `nvarchar` con una longitud máxima de `50` caracteres, y "`@Cantidad`" como una variable de tipo `int`.

2. **Asignación de valores a variables:**

Después de declarar las variables, puedes asignarles valores utilizando la declaración `SET` o mediante una consulta. Por ejemplo:

```
SET @NombreProducto = 'Chai';
SET @Cantidad = 10;
```

En este ejemplo, asignamos el valor '`Chai`' a la variable "`@NombreProducto`" y el valor `10` a la variable "`@Cantidad`".

3. **Uso de variables en consultas y operaciones:**

Una vez que hayas asignado valores a las variables, puedes utilizarlas en consultas y operaciones dentro del `Stored Procedure`. Por ejemplo:

```
SELECT ProductID, UnitPrice
FROM Products
WHERE ProductName = @NombreProducto;
```

En este ejemplo, utilizamos la variable "`@NombreProducto`" en la cláusula `WHERE` de una consulta para seleccionar los registros de la tabla "`Products`" que coinciden con el valor de la variable.

4. **Uso del operador ISNULL:**

El operador `ISNULL` se utiliza para evaluar si un valor es nulo y proporcionar un valor alternativo en caso de que sea nulo. Puedes utilizar el operador `ISNULL` en combinación con las variables para manejar los valores nulos de manera efectiva. Por ejemplo:

```
SELECT ProductID, ISNULL(UnitsInStock, 0) AS UnitsInStock
FROM Products;
```

En este ejemplo, utilizamos el operador `ISNULL` para evaluar el valor de la columna "`UnitsInStock`" en la tabla "`Products`". Si el valor es nulo, se reemplaza por `0` utilizando la función `ISNULL`. Esto asegura que no obtengamos valores nulos en el resultado de la consulta.

En resumen, una variable en SQL Server es un objeto utilizado para almacenar y manipular valores temporales en el contexto de un `Stored Procedure`. Puedes declarar variables, asignarles valores y utilizarlas en consultas y operaciones dentro del `Stored Procedure`. El operador `ISNULL` es útil para evaluar y manejar valores nulos, permitiéndote proporcionar un valor alternativo en caso de que un valor sea nulo. Utilizando variables y el operador `ISNULL`, puedes manipular valores y controlar los resultados dentro de un `Stored Procedure` en SQL Server, en el contexto de la base de datos Northwind.

[🔼](#índice)

---

| **Inicio**            | **atrás 8**                | **Siguiente 10**            |
| --------------------- | -------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./8_Consultas_SQL.md) | [⏩](./10_Consultas_SQL.md) |
