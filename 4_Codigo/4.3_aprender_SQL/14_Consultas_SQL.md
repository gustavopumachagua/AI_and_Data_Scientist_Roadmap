| **Inicio**            | **atrás 13**                | **Siguiente 15**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./13_Consultas_SQL.md) | [⏩](./15_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                  |
| -------------------------------------------------------------------------------------------------------- |
| [131. Introducción tablas temporales](#131-introducción-tablas-temporales)                               |
| [132. Definición y uso de Tabla Temporal en Memoria](#132-definición-y-uso-de-tabla-temporal-en-memoria) |
| [133. Definición y uso de Tabla Temporal Física](#133-definición-y-uso-de-tabla-temporal-física)         |
| [134. Introducción Tablas Temporales](#134-introducción-tablas-temporales)                               |
| [135. ¿Qué es una Vista? Uso e implementación](#135-¿qué-es-una-vista-uso-e-implementación)              |
| [136. Creando una vista desde el entorno gráfico](#136-creando-una-vista-desde-el-entorno-gráfico)       |
| [137. Conclusión las vistas en SQL](#137-conclusión-las-vistas-en-sql)                                   |
| [138. Introducción Trigger](#138-introducción-trigger)                                                   |
| [139. ¿Qué es un Trigger? Tipos posibles](#139-¿qué-es-un-trigger-tipos-posibles)                        |
| [140. Creación de Trigger de tipo INSERT](#140-creación-de-trigger-de-tipo-insert)                       |

---

# **Tutorial de SQL**

## **131. Introducción tablas temporales**

Las tablas temporales en SQL Server son tablas que se utilizan para almacenar datos temporales durante la ejecución de una consulta o de un proceso. Estas tablas son creadas en la base de datos `TempDB` y están disponibles solo durante la sesión de conexión en la que se crean. Las tablas temporales se utilizan principalmente para almacenar datos intermedios o para realizar operaciones complejas en conjunto con otras consultas.

Aquí tienes una explicación detallada de las tablas temporales, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de tablas temporales:

Para crear una tabla temporal, debes seguir los siguientes pasos:

- Especifica el nombre de la tabla `temporal`, que debe comenzar con el símbolo "`#`" o "`##`" (tabla local o tabla global, respectivamente).
- Define la estructura de la tabla, especificando las columnas y los tipos de datos.
- Opcionalmente, puedes agregar restricciones, índices u otras propiedades a la tabla.

2. Ejemplo de tabla temporal:

Supongamos que queremos realizar una consulta que involucre datos de la tabla "`OrderDetails`" y necesitamos almacenar los resultados intermedios en una tabla temporal. Utilizaremos la base de datos Northwind, donde tenemos la tabla "`OrderDetails`".

Ejemplo de tabla temporal:

```
USE Northwind;
GO

CREATE TABLE #TempOrderDetails
(
    OrderID INT,
    ProductID INT,
    Quantity INT,
    UnitPrice MONEY
);
```

En este ejemplo, creamos una tabla temporal llamada "`#TempOrderDetails`" con las mismas columnas que la tabla "`OrderDetails`". El prefijo "`#`" indica que es una tabla local, que solo está disponible dentro de la sesión de conexión actual.

3. Uso de tablas temporales:

Una vez que has creado una tabla temporal, puedes utilizarla en consultas SQL como cualquier otra tabla. Por ejemplo:

```
INSERT INTO #TempOrderDetails (OrderID, ProductID, Quantity, UnitPrice)
SELECT OrderID, ProductID, Quantity, UnitPrice
FROM OrderDetails
WHERE OrderID IN (SELECT OrderID FROM Orders WHERE CustomerID = 'ALFKI');
```

Esta consulta inserta datos de la tabla "`OrderDetails`" en la tabla temporal "`#TempOrderDetails`" solo para los pedidos realizados por el cliente con el ID '`ALFKI`'.

Luego, puedes realizar otras operaciones o consultas utilizando la tabla temporal como parte de la lógica de tu consulta.

4. Eliminación de tablas temporales:

Las tablas temporales se eliminan automáticamente al finalizar la sesión de conexión en la que se crearon. Sin embargo, también puedes eliminar una tabla temporal de forma explícita utilizando la instrucción `DROP TABLE`. Por ejemplo:

`DROP TABLE #TempOrderDetails;`

Esta instrucción elimina la tabla temporal "`#TempOrderDetails`".

Las tablas temporales en SQL Server son útiles cuando necesitas almacenar datos temporales para realizar operaciones complejas o almacenar resultados intermedios durante una sesión de conexión. Puedes utilizar tablas temporales para simplificar consultas complejas, dividir lógica en etapas o incluso mejorar el rendimiento al almacenar datos intermedios en lugar de realizar múltiples consultas a tablas reales. Sin embargo, es importante recordar que las tablas temporales están limitadas a la sesión de conexión en la que se crean y no son accesibles desde otras sesiones o conexiones.

[🔼](#índice)

---

## **132. Definición y uso de Tabla Temporal en Memoria**

Una tabla temporal en memoria en SQL Server es una estructura de datos que se crea y almacena en la memoria principal en lugar de en el disco duro. A diferencia de las tablas temporales tradicionales que se crean en la base de datos `TempDB`, las tablas temporales en memoria se crean en la base de datos actual y se almacenan completamente en la memoria, lo que puede mejorar significativamente el rendimiento de las consultas.

Aquí tienes una explicación detallada sobre las tablas temporales en memoria, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de tablas temporales en memoria:

Para crear una tabla temporal en memoria, debes seguir los siguientes pasos:

- Especifica el nombre de la tabla temporal, que debe comenzar con el símbolo "`#`" o "`##`" (tabla local o tabla global, respectivamente).
- Define la estructura de la tabla, especificando las columnas y los tipos de datos.
- Agrega la cláusula "`WITH (MEMORY_OPTIMIZED = ON)`" para indicar que la tabla se almacenará en memoria.

2. Ejemplo de tabla temporal en memoria:

Supongamos que queremos almacenar temporalmente los resultados intermedios de una consulta que involucra la tabla "`OrderDetails`". Utilizaremos la base de datos Northwind, donde tenemos la tabla "`OrderDetails`".

Ejemplo de tabla temporal en memoria:

```
USE Northwind;
GO

CREATE TABLE #TempOrderDetails
(
    OrderID INT,
    ProductID INT,
    Quantity INT,
    UnitPrice MONEY
)
WITH (MEMORY_OPTIMIZED = ON);
```

En este ejemplo, creamos una tabla temporal en memoria llamada "`#TempOrderDetails`" con las mismas columnas que la tabla "`OrderDetails`". El prefijo "`#`" indica que es una tabla local. La cláusula "`WITH (MEMORY_OPTIMIZED = ON)`" indica que la tabla se almacenará en memoria.

3. Uso de tablas temporales en memoria:

Una vez que has creado una tabla temporal en memoria, puedes utilizarla en consultas SQL de la misma manera que cualquier otra tabla. Por ejemplo:

```
INSERT INTO #TempOrderDetails (OrderID, ProductID, Quantity, UnitPrice)
SELECT OrderID, ProductID, Quantity, UnitPrice
FROM OrderDetails
WHERE OrderID IN (SELECT OrderID FROM Orders WHERE CustomerID = 'ALFKI');
```

Esta consulta inserta datos de la tabla "`OrderDetails`" en la tabla temporal en memoria "`#TempOrderDetails`" solo para los pedidos realizados por el cliente con el ID '`ALFKI`'.

Luego, puedes realizar otras operaciones o consultas utilizando la tabla temporal en memoria como parte de la lógica de tu consulta.

4. Eliminación de tablas temporales en memoria:

Al igual que con las tablas temporales tradicionales, las tablas temporales en memoria se eliminan automáticamente al finalizar la sesión de conexión en la que se crearon. Sin embargo, también puedes eliminar una tabla temporal en memoria de forma explícita utilizando la instrucción `DROP TABLE`. Por ejemplo:

`DROP TABLE #TempOrderDetails;`

Esta instrucción elimina la tabla temporal en memoria "`#TempOrderDetails`".

Las tablas temporales en memoria en SQL Server son una opción eficiente para almacenar datos temporales en la memoria principal y mejorar el rendimiento de las consultas. Al estar completamente en memoria, las operaciones de lectura y escritura en estas tablas son mucho más rápidas que en las tablas tradicionales en disco. Sin embargo, ten en cuenta que el uso de tablas temporales en memoria requiere más recursos de memoria y solo están disponibles dentro de la sesión de conexión en la que se crean.

[🔼](#índice)

---

## **133. Definición y uso de Tabla Temporal Física**

En SQL Server, una tabla temporal física es una tabla temporal que se crea en la base de datos `TempDB` y se utiliza para almacenar datos temporales durante la ejecución de una consulta o un proceso. A diferencia de las tablas temporales en memoria, las tablas temporales físicas se almacenan en el disco y pueden ser compartidas y accedidas por múltiples sesiones o conexiones simultáneamente.

Aquí tienes una explicación detallada sobre las tablas temporales físicas, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de tablas temporales físicas:

Para crear una tabla temporal física, debes seguir los siguientes pasos:

- Especifica el nombre de la tabla temporal, que debe comenzar con el prefijo "`#`".
- Define la estructura de la tabla, especificando las columnas y los tipos de datos.

2. Ejemplo de tabla temporal física:

Supongamos que queremos almacenar temporalmente los resultados intermedios de una consulta que involucra la tabla "`OrderDetails`". Utilizaremos la base de datos Northwind, donde tenemos la tabla "`OrderDetails`".

Ejemplo de tabla temporal física:

```
USE TempDB;
GO

CREATE TABLE #TempOrderDetails
(
    OrderID INT,
    ProductID INT,
    Quantity INT,
    UnitPrice MONEY
);
```

En este ejemplo, creamos una tabla temporal física llamada "`#TempOrderDetails`" en la base de datos `TempDB` con las mismas columnas que la tabla "`OrderDetails`". El prefijo "`#`" indica que es una tabla temporal.

3. Uso de tablas temporales físicas:

Una vez que has creado una tabla temporal física, puedes utilizarla en consultas SQL de la misma manera que cualquier otra tabla. Por ejemplo:

```
INSERT INTO #TempOrderDetails (OrderID, ProductID, Quantity, UnitPrice)
SELECT OrderID, ProductID, Quantity, UnitPrice
FROM Northwind.dbo.OrderDetails
WHERE OrderID IN (SELECT OrderID FROM Northwind.dbo.Orders WHERE CustomerID = 'ALFKI');
```

Esta consulta inserta datos de la tabla "`OrderDetails`" en la tabla temporal física "`#TempOrderDetails`" solo para los pedidos realizados por el cliente con el ID '`ALFKI`'.

Luego, puedes realizar otras operaciones o consultas utilizando la tabla temporal física como parte de la lógica de tu consulta.

4. Eliminación de tablas temporales físicas:

Las tablas temporales físicas se eliminan automáticamente al finalizar la conexión en la que se crearon. Sin embargo, también puedes eliminar una tabla temporal física de forma explícita utilizando la instrucción `DROP TABLE`. Por ejemplo:

```
USE TempDB;
GO

DROP TABLE #TempOrderDetails;
```

Esta instrucción elimina la tabla temporal física "`#TempOrderDetails`" de la base de datos `TempDB`.

Las tablas temporales físicas en SQL Server son útiles cuando necesitas compartir y acceder a datos temporales entre múltiples sesiones o conexiones. Aunque pueden ser más lentas que las tablas temporales en memoria debido a la necesidad de acceder al disco, siguen siendo una opción conveniente para el manejo de datos temporales en situaciones donde se requiere compartir datos entre diferentes partes de una aplicación o proceso.

[🔼](#índice)

---

## **134. Introducción Tablas Temporales**

En SQL Server, una vista es un objeto de base de datos que se crea a partir de una consulta y se almacena en la base de datos. Una vista actúa como una tabla virtual que permite acceder y manipular los datos de una o más tablas subyacentes mediante consultas. Proporciona una forma conveniente de presentar una vista lógica y estructurada de los datos para los usuarios, sin exponer la complejidad de las consultas subyacentes.

Aquí tienes una explicación detallada sobre las vistas, junto con un ejemplo utilizando la base de datos Northwind:

1. Creación de vistas:

Para crear una vista, debes seguir los siguientes pasos:

- Especifica el nombre de la vista.
- Define la consulta que determinará los datos que se mostrarán en la vista.
- Opcionalmente, puedes especificar columnas alias, filtros o cualquier otra cláusula de consulta.

2. Ejemplo de vista:

Supongamos que queremos crear una vista para mostrar los pedidos realizados por los clientes en la base de datos Northwind.

Ejemplo de creación de vista:

```
CREATE VIEW CustomerOrders AS
SELECT C.CustomerID, C.CompanyName, O.OrderID, O.OrderDate
FROM Customers C
JOIN Orders O ON C.CustomerID = O.CustomerID;
```

En este ejemplo, creamos una vista llamada "`CustomerOrders`" que muestra los campos `CustomerID`, `CompanyName`, `OrderID` y `OrderDate` para los pedidos realizados por los clientes. La vista combina la información de las tablas `Customers` y `Orders` utilizando una cláusula `JOIN`.

3. Uso de vistas:

Una vez que has creado una vista, puedes utilizarla como cualquier otra tabla en consultas `SELECT`, `INSERT`, `UPDATE` o `DELETE`. Por ejemplo:

`SELECT * FROM CustomerOrders WHERE CustomerID = 'ALFKI';`

Esta consulta selecciona todos los pedidos realizados por el cliente con el ID '`ALFKI`' utilizando la vista "`CustomerOrders`".

También puedes utilizar vistas en consultas más complejas o combinarlas con otras tablas o vistas para obtener resultados más elaborados.

4. Actualización de datos en vistas:

En general, las vistas son de solo lectura, lo que significa que no se pueden realizar operaciones de inserción, actualización o eliminación directamente en una vista. Sin embargo, en SQL Server es posible crear vistas actualizables utilizando ciertas reglas y restricciones, como tener claves primarias y cumplir con ciertos criterios de actualización. Esto permite realizar operaciones de actualización en las tablas subyacentes a través de la vista.

5. Modificación de vistas:

Puedes modificar una vista existente utilizando la instrucción `ALTER VIEW`. Esto te permite cambiar la definición de la vista, como agregar o eliminar columnas, modificar la consulta subyacente o cambiar los alias de columna.

6. Eliminación de vistas:

Puedes eliminar una vista utilizando la instrucción `DROP VIEW`. Esto eliminará la vista y todas las referencias a ella en consultas o procesos.

Las vistas en SQL Server ofrecen varias ventajas, como la simplificación y organización de consultas complejas, la presentación de datos específicos para diferentes usuarios y la protección de datos al limitar el acceso directo a las tablas subyacentes. Son una herramienta poderosa para el modelado de datos y la presentación de información en una forma más manejable y comprensible.

[🔼](#índice)

---

## **135. ¿Qué es una Vista? Uso e implementación**

Una vista en SQL Server es un objeto de base de datos que representa una consulta predefinida almacenada en forma de tabla virtual. Puede pensar en una vista como una tabla virtual que contiene filas y columnas, pero en realidad no almacena datos físicamente. En su lugar, se define mediante una consulta SQL y se crea como una estructura lógica que proporciona una representación organizada y filtrada de los datos de una o varias tablas subyacentes.

Las vistas se utilizan para simplificar la complejidad de las consultas, mejorar la seguridad de los datos y facilitar el acceso a la información relevante para los usuarios. Proporcionan una forma de ocultar la complejidad de las consultas SQL complejas detrás de una interfaz más simple y fácil de usar.

Para comprender mejor cómo se implementan y utilizan las vistas en SQL Server, vamos a usar la base de datos de ejemplo Northwind. Supongamos que queremos crear una vista que muestre información sobre los clientes y los pedidos correspondientes. Aquí está el ejemplo de cómo crearíamos una vista en SQL Server utilizando la base de datos Northwind:

```
USE Northwind;

-- Crear una vista que muestra información de clientes y pedidos
CREATE VIEW VistaClientesPedidos
AS
SELECT c.CustomerID, c.ContactName, o.OrderID, o.OrderDate
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID;
```

En este ejemplo, estamos creando una vista llamada "`VistaClientesPedidos`" que combina información de las tablas "`Customers`" y "`Orders`". La vista selecciona las columnas "`CustomerID`" y "`ContactName`" de la tabla "`Customers`", y las columnas "`OrderID`" y "`OrderDate`" de la tabla "`Orders`". La cláusula `JOIN` se utiliza para unir las dos tablas en función del campo "`CustomerID`".

Una vez que se ha creado la vista, se puede utilizar como una tabla normal en las consultas. Por ejemplo, podríamos ejecutar una consulta para obtener todos los clientes y los pedidos correspondientes:

```
SELECT *
FROM VistaClientesPedidos;
```

La consulta anterior devolverá los resultados de la vista "`VistaClientesPedidos`", que contendrá las columnas seleccionadas y los datos de las tablas subyacentes "`Customers`" y "`Orders`".

Es importante destacar que las vistas no almacenan datos físicamente, sino que se actualizan dinámicamente cuando se accede a ellas. Si se realizan cambios en las tablas subyacentes, como agregar, actualizar o eliminar registros, la vista reflejará automáticamente esos cambios en los resultados de la consulta.

En resumen, las vistas en SQL Server son objetos de base de datos que representan consultas predefinidas. Proporcionan una forma conveniente de simplificar las consultas, mejorar la seguridad y facilitar el acceso a los datos. Se pueden utilizar como tablas virtuales en las consultas y se actualizan dinámicamente en función de los cambios en las tablas subyacentes.

[🔼](#índice)

---

## **136. Creando una vista desde el entorno gráfico**

Para crear una vista desde el entorno gráfico en SQL Server, puedes utilizar SQL Server Management Studio (`SSMS`), que es una herramienta visual para administrar y trabajar con bases de datos SQL Server. A continuación, te explicaré cómo crear una vista utilizando `SSMS` con la base de datos Northwind como ejemplo:

1. Abre SQL Server Management Studio y conéctate a tu instancia de SQL Server.

2. Selecciona la base de datos Northwind en la ventana "`Explorador de objetos`" del `SSMS`.

3. Haz clic derecho sobre la carpeta "`Vistas`" y selecciona la opción "`Nueva vista`" en el menú desplegable. Se abrirá una nueva ventana de diseño de vista.

4. En la ventana de diseño de vista, puedes arrastrar y soltar las tablas necesarias desde la ventana "`Explorador de objetos`" a la cuadrícula de diseño. Por ejemplo, arrastra la tabla "`Customers`" y la tabla "`Orders`" a la cuadrícula.

5. Define la lógica de la vista mediante la selección de las columnas necesarias, la aplicación de condiciones o la utilización de funciones de agregado. Por ejemplo, selecciona las columnas "`CustomerID`", "`CompanyName`", "`OrderID`" y "`OrderDate`" de las tablas "`Customers`" y "`Orders`".

6. Si es necesario, puedes aplicar filtros o realizar cálculos adicionales utilizando expresiones SQL. Por ejemplo, puedes agregar una cláusula `WHERE` para filtrar solo los pedidos de un cliente específico.

7. Una vez que hayas definido la vista según tus necesidades, guarda la vista con un nombre descriptivo. Por ejemplo, "`CustomerOrders`".

8. Cierra la ventana de diseño de vista y ahora podrás ver la vista recién creada en la carpeta "`Vistas`" en el "`Explorador de objetos`" del SSMS.

A partir de este momento, puedes utilizar la vista creada en consultas SQL como si fuera una tabla normal. Por ejemplo, puedes ejecutar consultas `SELECT` en la vista "`CustomerOrders`" para obtener los pedidos realizados por los clientes.

Es importante tener en cuenta que la vista creada se guarda en la base de datos y se puede utilizar posteriormente en consultas y operaciones de datos. También puedes modificar o eliminar la vista utilizando las opciones correspondientes en el `SSMS`.

Recuerda que el uso de vistas puede mejorar la organización, la reutilización de código y la seguridad al ocultar los detalles de las tablas subyacentes y presentar datos específicos según tus necesidades.

[🔼](#índice)

---

## **137. Conclusión las vistas en SQL**

En conclusión, las vistas en SQL Server son objetos de base de datos que proporcionan una forma conveniente de presentar una vista lógica y estructurada de los datos almacenados en una o más tablas. Son una herramienta poderosa que permite simplificar consultas complejas, mejorar la seguridad al ocultar los detalles de las tablas subyacentes y facilitar la reutilización de código.

En el ejemplo de la base de datos Northwind, pudimos ver cómo crear una vista llamada "`CustomerOrders`" que muestra los campos `CustomerID`, `CompanyName`, `OrderID` y `OrderDate` para los pedidos realizados por los clientes. Esta vista combinaba la información de las tablas Customers y Orders utilizando la cláusula `JOIN`. Posteriormente, pudimos utilizar la vista "`CustomerOrders`" en consultas `SELECT` para obtener los pedidos realizados por los clientes.

Las vistas ofrecen varias ventajas, como:

1. **Simplificación de consultas complejas:**

Las vistas permiten encapsular consultas complejas en una estructura más manejable y fácil de comprender. Esto facilita el desarrollo y el mantenimiento de consultas complicadas, ya que se pueden crear vistas con la lógica necesaria y luego utilizarlas en consultas más simples.

2. **Seguridad y control de acceso a los datos:**

Las vistas permiten controlar el acceso a los datos al proporcionar una capa adicional de seguridad. Puedes limitar las columnas visibles en la vista, aplicar filtros y restringir el acceso a las tablas subyacentes. Esto garantiza que solo los usuarios autorizados puedan ver y manipular los datos.

3. **Reutilización de código:**

Las vistas se pueden utilizar en diferentes consultas y consultas en cascada. Esto evita la duplicación de código y promueve la reutilización, lo que resulta en un código más limpio y mantenible.

4. **Simplificación del diseño de la base de datos:**

Las vistas permiten crear una vista lógica personalizada de los datos, ocultando la complejidad y la estructura subyacente de las tablas. Esto facilita el diseño de bases de datos más intuitivas y centradas en las necesidades de los usuarios finales.

Es importante tener en cuenta que las vistas son objetos virtuales y no almacenan datos físicamente. En su lugar, ofrecen una representación lógica de los datos basada en las consultas definidas al crear la vista. Además, es posible actualizar, modificar o eliminar las vistas según sea necesario para adaptarse a los cambios en los requisitos del negocio.

En resumen, las vistas son una herramienta poderosa en SQL Server que permiten simplificar consultas, mejorar la seguridad y controlar el acceso a los datos, promover la reutilización de código y facilitar el diseño de bases de datos más intuitivas. Su uso adecuado puede mejorar la eficiencia y la productividad al interactuar con la base de datos.

[🔼](#índice)

---

## **138. Introducción Trigger**

Los Triggers (disparadores) en SQL Server son objetos de base de datos que se utilizan para automatizar acciones o responder a eventos específicos que ocurren en una tabla, como la inserción, actualización o eliminación de registros. Los triggers se ejecutan automáticamente en respuesta a eventos definidos y pueden contener código `T-SQL` para realizar acciones adicionales en la base de datos.

A continuación, te proporcionaré una explicación detallada de los `triggers` en SQL Server con un ejemplo utilizando la base de datos Northwind:

1. **Creación de un Trigger:**

Para crear un `trigger`, se utiliza la sentencia `CREATE TRIGGER`. Especificamos el nombre del `trigger`, la tabla a la que está asociado y el evento que activará el `trigger` (`INSERT`, `UPDATE` o `DELETE`). También definimos el tipo de `trigger` (`AFTER` o `INSTEAD OF`) y la acción que se realizará en el código del trigger.

Ejemplo de creación de un trigger en la tabla `Orders` de la base de datos Northwind que se activará después de una inserción:

```
CREATE TRIGGER OrderInserted
ON Orders
AFTER INSERT
AS
BEGIN
    -- Código del trigger
END;
```

2. **Código del Trigger:**

El código del `trigger` se encuentra dentro del bloque `BEGIN-END` y se ejecuta automáticamente cuando se activa el evento especificado. El código puede contener consultas SQL y otras instrucciones `T-SQL` para realizar acciones adicionales en la base de datos. Por ejemplo, podemos insertar datos en otra tabla, actualizar registros relacionados, enviar notificaciones por correo electrónico, etc.

Ejemplo de código de `trigger` que inserta una fila en la tabla `OrderDetails` cuando se inserta una nueva orden:

```
CREATE TRIGGER OrderInserted
ON Orders
AFTER INSERT
AS
BEGIN
    INSERT INTO OrderDetails (OrderID, ProductID, Quantity)
    SELECT i.OrderID, p.ProductID, 1
    FROM inserted i
    INNER JOIN Products p ON i.ProductID = p.ProductID;
END;
```

En este ejemplo, el `trigger` se activa después de la inserción de una nueva fila en la tabla `Orders`. El código del `trigger` realiza una inserción en la tabla `OrderDetails` utilizando los datos de la fila recién insertada en la tabla `Orders` y realiza una selección de la tabla `Products` para obtener el `ProductID` correspondiente.

3. **Tipos de Triggers:**

- **AFTER TRIGGER:** Se ejecuta después de que se haya realizado la acción en la tabla (`INSERT`, `UPDATE` o `DELETE`).
- **INSTEAD OF TRIGGER:** Se ejecuta en lugar de la acción original en la tabla. Se utiliza comúnmente para realizar validaciones adicionales o acciones personalizadas antes de realizar la acción original.

4. **Gestión de Triggers:**

Los triggers se pueden modificar, desactivar o eliminar según sea necesario. Puedes utilizar las sentencias `ALTER TRIGGER`, `DISABLE TRIGGER` y `DROP TRIGGER` respectivamente para realizar estas acciones.

Es importante tener en cuenta que los triggers pueden afectar el rendimiento de la base de datos si no se diseñan o gestionan correctamente. Es recomendable utilizar los triggers de manera cuidadosa y tener en cuenta las implicaciones en cuanto a la integridad de los datos y el rendimiento de las operaciones.

En resumen, los triggers en SQL Server son objetos de base de datos que se utilizan para automatizar acciones o responder a eventos específicos en una tabla. Permiten ejecutar código adicional en respuesta a la inserción, actualización o eliminación de registros. Los triggers pueden realizar acciones como la inserción, actualización o eliminación de datos en otras tablas, enviar notificaciones, realizar validaciones adicionales, entre otras. Son una herramienta poderosa para mantener la integridad de los datos y automatizar tareas en una base de datos.

[🔼](#índice)

---

## **139. ¿Qué es un Trigger? Tipos posibles**

Un `trigger` en SQL Server es un objeto de base de datos que se utiliza para realizar acciones automáticas en respuesta a eventos específicos que ocurren en una tabla. Estos eventos pueden ser la inserción, actualización o eliminación de registros en la tabla. Los `triggers` permiten ejecutar un conjunto de instrucciones `T-SQL` cuando se produce el evento definido, lo que brinda la posibilidad de realizar acciones adicionales en la base de datos.

Existen dos tipos de triggers en SQL Server:

1. **AFTER TRIGGER:**

Un `AFTER TRIGGER` se ejecuta después de que se haya completado la acción que lo activó. Por ejemplo, un `AFTER INSERT TRIGGER` se ejecutará después de que se haya insertado una fila en la tabla. Este tipo de `trigger` es el más comúnmente utilizado.

Ejemplo de un `AFTER TRIGGER` en la tabla `Orders` de la base de datos Northwind:

```
CREATE TRIGGER OrderInserted
ON Orders
AFTER INSERT
AS
BEGIN
    -- Código del trigger
END;
```

En este caso, el `trigger` "`OrderInserted`" se activará después de insertar una fila en la tabla "`Orders`". Puedes escribir el código necesario dentro del bloque `BEGIN-END` para realizar las acciones requeridas.

2. **INSTEAD OF TRIGGER:**

Un `INSTEAD OF TRIGGER` se ejecuta en lugar de la acción original que lo activó. Este tipo de `trigger` se utiliza comúnmente en situaciones donde se desea realizar una validación adicional o una acción personalizada antes de ejecutar la acción original.

Ejemplo de un `INSTEAD OF TRIGGER` en la tabla `Customers` de la base de datos Northwind:

```
CREATE TRIGGER InsteadOfDeleteCustomer
ON Customers
INSTEAD OF DELETE
AS
BEGIN
    -- Código del trigger
END;
```

En este ejemplo, el trigger "`InsteadOfDeleteCustomer`" se ejecutará en lugar de la operación `DELETE` en la tabla "`Customers`". Puedes proporcionar el código necesario dentro del bloque `BEGIN-END` para realizar las acciones personalizadas antes de realizar la eliminación.

Los triggers pueden ser útiles en diversas situaciones, como:

- **Mantener la integridad referencial:** Pueden utilizarse para asegurarse de que los datos insertados, actualizados o eliminados cumplan con las restricciones y reglas establecidas en la base de datos.

- **Auditoría de cambios:** Permiten registrar información sobre las acciones realizadas en una tabla, como quién realizó la acción y cuándo.

- **Actualizaciones automáticas:** Pueden utilizarse para actualizar automáticamente datos en otras tablas en función de las modificaciones realizadas en una tabla.

Es importante tener en cuenta que el uso de `triggers` puede afectar el rendimiento de la base de datos, especialmente si se ejecutan instrucciones complejas o se realizan operaciones costosas. Por lo tanto, se recomienda utilizar los `triggers` de manera cuidadosa y evaluar su impacto en el rendimiento del sistema.

En resumen, los `triggers` en SQL Server son objetos de base de datos que se utilizan para ejecutar acciones automáticas en respuesta a eventos específicos en una tabla. Pueden ser `AFTER TRIGGERS`, que se ejecutan después de la acción original, o `INSTEAD OF TRIGGERS`, que se ejecutan en lugar de la acción original. Los `triggers` son una herramienta poderosa para mantener la integridad de los datos y automatizar tareas en una base de datos.

[🔼](#índice)

---

## **140. Creación de Trigger de tipo INSERT**

Para crear un `trigger` de tipo `INSERT` en SQL Server, se utiliza la cláusula `AFTER INSERT` en la declaración `CREATE TRIGGER`. El `trigger` se activará automáticamente después de que se haya insertado una fila en la tabla especificada. Aquí tienes un ejemplo de creación de un `trigger` de tipo `INSERT` en la base de datos Northwind:

```
-- Crear una tabla para almacenar el historial de pedidos
CREATE TABLE OrderHistory (
    OrderID INT,
    OrderDate DATETIME,
    CustomerID VARCHAR(5),
    TotalAmount MONEY
);

-- Crear el trigger de tipo INSERT
CREATE TRIGGER InsertOrderHistory
ON Orders
AFTER INSERT
AS
BEGIN
    -- Insertar los datos del pedido en la tabla OrderHistory
    INSERT INTO OrderHistory (OrderID, OrderDate, CustomerID, TotalAmount)
    SELECT OrderID, OrderDate, CustomerID, TotalAmount
    FROM inserted;
END;
```

En este ejemplo, se crea una tabla llamada `OrderHistory` que se utilizará para almacenar el historial de pedidos. A continuación, se crea el trigger `InsertOrderHistory` en la tabla `Orders`. El trigger se ejecutará después de que se haya insertado una fila en la tabla `Orders`. Dentro del bloque `BEGIN-END` del trigger, se utiliza la instrucción `INSERT INTO` para insertar los datos del pedido en la tabla `OrderHistory`. La cláusula `SELECT` se utiliza junto con la tabla especial inserted para obtener los datos de la fila insertada en la tabla `Orders`.

Cuando se inserte una nueva fila en la tabla `Orders`, el trigger `InsertOrderHistory` se activará automáticamente y registrará los datos del pedido en la tabla `OrderHistory`. Esto proporciona un registro histórico de todos los pedidos realizados en la base de datos.

Es importante destacar que el código dentro del trigger puede ser personalizado según los requisitos específicos. En este ejemplo, solo se insertan los datos del pedido en la tabla `OrderHistory`, pero puedes agregar lógica adicional, como validaciones o actualizaciones en otras tablas, según sea necesario.

Los triggers de tipo `INSERT` son útiles para realizar acciones adicionales después de insertar datos en una tabla. Pueden utilizarse para auditar cambios, mantener la integridad de los datos o realizar cálculos automáticos. Sin embargo, es importante tener en cuenta que los triggers pueden afectar el rendimiento de la base de datos, por lo que se recomienda utilizarlos con prudencia y considerar su impacto en el rendimiento del sistema.

**Conclusión**

En conclusión, los `triggers` en SQL Server son objetos de base de datos que se utilizan para realizar acciones automáticas en respuesta a eventos específicos, como operaciones de inserción, actualización o eliminación en una tabla. Proporcionan una forma de implementar lógica empresarial adicional o mantener la integridad de los datos en la base de datos.

Los `triggers` se definen en una tabla y se activan automáticamente cuando ocurre un evento especificado. Pueden realizar acciones como insertar, actualizar, eliminar registros en otras tablas, generar registros de auditoría, aplicar validaciones adicionales, entre otros. Los `triggers` son útiles cuando se requiere realizar acciones adicionales o realizar verificaciones antes o después de realizar cambios en los datos.

Un ejemplo concreto de uso de `triggers` en la base de datos Northwind sería el siguiente:

Supongamos que deseamos mantener un registro de cambios en la tabla de productos cada vez que se realice una actualización en el campo `UnitPrice`. Podemos crear un `trigger` que registre automáticamente el cambio en una tabla de auditoría:

```
-- Crear tabla de auditoría para cambios en productos
CREATE TABLE ProductAudit (
    ProductID INT,
    OldUnitPrice MONEY,
    NewUnitPrice MONEY,
    ChangeDate DATETIME
);

-- Crear el trigger de tipo UPDATE
CREATE TRIGGER UpdateProductAudit
ON Products
AFTER UPDATE
AS
BEGIN
    -- Insertar los datos del cambio en la tabla ProductAudit
    INSERT INTO ProductAudit (ProductID, OldUnitPrice, NewUnitPrice, ChangeDate)
    SELECT ProductID, UnitPrice AS OldUnitPrice, i.UnitPrice AS NewUnitPrice, GETDATE()
    FROM inserted i
    INNER JOIN deleted d ON i.ProductID = d.ProductID
    WHERE i.UnitPrice <> d.UnitPrice;
END;
```

En este ejemplo, se crea una tabla llamada `ProductAudit` para almacenar los registros de auditoría de cambios en el precio de los productos. Luego se crea el `trigger` `UpdateProductAudit` en la tabla `Products`, que se activará después de una operación de actualización en la tabla. Dentro del bloque `BEGIN-END` del `trigger`, se utiliza la instrucción `INSERT INTO` para insertar los datos del cambio en la tabla `ProductAudit`. Se utiliza la tabla especial `inserted` para obtener los nuevos valores de `UnitPrice` y la tabla especial `deleted` para obtener los valores antiguos de `UnitPrice`. Se realiza una comparación para determinar si ha habido un cambio en el precio y solo se insertan los registros modificados en la tabla `ProductAudit` junto con la fecha y hora del cambio.

Al implementar este `trigger`, cada vez que se realice una actualización en el campo `UnitPrice` de la tabla `Products`, se registrará automáticamente el cambio en la tabla `ProductAudit`. Esto proporciona un registro de auditoría que puede ser útil para fines de seguimiento y control.

En resumen, los `triggers` en SQL Server son herramientas poderosas que permiten automatizar acciones en respuesta a eventos específicos en una base de datos. Pueden ayudar a mantener la integridad de los datos, implementar reglas de negocio adicionales y generar registros de auditoría. Sin embargo, es importante utilizar los `triggers` con cuidado y considerar su impacto en el rendimiento de la base de datos, ya que pueden afectar el tiempo de ejecución de las operaciones.

[🔼](#índice)

---

| **Inicio**            | **atrás 13**                | **Siguiente 15**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./13_Consultas_SQL.md) | [⏩](./15_Consultas_SQL.md) |
