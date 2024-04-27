| **Inicio**            | **atrás 10**                | **Siguiente 12**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./10_Consultas_SQL.md) | [⏩](./12_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [101. Operadores Aritméticos de suma, resta, división, multiplicación, módulo](#101-operadores-aritméticos-de-suma-resta-división-multiplicación-módulo) |
| [102. Operadores mayor o igual, menor o igual, distinto](#102-operadores-mayor-o-igual-menor-o-igual-distinto)                                           |
| [103. Proceso SP_HELP](#103-proceso-sp_help)                                                                                                             |
| [104. Proceso SP_HELPTEXT](#104-proceso-sp_helptext)                                                                                                     |
| [105. Agregando Shortcuts en la consola (sp_help, sp_helptext)](#105-agregando-shortcuts-en-la-consola-sp_help-sp_helptext)                              |
| [106. Las sentencias SQL](#106-las-sentencias-sql)                                                                                                       |
| [107. La Sentencia CREATE (Table, Type, Function)](#107-la-sentencia-create-table-type-function)                                                         |
| [108. La Sentencia ALTER](#108-la-sentencia-alter)                                                                                                       |
| [109. La Sentencia DROP](#109-la-sentencia-drop)                                                                                                         |
| [110. La Sentencia TRUNCATE](#110-la-sentencia-truncate)                                                                                                 |

---

# **Tutorial de SQL**

## **101. Operadores Aritméticos de suma, resta, división, multiplicación, módulo**

En SQL Server, los operadores aritméticos se utilizan para realizar operaciones matemáticas en los datos almacenados en la base de datos. Los operadores aritméticos más comunes son la suma (`+`), la resta (`-`), la multiplicación (`*`), la división (`/`) y el módulo (`%`).

Aquí tienes una explicación detallada de cada operador aritmético con ejemplos utilizando la base de datos Northwind:

1. **Operador de suma (+):**

El operador de suma se utiliza para sumar dos valores. Puede usarse tanto con valores numéricos como con cadenas de caracteres (concatenación). Si los operandos son de tipo numérico, se realizará una suma aritmética; si son cadenas de caracteres, se concatenarán.
Ejemplo:

```
USE Northwind;
GO

-- Suma aritmética
SELECT OrderID, Quantity, UnitPrice, Quantity * UnitPrice AS Total
FROM [Order Details]
WHERE OrderID = 10248;

-- Concatenación de cadenas
SELECT CustomerID, CompanyName, ContactName, ContactTitle,
       ContactName + ' (' + ContactTitle + ')' AS FullName
FROM Customers
WHERE Country = 'USA';
```

En el primer ejemplo, utilizamos el operador de suma para calcular el total de una línea de pedido multiplicando la cantidad y el precio unitario.

En el segundo ejemplo, utilizamos el operador de suma para concatenar cadenas de caracteres y crear un campo "`FullName`" que combina el nombre de contacto y el título de contacto de los clientes.

2. **Operador de resta (-):**

El operador de resta se utiliza para restar un valor de otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT OrderID, Quantity, UnitPrice, Quantity * UnitPrice AS Total,
       Quantity - 10 AS QuantityAfterDiscount
FROM [Order Details]
WHERE OrderID = 10248;
```

En este ejemplo, utilizamos el operador de resta para calcular la cantidad restante después de aplicar un descuento de `10` a la cantidad original en una línea de pedido.

3. **Operador de multiplicación (\*):**

El operador de multiplicación se utiliza para multiplicar dos valores.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductID, UnitPrice, Quantity, UnitPrice * Quantity AS TotalPrice
FROM [Order Details]
WHERE OrderID = 10248;
```

En este ejemplo, utilizamos el operador de multiplicación para calcular el precio total multiplicando el precio unitario por la cantidad en una línea de pedido.

4. **Operador de división (/):**

El operador de división se utiliza para dividir un valor por otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductID, UnitPrice, Quantity, UnitPrice / Quantity AS PricePerUnit
FROM [Order Details]
WHERE OrderID = 10248;
```

En este ejemplo, utilizamos el operador de división para calcular el precio por unidad dividiendo el precio unitario por la cantidad en una línea de pedido.

5. **Operador de módulo (%):**

El operador de módulo se utiliza para obtener el resto de una división entera.
Ejemplo:

```
USE Northwind;
GO

SELECT OrderID, Quantity, Quantity % 5 AS RemainingQuantity
FROM [Order Details]
WHERE OrderID = 10248;
```

En este ejemplo, utilizamos el operador de módulo para calcular la cantidad restante después de dividir la cantidad en una línea de pedido por `5`.

Los operadores aritméticos en SQL Server son fundamentales para realizar cálculos matemáticos en consultas y generar resultados personalizados. Pueden aplicarse a columnas individuales o combinarse con otras funciones y operadores para obtener resultados más complejos.

[🔼](#índice)

---

## **102. Operadores mayor o igual, menor o igual, distinto**

En SQL Server, existen operadores de comparación que permiten evaluar condiciones de igualdad, desigualdad, mayor que, menor que, mayor o igual que, y menor o igual que. Estos operadores se utilizan para realizar comparaciones entre dos valores y devolver un resultado booleano (verdadero o falso) según se cumpla o no la condición especificada.

Aquí tienes una explicación detallada de los operadores de comparación con ejemplos utilizando la base de datos Northwind:

1. **Operador mayor que (>):**

El operador mayor que se utiliza para evaluar si un valor es mayor que otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice > 50;
```

En este ejemplo, utilizamos el operador mayor que para seleccionar los productos cuyo precio unitario es mayor que `50`. Devolverá los productos con un precio unitario superior a `50`.

2. **Operador menor que (<):**

El operador menor que se utiliza para evaluar si un valor es menor que otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice < 20;
```

En este ejemplo, utilizamos el operador menor que para seleccionar los productos cuyo precio unitario es menor que `20`. Devolverá los productos con un precio unitario inferior a `20`.

3. **Operador mayor o igual que (>=):**

El operador mayor o igual que se utiliza para evaluar si un valor es mayor o igual que otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice >= 30;
```

En este ejemplo, utilizamos el operador mayor o igual que para seleccionar los productos cuyo precio unitario es mayor o igual que `30`. Devolverá los productos con un precio unitario igual o superior a `30`.

4. **Operador menor o igual que (<=):**

El operador menor o igual que se utiliza para evaluar si un valor es menor o igual que otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice <= 10;
```

En este ejemplo, utilizamos el operador menor o igual que para seleccionar los productos cuyo precio unitario es menor o igual que `10`. Devolverá los productos con un precio unitario igual o inferior a `10`.

5. **Operador distinto de (<>, !=):**

El operador distinto de se utiliza para evaluar si un valor es diferente de otro valor.
Ejemplo:

```
USE Northwind;
GO

SELECT ProductName, UnitPrice
FROM Products
WHERE UnitPrice <> 15;
```

En este ejemplo, utilizamos el operador distinto de para seleccionar los productos cuyo precio unitario no es igual a `15`. Devolverá los productos con un precio unitario diferente de `15`.

Es importante tener en cuenta que estos operadores de comparación también se pueden combinar con otros operadores y utilizar en condiciones más complejas en las cláusulas `WHERE` de las consultas SQL. Permiten filtrar y obtener conjuntos de datos específicos según criterios de comparación.

[🔼](#índice)

---

## **103. Proceso SP_HELP**

El procedimiento almacenado `sp_help` en SQL Server es una utilidad incorporada que proporciona información detallada sobre un objeto de base de datos específico. Se utiliza para obtener información sobre tablas, vistas, procedimientos almacenados, funciones y otros objetos de la base de datos.

El `sp_help` acepta como parámetro el nombre del objeto que se desea analizar y devuelve información relevante sobre ese objeto. La información proporcionada incluye el nombre, el tipo, las columnas, los índices, las restricciones y otros detalles del objeto.

Aquí tienes un ejemplo de cómo usar `sp_help` con la base de datos Northwind para obtener información sobre la tabla "`Customers`":

```
USE Northwind;
GO

EXEC sp_help 'Customers';
```

Al ejecutar este código, se mostrará un conjunto de resultados que contiene múltiples secciones con información sobre la tabla "`Customers`". Estas secciones pueden incluir:

1. **"Name" (Nombre):** El nombre completo de la tabla.

2. **"Owner" (Propietario):** El propietario de la tabla.

3. **"Type" (Tipo):** El tipo de objeto (en este caso, "`table`").

4. **"Columns" (Columnas):** Una lista de las columnas de la tabla, que incluye el nombre de la columna, el tipo de datos, la longitud máxima, etc.

5. **"Indexes" (Índices):** Una lista de los índices definidos en la tabla, incluyendo el nombre del índice, las columnas involucradas y el tipo de índice.

6. **"Keys" (Claves):** Información sobre las claves primarias y extranjeras definidas en la tabla, incluyendo los nombres de las claves, las columnas involucradas y la tabla relacionada en caso de claves foráneas.

7. **"Referenced by" (Referenciado por):** En caso de claves foráneas, muestra qué tablas hacen referencia a la tabla actual.

8. **"Text" (Texto):** El texto de la definición de la tabla.

El resultado exacto puede variar dependiendo de la versión de SQL Server que estés utilizando y la configuración de la base de datos.

El `sp_help` es una herramienta útil para obtener información rápida y detallada sobre los objetos de la base de datos. Puede ayudar en tareas de desarrollo y mantenimiento al proporcionar una visión general de la estructura y características de los objetos. Es importante destacar que `sp_help` solo muestra información sobre un objeto específico y no proporciona una visión completa de toda la base de datos.

[🔼](#índice)

---

## **104. Proceso SP_HELPTEXT**

El procedimiento almacenado `sp_helptext` en SQL Server es una utilidad incorporada que se utiliza para mostrar el texto de definición de un objeto de base de datos, como un procedimiento almacenado, una función o una vista. Proporciona el código fuente completo de dicho objeto, lo que resulta útil para entender cómo está implementado.

El `sp_helptext` acepta como parámetro el nombre del objeto para el cual se desea obtener el texto de definición y devuelve el código fuente del objeto en forma de múltiples filas de texto.

Aquí tienes un ejemplo de cómo usar `sp_helptext` con la base de datos Northwind para obtener el código fuente de un procedimiento almacenado llamado "`CustOrdersDetail`":

```
USE Northwind;
GO

EXEC sp_helptext 'CustOrdersDetail';
```

Al ejecutar este código, se mostrará un conjunto de resultados que contiene múltiples filas de texto que conforman el código fuente del procedimiento almacenado "`CustOrdersDetail`". Cada fila representa una parte del código fuente, y las filas se pueden combinar para reconstruir el código completo.

Es importante tener en cuenta que `sp_helptext` solo muestra el código fuente de objetos de base de datos que son explícitamente visibles para el usuario actual y a los que se tiene permiso de acceso. Si no tienes permisos suficientes, es posible que no puedas ver el código fuente de ciertos objetos.

El uso de `sp_helptext` es útil cuando necesitas revisar y analizar la lógica y estructura de un procedimiento almacenado, función o vista en SQL Server. Puede ayudarte a comprender cómo se implementa un objeto y facilitar la identificación de errores o mejoras potenciales en el código.

Es importante tener en cuenta que `sp_helptext` muestra el texto de definición del objeto tal como está almacenado en la base de datos. Si se han realizado modificaciones al objeto sin actualizar el texto de definición, es posible que el resultado no refleje los cambios más recientes.

En resumen, el uso de `sp_helptext` te permite acceder rápidamente al código fuente de un objeto de base de datos y te brinda la posibilidad de revisar y analizar su implementación. Esto puede ser especialmente útil en tareas de desarrollo, resolución de problemas y mantenimiento de la base de datos.

[🔼](#índice)

---

## **105. Agregando Shortcuts en la consola (sp_help, sp_helptext)**

En SQL Server, puedes agregar atajos o shortcuts personalizados en la consola para ejecutar comandos comunes de forma más rápida. Esto puede incluir la creación de atajos para ejecutar los procedimientos almacenados `sp_help` y `sp_helptext` en la base de datos Northwind.

Aquí tienes una explicación detallada de cómo agregar shortcuts para `sp_help` y `sp_helptext` en la consola de SQL Server Management Studio (SSMS):

1. Creación de un shortcut para `sp_help`:

- Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde se encuentra la base de datos Northwind.
- Haz clic en "`Tools`" (Herramientas) en la barra de menú superior y selecciona "`Options`" (Opciones).
- En la ventana "`Options`" (Opciones), expande "`Environment`" (Entorno) en el panel izquierdo y selecciona "`Keyboard`" (Teclado).
- En la parte inferior de la ventana, en la sección "`Show commands containing`", escribe "`sp_help`".
- En la lista "`Shortcut(s) for selected command`", selecciona un atajo disponible, por ejemplo, "`Ctrl+1`".
- Haz clic en "`Assign`" (Asignar) y luego en "`OK`" para guardar los cambios.

Ahora, puedes usar el atajo "`Ctrl+1`" para ejecutar rápidamente el procedimiento almacenado `sp_help` en cualquier ventana de consulta en `SSMS`. Puedes probarlo ejecutando lo siguiente:

```
USE Northwind;
GO

EXEC sp_help 'Customers';
```

2. Creación de un shortcut para `sp_helptext`:

- Sigue los mismos pasos iniciales para abrir la ventana "`Options`" (Opciones) en SSMS.
- En la sección "`Show commands containing`", escribe "`sp_helptext`".
- Selecciona un atajo disponible, por ejemplo, "`Ctrl+2`".
- Haz clic en "`Assign`" (Asignar) y luego en "`OK`" para guardar los cambios.

Ahora, puedes usar el atajo "`Ctrl+2`" para ejecutar rápidamente el procedimiento almacenado `sp_helptext` en cualquier ventana de consulta en SSMS. Puedes probarlo ejecutando lo siguiente:

```
USE Northwind;
GO

EXEC sp_helptext 'CustOrdersDetail';
```

Al agregar estos shortcuts, puedes acelerar tu flujo de trabajo al acceder rápidamente a los procedimientos almacenados `sp_help` y `sp_helptext` sin tener que escribirlos completamente cada vez.

Ten en cuenta que los atajos personalizados que establezcas en SSMS solo estarán disponibles en esa instancia de SSMS. Si utilizas diferentes instancias de SSMS en diferentes entornos, es posible que necesites configurar los atajos en cada instancia por separado.

Recuerda adaptar los atajos según tus preferencias y disponibilidad. Los atajos mencionados aquí son solo ejemplos y puedes seleccionar otros que sean más adecuados para ti.

[🔼](#índice)

---

## **106. Las sentencias SQL**

Las sentencias SQL (Structured Query Language) en SQL Server son comandos utilizados para interactuar con una base de datos y realizar operaciones como consultas, inserciones, actualizaciones, eliminaciones y más. Estas sentencias permiten a los desarrolladores y administradores de bases de datos manipular y administrar los datos almacenados en una base de datos.

Aquí tienes una explicación detallada de algunas de las sentencias SQL más comunes junto con ejemplos utilizando la base de datos Northwind:

1. **SELECT:**

La sentencia `SELECT` se utiliza para recuperar datos de una o más tablas en una base de datos.

Ejemplo:

```
USE Northwind;
GO

SELECT * FROM Customers;
```

En este ejemplo, la sentencia `SELECT` recupera todos los registros de la tabla "`Customers`" en la base de datos Northwind.

2. **INSERT INTO:**

La sentencia `INSERT INTO` se utiliza para insertar nuevos registros en una tabla de la base de datos.

Ejemplo:

```
USE Northwind;
GO

INSERT INTO Customers (CustomerID, CompanyName, ContactName)
VALUES ('ABC123', 'Example Company', 'John Doe');
```

En este ejemplo, la sentencia `INSERT INTO` inserta un nuevo registro en la tabla "`Customers`" con los valores proporcionados para las columnas "`CustomerID`", "`CompanyName`" y "`ContactName`".

3. **UPDATE:**

La sentencia `UPDATE` se utiliza para actualizar los valores de uno o más registros en una tabla de la base de datos.

Ejemplo:

```
USE Northwind;
GO

UPDATE Customers
SET ContactName = 'Jane Smith'
WHERE CustomerID = 'ABC123';
```

En este ejemplo, la sentencia `UPDATE` actualiza el valor de la columna "`ContactName`" a '`Jane Smith`' en la tabla "`Customers`" para el registro con el `CustomerID` '`ABC123`'.

4. **DELETE FROM:**

La sentencia `DELETE FROM` se utiliza para eliminar uno o más registros de una tabla de la base de datos.

Ejemplo:

```
USE Northwind;
GO

DELETE FROM Customers
WHERE CustomerID = 'ABC123';
```

En este ejemplo, la sentencia `DELETE FROM` elimina el registro de la tabla "`Customers`" que tiene el `CustomerID` '`ABC123`'.

Estas son solo algunas de las sentencias SQL más comunes en SQL Server. Hay otras sentencias disponibles, como `CREATE TABLE` para crear tablas, `ALTER TABLE` para modificar la estructura de una tabla, y muchas más. Estas sentencias permiten a los desarrolladores y administradores de bases de datos realizar una amplia gama de operaciones en la base de datos según sus necesidades.

Es importante tener en cuenta que las sentencias SQL deben escribirse con precisión y seguir la sintaxis correcta para evitar errores y obtener los resultados deseados. Además, siempre es recomendable realizar pruebas y asegurarse de comprender el impacto de una sentencia antes de ejecutarla en un entorno de producción.

[🔼](#índice)

---

## **107. La Sentencia CREATE (Table, Type, Function)**

La sentencia `CREATE` en SQL Server se utiliza para crear nuevos objetos en la base de datos, como tablas, tipos de datos definidos por el usuario y funciones. A continuación, te brindo una explicación detallada de cada una de estas variantes, junto con ejemplos utilizando la base de datos Northwind.

1. **CREATE TABLE:**

La sentencia `CREATE TABLE` se utiliza para crear una nueva tabla en la base de datos. Define la estructura de la tabla, incluyendo los nombres de las columnas, los tipos de datos y las restricciones.

Ejemplo:

```
USE Northwind;
GO

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID CHAR(5),
    OrderDate DATE,
    TotalAmount DECIMAL(10,2),
    ShipAddress VARCHAR(100)
);
```

En este ejemplo, la sentencia `CREATE TABLE` crea una nueva tabla llamada "`Orders`" con cinco columnas: "`OrderID`", "`CustomerID`", "`OrderDate`", "`TotalAmount`" y "`ShipAddress`". La columna "`OrderID`" se define como clave primaria.

2. **CREATE TYPE:**

La sentencia `CREATE TYPE` se utiliza para crear un nuevo tipo de datos definido por el usuario en la base de datos. Estos tipos de datos personalizados pueden contener múltiples propiedades y estructuras de datos.

Ejemplo:

```
USE Northwind;
GO

CREATE TYPE AddressType AS TABLE (
    Street VARCHAR(100),
    City VARCHAR(50),
    Country VARCHAR(50)
);
```

En este ejemplo, la sentencia `CREATE TYPE` crea un nuevo tipo de datos llamado "`AddressType`". Este tipo de datos define una estructura de tabla con tres columnas: "`Street`", "`City`" y "`Country`". Este tipo de datos personalizado se puede utilizar luego en columnas de tablas o parámetros de procedimientos almacenados.

3. **CREATE FUNCTION:**

La sentencia CREATE FUNCTION se utiliza para crear una nueva función en la base de datos. Una función es un objeto que realiza cálculos o manipulaciones de datos y devuelve un resultado.

Ejemplo:

```
USE Northwind;
GO

CREATE FUNCTION CalculateOrderTotal (@OrderID INT)
RETURNS MONEY
AS
BEGIN
    DECLARE @TotalAmount MONEY;

    SELECT @TotalAmount = SUM(UnitPrice * Quantity)
    FROM [Order Details]
    WHERE OrderID = @OrderID;

    RETURN @TotalAmount;
END;
```

En este ejemplo, la sentencia `CREATE FUNCTION` crea una nueva función llamada "`CalculateOrderTotal`". Esta función toma el parámetro "`@OrderID`" y realiza un cálculo para obtener el monto total de un pedido sumando el producto del precio unitario y la cantidad de cada artículo en la tabla "`[Order Details]`". El resultado se devuelve como un tipo de datos `MONEY`.

Es importante tener en cuenta que estas son solo algunas de las variantes de la sentencia `CREATE` en SQL Server. También puedes utilizar `CREATE PROCEDURE` para crear procedimientos almacenados, `CREATE VIEW` para crear vistas y `CREATE INDEX` para crear índices, entre otras opciones.

Recuerda que al utilizar la sentencia `CREATE`, debes tener los permisos adecuados para crear nuevos objetos en la base de datos. Además, asegúrate de comprender la sintaxis y los parámetros específicos de cada variante de la sentencia `CREATE` para crear correctamente los objetos deseados en tu base de datos.

[🔼](#índice)

---

## **108. La Sentencia ALTER**

La sentencia `ALTER` en SQL Server se utiliza para modificar la estructura de los objetos existentes en la base de datos, como tablas, vistas, procedimientos almacenados y funciones. Permite realizar cambios como agregar columnas, cambiar el tipo de datos de una columna, eliminar restricciones, modificar la definición de un procedimiento almacenado, entre otros.

A continuación, te brindo una explicación detallada de cómo se utiliza la sentencia `ALTER`, junto con un ejemplo utilizando la base de datos Northwind:

1. **ALTER TABLE:**

La sentencia `ALTER TABLE` se utiliza para modificar la estructura de una tabla existente en la base de datos. Puedes agregar, modificar o eliminar columnas, restricciones y otros elementos relacionados con la tabla.

Ejemplo:

```
USE Northwind;
GO

ALTER TABLE Customers
ADD Email VARCHAR(100);
```

En este ejemplo, la sentencia `ALTER TABLE` agrega una nueva columna llamada "`Email`" a la tabla "`Customers`". La columna se define con un tipo de datos `VARCHAR` y una longitud de 100 caracteres.

2. **ALTER PROCEDURE:**

La sentencia `ALTER PROCEDURE` se utiliza para modificar la definición de un procedimiento almacenado existente en la base de datos. Puedes cambiar el código, los parámetros o cualquier otra parte del procedimiento almacenado.

Ejemplo:

```
USE Northwind;
GO

ALTER PROCEDURE GetCustomerOrders
    @CustomerID CHAR(5)
AS
BEGIN
    SELECT *
    FROM Orders
    WHERE CustomerID = @CustomerID;
END;
```

En este ejemplo, la sentencia `ALTER PROCEDURE` modifica la definición del procedimiento almacenado "`GetCustomerOrders`". En este caso, se cambia el nombre del parámetro a "`@CustomerID`" y se realiza una consulta para recuperar los pedidos correspondientes a ese `ID` de cliente.

3. **ALTER VIEW:**

La sentencia `ALTER VIEW` se utiliza para modificar la definición de una vista existente en la base de datos. Puedes cambiar la consulta subyacente, los nombres de columnas o cualquier otra parte de la vista.

Ejemplo:

```
USE Northwind;
GO

ALTER VIEW [dbo].[CustomerOrders]
AS
SELECT C.CustomerID, C.CompanyName, O.OrderID, O.OrderDate
FROM Customers C
INNER JOIN Orders O ON C.CustomerID = O.CustomerID;
```

En este ejemplo, la sentencia `ALTER VIEW` modifica la definición de la vista "`CustomerOrders`". Se cambia la consulta para incluir la columna "`OrderDate`" en los resultados y se establecen los alias de tabla para las tablas "`Customers`" y "`Orders`".

Recuerda que al utilizar la sentencia `ALTER`, debes tener los permisos adecuados para realizar modificaciones en los objetos de la base de datos. Además, asegúrate de comprender cómo afectarán los cambios realizados a la estructura existente y a cualquier otro código o consulta que dependa de los objetos modificados.

Es recomendable realizar copias de seguridad de la base de datos antes de ejecutar sentencias `ALTER`, especialmente en entornos de producción, para poder revertir los cambios si es necesario.

[🔼](#índice)

---

## **109. La Sentencia DROP**

La sentencia `DROP` en SQL Server se utiliza para eliminar objetos existentes en la base de datos, como tablas, vistas, procedimientos almacenados, funciones, índices, restricciones y más. Esta sentencia permite eliminar completamente un objeto y todos sus datos asociados de la base de datos.

A continuación, te brindo una explicación detallada de cómo se utiliza la sentencia `DROP`, junto con ejemplos utilizando la base de datos Northwind:

1. **DROP TABLE:**

La sentencia `DROP TABLE` se utiliza para eliminar una tabla existente en la base de datos. Al ejecutar esta sentencia, se eliminan todos los datos y la estructura de la tabla.

Ejemplo:

```
USE Northwind;
GO

DROP TABLE Customers;
```

En este ejemplo, la sentencia `DROP TABLE` elimina completamente la tabla "`Customers`" de la base de datos Northwind, junto con todos los datos y la estructura asociada.

2. **DROP PROCEDURE:**

La sentencia `DROP PROCEDURE` se utiliza para eliminar un procedimiento almacenado existente en la base de datos. Al ejecutar esta sentencia, se elimina completamente la definición del procedimiento almacenado.

Ejemplo:

```
USE Northwind;
GO

DROP PROCEDURE GetCustomerOrders;
```

En este ejemplo, la sentencia `DROP PROCEDURE` elimina el procedimiento almacenado "`GetCustomerOrders`" de la base de datos Northwind.

3. **DROP VIEW:**

La sentencia `DROP VIEW` se utiliza para eliminar una vista existente en la base de datos. Al ejecutar esta sentencia, se elimina completamente la definición de la vista.

Ejemplo:

```
USE Northwind;
GO

DROP VIEW [dbo].[CustomerOrders];
```

En este ejemplo, la sentencia `DROP VIEW` elimina la vista "`CustomerOrders`" de la base de datos Northwind.

Recuerda que al utilizar la sentencia `DROP`, debes tener los permisos adecuados para eliminar objetos de la base de datos. Además, ten en cuenta que una vez que se ejecuta la sentencia `DROP`, no hay forma de recuperar los datos o la definición del objeto eliminado, a menos que se haya realizado una copia de seguridad previa.

Es importante tener precaución al utilizar la sentencia `DROP` y asegurarse de que se están eliminando los objetos correctos, ya que los datos y la estructura de la base de datos pueden perderse permanentemente. Es recomendable realizar copias de seguridad regulares y tener un plan de recuperación en caso de eliminar accidentalmente objetos importantes.

[🔼](#índice)

---

## **110. La Sentencia TRUNCATE**

La sentencia `TRUNCATE` en SQL Server se utiliza para eliminar todos los registros de una tabla de la base de datos de manera rápida y eficiente. A diferencia de la sentencia `DELETE`, que elimina registros uno por uno y genera registros de deshacer (undo logs) para cada eliminación, `TRUNCATE` elimina todos los registros de la tabla de una vez, liberando así el espacio utilizado.

A continuación, te brindo una explicación detallada de cómo se utiliza la sentencia `TRUNCATE`, junto con un ejemplo utilizando la base de datos Northwind:

Ejemplo:

```
USE Northwind;
GO

TRUNCATE TABLE Customers;
```

En este ejemplo, la sentencia `TRUNCATE TABLE` se utiliza para eliminar todos los registros de la tabla "`Customers`" de la base de datos Northwind.

Algunos puntos importantes a tener en cuenta sobre la sentencia `TRUNCATE`:

1. No se pueden utilizar cláusulas `WHERE` con `TRUNCATE`. La sentencia eliminará todos los registros de la tabla sin excepción.

2. `TRUNCATE` es una operación `DDL` (Data Definition Language) y no una operación `DML` (Data Manipulation Language). Esto significa que `TRUNCATE` no genera registros de deshacer (undo logs) y no se puede deshacer una vez ejecutada. Por lo tanto, debes tener cuidado al usar `TRUNCATE`, ya que no se puede recuperar los datos eliminados.

3. `TRUNCATE` reinicia el identificador de la tabla. Si la tabla tiene una columna de identidad (identity column), el valor se restablecerá al valor inicial especificado en la definición de la columna.

4. `TRUNCATE` es más rápido que `DELETE` para eliminar todos los registros de una tabla, ya que no realiza un seguimiento de cada eliminación individual en los registros de deshacer (undo logs).

Es importante tener precaución al utilizar la sentencia `TRUNCATE`, ya que eliminará todos los registros de la tabla de una vez. Asegúrate de tener copias de seguridad adecuadas de los datos antes de ejecutar `TRUNCATE` en una tabla para evitar la pérdida permanente de información importante. Además, asegúrate de tener los permisos necesarios para ejecutar `TRUNCATE` en la tabla específica.

**Conclusión**

Las sentencias SQL en SQL Server son herramientas fundamentales para interactuar con una base de datos y realizar diversas operaciones, como crear, modificar y eliminar objetos, así como manipular y consultar datos. A través de las diferentes sentencias, podemos diseñar y mantener la estructura de la base de datos, así como realizar consultas y obtener resultados específicos.

En la base de datos Northwind, podemos ver ejemplos de cómo se utilizan estas sentencias en el contexto de un sistema de gestión de pedidos y ventas. Algunas de las sentencias más comunes y utilizadas son:

1. La sentencia `CREATE` se utiliza para crear nuevos objetos en la base de datos, como tablas, vistas, procedimientos almacenados y funciones. Por ejemplo, podemos utilizar `CREATE TABLE` para crear una nueva tabla "`Orders`" con columnas como "`OrderID`", "`CustomerID`" y "`OrderDate`".

2. La sentencia `ALTER` se utiliza para modificar la estructura de los objetos existentes en la base de datos. Por ejemplo, `ALTER TABLE` nos permite agregar columnas adicionales a una tabla existente, como agregar la columna "`Email`" a la tabla "`Customers`".

3. La sentencia `DROP` se utiliza para eliminar objetos existentes en la base de datos. Por ejemplo, podemos utilizar `DROP TABLE` para eliminar completamente una tabla, como la tabla "`Customers`" en la base de datos Northwind.

4. La sentencia `TRUNCATE` se utiliza para eliminar todos los registros de una tabla de manera eficiente. Por ejemplo, podemos utilizar `TRUNCATE TABLE` para eliminar todos los registros de la tabla "`Customers`" y reiniciar el identificador de la tabla.

Estas sentencias SQL son esenciales para administrar y manipular datos en una base de datos. Nos permiten crear y modificar la estructura de los objetos, realizar operaciones de eliminación eficientes y mantener la integridad de los datos.

En conclusión, las sentencias SQL en SQL Server son una parte fundamental del lenguaje de consulta estructurado y proporcionan una forma poderosa de interactuar con una base de datos. Su uso adecuado nos permite diseñar y mantener la estructura de la base de datos, realizar operaciones de manipulación de datos y obtener resultados específicos según nuestras necesidades. A través de los ejemplos en la base de datos Northwind, podemos comprender cómo estas sentencias se aplican en un contexto real y cómo afectan la estructura y los datos de la base de datos.

[🔼](#índice)

---

| **Inicio**            | **atrás 10**                | **Siguiente 12**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./10_Consultas_SQL.md) | [⏩](./12_Consultas_SQL.md) |
