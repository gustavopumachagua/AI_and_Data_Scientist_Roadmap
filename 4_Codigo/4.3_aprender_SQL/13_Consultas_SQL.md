| **Inicio**            | **atrás 12**                | **Siguiente 14**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./12_Consultas_SQL.md) | [⏩](./14_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------ |
| [121. Función DATEPART](#121-función-datepart)                                                                           |
| [122. Función ISDATE](#122-función-isdate)                                                                               |
| [123. Funciones CAST y CONVERT](#123-funciones-cast-y-convert)                                                           |
| [124. Las transacciones](#124-las-transacciones)                                                                         |
| [125. La instrucción BEGIN TRAN](#125-la-instrucción-begin-tran)                                                         |
| [126. Introducción JOIN y UNIONS entre tablas](#126-introducción-join-y-unions-entre-tablas)                             |
| [127. La cláusula INNER JOIN](#127-la-cláusula-inner-join)                                                               |
| [128. Consideraciones a tener en cuenta con el uso de INNER](#128-consideraciones-a-tener-en-cuenta-con-el-uso-de-inner) |
| [129. La cláusula UNION y UNION ALL](#129-la-cláusula-union-y-union-all)                                                 |
| [130. Funciones definidas por el usuario](#130-funciones-definidas-por-el-usuario)                                       |

---

# **Tutorial de SQL**

## **121. Función DATEPART**

La función `DATEPART` en SQL Server se utiliza para extraer una parte específica de una fecha o hora. Esta función es útil cuando se necesita obtener componentes individuales, como el año, mes, día, hora, minuto, etc., de una fecha o hora completa.

Aquí tienes una explicación detallada de la función `DATEPART`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `DATEPART` es la siguiente:

`DATEPART(intervalo, fecha)`

- **intervalo:** es la parte de la fecha que se desea extraer. Puede ser uno de los siguientes valores: year, quarter, month, day, week, hour, minute, second, millisecond, microsecond o nanosecond.
- **fecha:** es la fecha o hora de la cual se desea extraer la parte especificada.

Ejemplo:

```
USE Northwind;
GO

SELECT DATEPART(year, OrderDate) AS Anio,
       DATEPART(month, OrderDate) AS Mes,
       DATEPART(day, OrderDate) AS Dia
FROM Orders;
```

En este ejemplo, se utiliza la función `DATEPART` para extraer las partes individuales (año, mes, día) de la columna "`OrderDate`" en la tabla "`Orders`". Esto generará tres columnas: "`Anio`" que contiene el año de la fecha, "`Mes`" que contiene el número del mes y "`Dia`" que contiene el número del día correspondiente a cada registro.

La función `DATEPART` permite extraer información específica de una fecha o hora. Puedes utilizar diferentes intervalos para obtener diferentes partes, como el año, mes, día, hora, minuto, etc. Esto es útil cuando se necesita realizar cálculos o filtrar registros basados en partes específicas de una fecha o hora.

Es importante tener en cuenta que el valor devuelto por la función `DATEPART` será un número entero que representa la parte solicitada. Por ejemplo, para el intervalo "`month`", se devolverá un número entero del 1 al 12 que representa el mes correspondiente.

Recuerda que la función `DATEPART` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **122. Función ISDATE**

La función `ISDATE` en SQL Server se utiliza para verificar si una expresión es una fecha válida. Retorna 1 si la expresión es una fecha válida y 0 si no lo es. Esta función es útil cuando se necesita validar si un valor es una fecha antes de realizar operaciones o comparaciones relacionadas con fechas.

Aquí tienes una explicación detallada de la función `ISDATE`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `ISDATE` es la siguiente:

`ISDATE(expresion)`

- **expresion:** es la expresión que se desea evaluar para determinar si es una fecha válida o no.

Ejemplo:

```
USE Northwind;
GO

SELECT OrderID, OrderDate, ISDATE(OrderDate) AS EsFechaValida
FROM Orders;
```

En este ejemplo, se utiliza la función `ISDATE` para determinar si la columna "`OrderDate`" en la tabla "`Orders`" contiene valores de fecha válidos. La función retorna 1 si la expresión es una fecha válida y 0 si no lo es. El resultado se muestra en una columna llamada "`EsFechaValida`".

Es importante tener en cuenta que la función `ISDATE` tiene en cuenta diversos formatos de fecha reconocidos por SQL Server para determinar si una expresión es una fecha válida. Sin embargo, es posible que la función no pueda reconocer formatos de fecha personalizados o interpretar correctamente fechas en formatos ambiguos.

La función `ISDATE` es útil para validar datos de fecha antes de realizar operaciones o comparaciones relacionadas con fechas. Puede utilizarse en consultas para filtrar registros basados en la validez de las fechas, evitando así errores de tiempo de ejecución al realizar cálculos con datos no válidos.

Recuerda que la función `ISDATE` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **123. Funciones CAST y CONVERT**

Las funciones `CAST` y `CONVERT` en SQL Server se utilizan para convertir un tipo de datos a otro. Estas funciones son útiles cuando se necesita cambiar el tipo de datos de una columna o expresión en una consulta.

Aquí tienes una explicación detallada de las funciones `CAST` y `CONVERT`, junto con un ejemplo utilizando la base de datos Northwind:

La función `CAST` se utiliza para realizar conversiones de tipo de datos explícitas en SQL Server. La sintaxis de la función `CAST` es la siguiente:

`CAST(expresion AS tipo_de_dato)`

- expresion es la expresión o columna que se desea convertir.
- tipo_de_dato es el tipo de datos al que se desea convertir la expresión.

Ejemplo:

```
USE Northwind;
GO

SELECT OrderID, CAST(Quantity AS varchar(10)) AS CantidadTexto
FROM [Order Details];
```

En este ejemplo, se utiliza la función `CAST` para convertir la columna "`Quantity`" de la tabla "`Order Details`" en una cadena de texto (`varchar`). Esto genera una nueva columna llamada "`CantidadTexto`" que contiene la cantidad convertida como una cadena de texto.

La función `CONVERT` también se utiliza para realizar conversiones de tipo de datos en SQL Server. La diferencia principal entre `CAST` y `CONVERT` es que `CONVERT` permite especificar un estilo de formato adicional para ciertos tipos de datos, como fechas y horas. La sintaxis de la función `CONVERT` es la siguiente:

`CONVERT(tipo_de_dato, expresion, estilo)`

- tipo_de_dato es el tipo de datos al que se desea convertir la expresión.
- expresion es la expresión o columna que se desea convertir.
- estilo (opcional) es un valor numérico que representa el estilo de formato para las conversiones de fecha y hora.

Ejemplo:

```
USE Northwind;
GO

SELECT OrderID, CONVERT(varchar(10), OrderDate, 103) AS FechaTexto
FROM Orders;
```

En este ejemplo, se utiliza la función `CONVERT` para convertir la columna "`OrderDate`" de la tabla "`Orders`" en una cadena de texto (varchar) con un estilo de formato específico (103). Esto genera una nueva columna llamada "`FechaTexto`" que contiene la fecha convertida como una cadena de texto en formato `DD/MM/AAAA`.

Tanto `CAST` como `CONVERT` son útiles para cambiar el tipo de datos de una columna o expresión en una consulta. Estas funciones permiten manipular y presentar los datos de una manera más adecuada para las necesidades de la aplicación o el informe.

Recuerda que las funciones `CAST` y `CONVERT` están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **124. Las transacciones**

Las transacciones en SQL Server son una unidad lógica de trabajo que agrupa una o más operaciones de base de datos en una secuencia coherente. Una transacción asegura que todas las operaciones se completen correctamente o se deshagan en caso de que ocurra algún error, garantizando así la integridad y consistencia de los datos.

Aquí tienes una explicación detallada de las transacciones en SQL Server, junto con un ejemplo utilizando la base de datos Northwind:

1. Las transacciones se componen de tres partes esenciales: inicio, operaciones y finalización. La secuencia típica de una transacción es la siguiente:

2. Inicio de la transacción (`BEGIN TRANSACTION`): Se inicia una transacción para agrupar las operaciones que se ejecutarán dentro de ella. Esto marca el punto de inicio de la transacción.

3. Operaciones de la transacción: Se realizan una o más operaciones de base de datos dentro de la transacción. Estas operaciones pueden incluir inserciones, actualizaciones o eliminaciones de datos.

4. Confirmación de los cambios (`COMMIT`): Si todas las operaciones de la transacción se han completado correctamente, se confirman los cambios realizados en la base de datos y se hace permanente. Esto marca el punto de finalización de la transacción.

5. Deshacer cambios (`ROLLBACK`): Si ocurre algún error durante la ejecución de las operaciones de la transacción, se realiza un rollback para deshacer todos los cambios realizados hasta el punto de inicio de la transacción. Esto asegura que no se realicen cambios parciales o incorrectos en la base de datos.

Es importante destacar que las transacciones en SQL Server se utilizan en conjunción con el control de concurrencia para garantizar la consistencia de los datos. Durante una transacción, se bloquean los recursos involucrados para evitar que otros usuarios realicen modificaciones simultáneas hasta que la transacción se complete o se deshaga.

Ejemplo:

```
USE Northwind;
GO

BEGIN TRANSACTION;

UPDATE Customers
SET ContactName = 'John Doe'
WHERE CustomerID = 'ALFKI';

INSERT INTO Orders (CustomerID, OrderDate)
VALUES ('ALFKI', GETDATE());

COMMIT;
```

En este ejemplo, se inicia una transacción utilizando la sentencia `BEGIN TRANSACTION`. Luego se realizan dos operaciones: se actualiza el nombre de contacto de un cliente en la tabla "`Customers`" y se inserta un nuevo pedido en la tabla "`Orders`". Finalmente, se confirman los cambios realizados en la transacción utilizando la sentencia `COMMIT`.

Si hubiera ocurrido algún error durante la ejecución de las operaciones, se podría haber realizado un `rollback` para deshacer los cambios utilizando la sentencia `ROLLBACK`.

Las transacciones son útiles cuando se necesita asegurar la atomicidad y la integridad de un conjunto de operaciones relacionadas. Al agrupar las operaciones en una transacción, se garantiza que todas se completen o se deshagan de manera coherente, evitando cambios parciales o inconsistentes en la base de datos.

Recuerda que las transacciones están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las sintaxis y características específicas pueden variar entre los diferentes sistemas.

[🔼](#índice)

---

## **125. La instrucción BEGIN TRAN**

La instrucción "`BEGIN TRAN`" en SQL Server se utiliza para iniciar una transacción. Marca el inicio de una secuencia de operaciones que deben ejecutarse como una unidad lógica de trabajo dentro de una transacción.

Aquí tienes una explicación detallada de la instrucción "`BEGIN TRAN`", junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis básica de la instrucción "`BEGIN TRAN`" es la siguiente:

`BEGIN TRAN [NombreTransaccion]`

- "`NombreTransaccion`" es un identificador opcional que se puede proporcionar para dar un nombre específico a la transacción. Este nombre puede ser útil para identificar y gestionar transacciones en situaciones más complejas.

Ejemplo:

```
USE Northwind;
GO

BEGIN TRAN MiTransaccion;

UPDATE Customers
SET ContactName = 'John Doe'
WHERE CustomerID = 'ALFKI';

INSERT INTO Orders (CustomerID, OrderDate)
VALUES ('ALFKI', GETDATE());
```

En este ejemplo, se utiliza la instrucción "`BEGIN TRAN`" para iniciar una transacción llamada "`MiTransaccion`". Luego se realizan dos operaciones dentro de la transacción: se actualiza el nombre de contacto de un cliente en la tabla "`Customers`" y se inserta un nuevo pedido en la tabla "`Orders`".

Al utilizar "`BEGIN TRAN`", se asegura que todas las operaciones realizadas después de esta instrucción formen parte de la misma transacción. Esto significa que todas las operaciones deben completarse con éxito o deshacerse en caso de error o necesidad de deshacer los cambios.

Es importante tener en cuenta que, para finalizar una transacción, se debe utilizar la instrucción "`COMMIT`" para confirmar los cambios o la instrucción "`ROLLBACK`" para deshacerlos. Sin una de estas instrucciones, la transacción quedará abierta y los cambios no se harán permanentes.

La instrucción "`BEGIN TRAN`" es una parte fundamental del control de transacciones en SQL Server. Permite agrupar operaciones relacionadas en una unidad coherente y controlar su ejecución y resultado como una sola entidad.

Recuerda que las transacciones están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las sintaxis y características específicas pueden variar entre los diferentes sistemas.

[🔼](#índice)

---

## **126. Introducción JOIN y UNIONS entre tablas**

Los `JOIN` y `UNIONS` son operaciones utilizadas en SQL Server para combinar datos de múltiples tablas. Aunque tienen propósitos diferentes, ambos son fundamentales para realizar consultas complejas y obtener conjuntos de resultados más completos.

Aquí tienes una explicación detallada de los `JOIN` y `UNIONS`, junto con ejemplos utilizando la base de datos Northwind:

1. **JOIN:**

Los `JOIN` se utilizan para combinar registros relacionados de dos o más tablas en función de una condición de unión. Hay diferentes tipos de `JOIN` disponibles en SQL Server, que incluyen `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN` y `FULL JOIN`. Estos tipos de `JOIN` determinan cómo se combinan los registros y qué registros se incluyen en el resultado final.

- Ejemplo de `INNER JOIN`:

```
USE Northwind;
GO

SELECT Orders.OrderID, Customers.ContactName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

En este ejemplo, se realiza un `INNER JOIN` entre las tablas "`Orders`" y "`Customers`" utilizando la columna "`CustomerID`" como condición de unión. El resultado muestra el `OrderID` y el `ContactName` de los registros que tienen una coincidencia en ambas tablas.

2. **UNION:**

Los `UNION` se utilizan para combinar el resultado de dos o más consultas en un solo conjunto de resultados. Las consultas deben tener la misma estructura de columna para poder realizar un `UNION`. Las duplicaciones de registros se eliminan automáticamente a menos que se utilice `UNION ALL`, que conserva todas las filas, incluso las duplicadas.

- Ejemplo de `UNION`:

```
USE Northwind;
GO

SELECT CustomerID, ContactName
FROM Customers
WHERE Country = 'Germany'

UNION

SELECT CustomerID, ContactName
FROM Customers
WHERE Country = 'France';
```

En este ejemplo, se realizan dos consultas para obtener los clientes de Alemania y Francia respectivamente. Las dos consultas tienen la misma estructura de columna, por lo que se utiliza `UNION` para combinar los resultados en un único conjunto de resultados.

Es importante destacar que el número y el orden de las columnas deben ser los mismos en todas las consultas que se utilizan en el `UNION`.

Tanto los `JOIN` como los `UNIONS` son herramientas poderosas para combinar y relacionar datos de diferentes tablas en SQL Server. Los `JOIN` permiten obtener resultados basados en condiciones de unión específicas, mientras que los `UNIONS` permiten combinar el resultado de consultas similares. Ambos se utilizan ampliamente para realizar consultas complejas y obtener conjuntos de resultados más completos y relevantes.

Recuerda que los `JOIN` y `UNIONS` son operaciones estándar en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, es posible que algunas sintaxis y características específicas varíen entre los diferentes sistemas.

[🔼](#índice)

---

## **127. La cláusula INNER JOIN**

La cláusula `INNER JOIN` en SQL Server se utiliza para combinar registros de dos o más tablas en función de una condición de unión. Se seleccionan solo los registros que tienen una coincidencia en ambas tablas involucradas en la operación `JOIN`.

Aquí tienes una explicación detallada de la cláusula `INNER JOIN`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis básica de la cláusula `INNER JOIN` es la siguiente:

```
SELECT columnas
FROM tabla1
INNER JOIN tabla2
   ON tabla1.columna = tabla2.columna;
```

- "`columnas`" representa las columnas específicas que deseas seleccionar de las tablas involucradas en el `JOIN`.
- "`tabla1`" y "`tabla2`" son las tablas que deseas combinar mediante el `JOIN`.
- "`columna`" es la columna común utilizada para realizar la unión entre las tablas.

Ejemplo:

```
USE Northwind;
GO

SELECT Orders.OrderID, Customers.ContactName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

En este ejemplo, se realiza un `INNER JOIN` entre las tablas "`Orders`" y "`Customers`" utilizando la columna "`CustomerID`" como condición de unión. La cláusula `ON` establece la relación entre las tablas, especificando que los registros deben tener el mismo valor en la columna "`CustomerID`" para ser incluidos en el resultado.

El resultado de esta consulta mostrará el `OrderID` y el `ContactName` de los registros que tienen una coincidencia en ambas tablas. Solo se seleccionarán los registros que cumplan con la condición de unión establecida en el `INNER JOIN`.

La cláusula `INNER JOIN` es útil cuando se necesita combinar registros de dos o más tablas basándose en una relación definida. Esto permite obtener información relacionada de diferentes tablas en una sola consulta. Es una forma efectiva de aprovechar las relaciones definidas en la estructura de la base de datos para obtener resultados más completos y relevantes.

Recuerda que la cláusula `INNER JOIN` es una funcionalidad estándar en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las sintaxis y características específicas pueden variar entre los diferentes sistemas.

[🔼](#índice)

---

## **128. Consideraciones a tener en cuenta con el uso de INNER**

Al utilizar la cláusula `INNER JOIN` en SQL Server, es importante tener en cuenta algunas consideraciones para garantizar resultados correctos y eficientes. Aquí tienes una explicación detallada de las consideraciones al usar `INNER JOIN`, junto con un ejemplo utilizando la base de datos Northwind:

1. **Coincidencia de claves:**

La condición de unión en el `INNER JOIN` debe basarse en columnas que contengan claves relacionadas entre las tablas. Asegúrate de que las columnas utilizadas para la unión sean del mismo tipo de datos y tengan valores coincidentes en ambas tablas. De lo contrario, los resultados pueden ser inexactos o incompletos.

Ejemplo:

```
USE Northwind;
GO

SELECT Orders.OrderID, Customers.ContactName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

En este ejemplo, la condición de unión se basa en la columna "`CustomerID`" en las tablas "`Orders`" y "`Customers`". Ambas columnas deben ser del mismo tipo de datos y contener valores coincidentes para obtener resultados precisos.

2. **Tablas relacionadas correctamente:**

Asegúrate de que las tablas involucradas en el `INNER JOIN` estén relacionadas correctamente en la base de datos. Esto se logra mediante la definición adecuada de las claves primarias y foráneas en las tablas relacionadas. Verifica las relaciones establecidas entre las tablas para asegurarte de que el `INNER JOIN` se realiza en las tablas correctas.

3. **Optimización de consultas:**

Al utilizar `INNER JOIN` en consultas con grandes volúmenes de datos, es importante optimizar las consultas para un rendimiento óptimo. Utiliza índices adecuados en las columnas utilizadas para la unión y asegúrate de que las estadísticas de la base de datos estén actualizadas. Esto ayudará al motor de SQL Server a generar planes de ejecución eficientes y acelerar el tiempo de respuesta de la consulta.

4. **Alias de tabla:**

Considera el uso de alias de tabla para mejorar la legibilidad y la claridad de las consultas. Los alias de tabla proporcionan nombres más cortos y descriptivos para las tablas, lo que facilita la comprensión de la estructura de la consulta.

Ejemplo:

```
USE Northwind;
GO

SELECT O.OrderID, C.ContactName
FROM Orders AS O
INNER JOIN Customers AS C ON O.CustomerID = C.CustomerID;
```

En este ejemplo, se utilizan alias de tabla "`O`" y "`C`" para las tablas "`Orders`" y "`Customers`", respectivamente. Esto hace que la consulta sea más legible y comprensible.

Al considerar estas recomendaciones al usar `INNER JOIN` en SQL Server, puedes asegurarte de obtener resultados precisos y eficientes en tus consultas. Recuerda que las consideraciones pueden variar según la estructura y las necesidades específicas de tu base de datos, por lo que es importante analizar y ajustar en consecuencia.

[🔼](#índice)

---

## **129. La cláusula UNION y UNION ALL**

La cláusula `UNION` y `UNION ALL` en SQL Server se utilizan para combinar el resultado de dos o más consultas en un solo conjunto de resultados. Sin embargo, hay una diferencia importante entre ambas cláusulas.

La cláusula `UNION` combina los resultados de las consultas eliminando cualquier duplicado, es decir, solo muestra los valores únicos en el conjunto de resultados final. Por otro lado, la cláusula `UNION ALL` combina los resultados de las consultas sin eliminar duplicados, es decir, muestra todos los valores, incluidos los duplicados, en el conjunto de resultados final.

Aquí tienes una explicación detallada de ambas cláusulas, junto con un ejemplo utilizando la base de datos Northwind:

1. **Cláusula UNION:**

La cláusula `UNION` se utiliza para combinar el resultado de dos o más consultas y mostrar solo los valores únicos en el conjunto de resultados final. Para que funcione correctamente, las consultas involucradas deben tener la misma estructura de columnas.

Sintaxis básica:

```
SELECT columnas
FROM tabla1
UNION
SELECT columnas
FROM tabla2;
```

Ejemplo:

```
USE Northwind;
GO

SELECT CustomerID
FROM Customers
WHERE Country = 'USA'
UNION
SELECT CustomerID
FROM Customers
WHERE City = 'London';
```

En este ejemplo, se combinan los `CustomerID` de los clientes en Estados Unidos y en Londres utilizando la cláusula `UNION`. El resultado mostrará solo los `CustomerID` únicos que cumplan con las condiciones de ambas consultas.

2. **Cláusula UNION ALL:**

La cláusula `UNION ALL` se utiliza para combinar el resultado de dos o más consultas y mostrar todos los valores, incluidos los duplicados, en el conjunto de resultados final.

Sintaxis básica:

```
SELECT columnas
FROM tabla1
UNION ALL
SELECT columnas
FROM tabla2;
```

Ejemplo:

```
USE Northwind;
GO

SELECT CustomerID
FROM Customers
WHERE Country = 'USA'
UNION ALL
SELECT CustomerID
FROM Customers
WHERE City = 'London';
```

En este ejemplo, se combinan los `CustomerID` de los clientes en Estados Unidos y en Londres utilizando la cláusula `UNION ALL`. El resultado mostrará todos los `CustomerID`, incluidos los duplicados, que cumplan con las condiciones de ambas consultas.

Es importante tener en cuenta que la cláusula `UNION` y `UNION ALL` requieren que las consultas involucradas tengan la misma estructura de columnas en el mismo orden. Si las consultas no cumplen con esta condición, se generará un error. Además, es importante considerar el rendimiento y el uso de memoria al elegir entre `UNION` y `UNION ALL`, ya que `UNION` puede implicar una operación de eliminación de duplicados que puede tener un impacto en el rendimiento.

En resumen, la cláusula `UNION` y `UNION ALL` en SQL Server son utilizadas para combinar el resultado de múltiples consultas en un solo conjunto de resultados. La cláusula `UNION` elimina los duplicados, mientras que la cláusula `UNION ALL` muestra todos los valores, incluidos los duplicados. El uso de una u otra depende de los requisitos específicos de la consulta y del resultado deseado.

![sql join](../../img/sql%20joins.jpg "sql join")

[🔼](#índice)

---

## **130. Funciones definidas por el usuario**

Las funciones definidas por el usuario en SQL Server son funciones personalizadas que puedes crear para realizar operaciones específicas y complejas en los datos de la base de datos. Estas funciones se pueden utilizar en consultas SQL de la misma manera que las funciones incorporadas en SQL Server.

Aquí tienes una explicación detallada de las funciones definidas por el usuario, junto con un ejemplo utilizando la base de datos Northwind:

Tipos de funciones definidas por el usuario:

1. En SQL Server, puedes crear tres tipos de funciones definidas por el usuario:

- **Funciones escalares:** Devuelven un solo valor basado en los parámetros de entrada.
- **Funciones en línea:** Devuelven una tabla en línea que puede ser utilizada en la cláusula `FROM` de una consulta.
- **Funciones de tabla:** Devuelven una tabla completa que puede ser tratada como una tabla independiente en una consulta.

2. Creación de funciones definidas por el usuario:

Para crear una función definida por el usuario, debes seguir los siguientes pasos:

- Especifica el nombre de la función y los parámetros de entrada (si los hay).
- Define el tipo de retorno de la función.
- Implementa la lógica de la función utilizando sentencias SQL.
- Opcionalmente, agrega declaraciones variables, condiciones `IF`, bucles `WHILE`, etc.

3. Ejemplo de función definida por el usuario:

Supongamos que queremos crear una función que devuelva el número de productos en una categoría específica. Utilizaremos la base de datos Northwind, donde tenemos la tabla "`Products`" y la tabla "`Categories`".

Ejemplo de función definida por el usuario:

```
USE Northwind;
GO

CREATE FUNCTION dbo.GetProductCountByCategory(@categoryName NVARCHAR(50))
RETURNS INT
AS
BEGIN
    DECLARE @productCount INT;
    SET @productCount = (
        SELECT COUNT(*)
        FROM Products P
        INNER JOIN Categories C ON P.CategoryID = C.CategoryID
        WHERE C.CategoryName = @categoryName
    );
    RETURN @productCount;
END;
```

En este ejemplo, creamos una función llamada "`GetProductCountByCategory`" que acepta un parámetro de entrada "`categoryName`". La función utiliza una consulta SQL para contar el número de productos en la categoría especificada. Luego, se retorna el resultado utilizando la instrucción "`RETURN`".

4. Uso de funciones definidas por el usuario:

Una vez que has creado una función definida por el usuario, puedes utilizarla en consultas SQL de la misma manera que las funciones incorporadas. Por ejemplo:

`SELECT dbo.GetProductCountByCategory('Beverages') AS BeverageProductCount;`

Esta consulta utiliza la función definida por el usuario para obtener el recuento de productos en la categoría '`Beverages`'. El resultado se mostrará en una columna llamada "`BeverageProductCount`".

Las funciones definidas por el usuario son una forma poderosa de encapsular lógica personalizada y reutilizable en SQL Server. Puedes crear funciones para realizar cálculos complejos, manipular datos y realizar transformaciones específicas. Esto ayuda a simplificar las consultas y mejorar la modularidad y mantenibilidad del código SQL.

**Funciones de tipo Escalares**

Las funciones de tipo escalar en SQL Server son funciones definidas por el usuario que devuelven un solo valor basado en los parámetros de entrada. Estas funciones se utilizan para realizar cálculos o manipulaciones de datos específicas y se pueden utilizar en cualquier lugar donde se espera un valor en una consulta SQL.

Aquí tienes una explicación detallada de las funciones de tipo escalar, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de funciones escalares:

Para crear una función escalar, debes seguir los siguientes pasos:

- Especifica el nombre de la función y los parámetros de entrada (si los hay).
- Define el tipo de retorno de la función.
- Implementa la lógica de la función utilizando sentencias SQL.
- Opcionalmente, agrega declaraciones variables, condiciones `IF`, bucles `WHILE`, etc.

2. Ejemplo de función escalar:

Supongamos que queremos crear una función que calcule el precio total de un pedido en función de la cantidad y el precio unitario. Utilizaremos la base de datos Northwind, donde tenemos la tabla "`OrderDetails`" que contiene información sobre los productos en cada pedido.

Ejemplo de función escalar:

```
USE Northwind;
GO

CREATE FUNCTION dbo.CalculateOrderTotal(@quantity INT, @unitPrice MONEY)
RETURNS MONEY
AS
BEGIN
    DECLARE @totalPrice MONEY;
    SET @totalPrice = @quantity * @unitPrice;
    RETURN @totalPrice;
END;
```

En este ejemplo, creamos una función llamada "`CalculateOrderTotal`" que acepta dos parámetros de entrada: `@quantity` (cantidad) y `@unitPrice` (precio unitario). La función realiza un cálculo simple multiplicando la cantidad por el precio unitario y retorna el resultado como un valor de tipo `MONEY`.

3. Uso de funciones escalares:

Una vez que has creado una función escalar, puedes utilizarla en consultas SQL de la misma manera que las funciones incorporadas. Por ejemplo:

```
SELECT OrderID, ProductID, Quantity, UnitPrice, dbo.CalculateOrderTotal(Quantity, UnitPrice) AS OrderTotal
FROM OrderDetails;
```

Esta consulta utiliza la función escalar "`CalculateOrderTotal`" para calcular el precio total de cada pedido en la tabla "`OrderDetails`". El resultado se muestra en una columna llamada "`OrderTotal`".

Las funciones escalares en SQL Server son útiles cuando necesitas realizar cálculos simples o manipulaciones de datos en una consulta y deseas encapsular esa lógica en una función reutilizable. Puedes usar funciones escalares para realizar operaciones matemáticas, concatenación de cadenas, conversión de tipos de datos, manipulación de fechas, entre otras tareas. Al utilizar funciones escalares, puedes simplificar y modularizar tus consultas SQL, mejorando la legibilidad y el mantenimiento del código.

**Funciones de tipo Tabla**

Las funciones de tipo tabla en SQL Server son funciones definidas por el usuario que devuelven un conjunto de resultados en forma de tabla. Estas funciones se utilizan para realizar consultas más complejas y devolver un conjunto de registros que se pueden utilizar en otras partes de una consulta SQL, como la cláusula `FROM`.

Aquí tienes una explicación detallada de las funciones de tipo tabla, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de funciones de tipo tabla:

Para crear una función de tipo tabla, debes seguir los siguientes pasos:

- Especifica el nombre de la función y los parámetros de entrada (si los hay).
- Define la estructura de la tabla que será devuelta por la función.
- Implementa la lógica de la función utilizando sentencias SQL.
- Rellena la tabla de resultados utilizando instrucciones `INSERT`, `SELECT`, o cualquier otra operación necesaria.

2. Ejemplo de función de tipo tabla:

Supongamos que queremos crear una función que devuelva los productos de una categoría específica. Utilizaremos la base de datos Northwind, donde tenemos la tabla "`Products`" y la tabla "`Categories`".

Ejemplo de función de tipo tabla:

```
USE Northwind;
GO

CREATE FUNCTION dbo.GetProductsByCategory(@categoryName NVARCHAR(50))
RETURNS TABLE
AS
RETURN
(
    SELECT P.ProductID, P.ProductName, P.UnitPrice
    FROM Products P
    INNER JOIN Categories C ON P.CategoryID = C.CategoryID
    WHERE C.CategoryName = @categoryName
);
```

En este ejemplo, creamos una función llamada "`GetProductsByCategory`" que acepta un parámetro de entrada "`categoryName`". La función devuelve una tabla con tres columnas: `ProductID`, `ProductName` y `UnitPrice`. La función realiza una consulta SQL para seleccionar los productos de la categoría especificada utilizando una cláusula `INNER JOIN` con la tabla "`Categories`".

3. Uso de funciones de tipo tabla:

Una vez que has creado una función de tipo tabla, puedes utilizarla en consultas SQL de la misma manera que una tabla real. Por ejemplo:

```
SELECT *
FROM dbo.GetProductsByCategory('Beverages');
```

Esta consulta utiliza la función de tipo tabla "`GetProductsByCategory`" para obtener los productos de la categoría '`Beverages`'. Los resultados se mostrarán como si fueran el resultado de una consulta normal, con las columnas `ProductID`, `ProductName` y `UnitPrice`.

Las funciones de tipo tabla en SQL Server son útiles cuando necesitas encapsular una consulta compleja y devolver un conjunto de resultados que se pueden utilizar en otras partes de una consulta. Puedes utilizar funciones de tipo tabla para realizar consultas avanzadas, filtrar datos, realizar cálculos o cualquier otra operación necesaria para obtener los resultados deseados. Al utilizar funciones de tipo tabla, puedes modularizar y reutilizar lógica de consulta compleja, mejorando la legibilidad y el rendimiento de tus consultas SQL.

[🔼](#índice)

---

| **Inicio**            | **atrás 12**                | **Siguiente 14**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./12_Consultas_SQL.md) | [⏩](./14_Consultas_SQL.md) |
