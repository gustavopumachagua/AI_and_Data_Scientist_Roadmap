| **Inicio**            | **atrás 11**                | **Siguiente 13**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./11_Consultas_SQL.md) | [⏩](./13_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                |
| ---------------------------------------------------------------------- |
| [111. Funciones LEFT y RIGHT](#111-funciones-left-y-right)             |
| [112. Función LEN](#112-función-len)                                   |
| [113. Funciones LOWER y UPPER](#113-funciones-lower-y-upper)           |
| [114. Función REPLACE](#114-función-replace)                           |
| [115. Función REPLICATE](#115-función-replicate)                       |
| [116. Funciones LTRIM y RTRIM](#116-funciones-ltrim-y-rtrim)           |
| [117. Función CONCAT](#117-función-concat)                             |
| [118. Función GETDATE y GETUTCDATE](#118-función-getdate-y-getutcdate) |
| [119. Función DATEADD](#119-función-dateadd)                           |
| [120. Función DATEDIFF](#120-función-datediff)                         |

---

# **Tutorial de SQL**

## **111. Funciones LEFT y RIGHT**

Las funciones `LEFT` y `RIGHT` en SQL Server son funciones de cadena que se utilizan para extraer una parte específica de una cadena de texto. La función `LEFT` devuelve un número específico de caracteres desde el lado izquierdo de la cadena, mientras que la función `RIGHT` devuelve un número específico de caracteres desde el lado derecho de la cadena.

Aquí tienes una explicación detallada de cada una de estas funciones, junto con ejemplos utilizando la base de datos Northwind:

1. **Función LEFT:**

La función `LEFT` se utiliza para extraer un número específico de caracteres desde el lado izquierdo de una cadena de texto. La sintaxis de la función `LEFT` es la siguiente:

`LEFT(cadena, longitud)`

- **cadena:** es la cadena de texto de la cual se extraerán los caracteres.
- **longitud:** es el número de caracteres que se extraerán desde el lado izquierdo de la cadena.

Ejemplo:

```
USE Northwind;
GO

SELECT LEFT(ContactName, 5) AS PrimerosCincoCaracteres
FROM Customers;
```

En este ejemplo, se utiliza la función `LEFT` para extraer los primeros cinco caracteres del campo "`ContactName`" en la tabla "`Customers`". Esto devolverá los primeros cinco caracteres de cada nombre de contacto en la tabla.

2. **Función RIGHT:**

La función `RIGHT` se utiliza para extraer un número específico de caracteres desde el lado derecho de una cadena de texto. La sintaxis de la función `RIGHT` es la siguiente:

`RIGHT(cadena, longitud)`

- **cadena:** es la cadena de texto de la cual se extraerán los caracteres.
- **longitud:** es el número de caracteres que se extraerán desde el lado derecho de la cadena.

Ejemplo:

```
USE Northwind;
GO

SELECT RIGHT(Phone, 4) AS UltimosCuatroDigitos
FROM Suppliers;
```

En este ejemplo, se utiliza la función `RIGHT` para extraer los últimos cuatro dígitos del campo "`Phone`" en la tabla "`Suppliers`". Esto devolverá los últimos cuatro dígitos de cada número de teléfono en la tabla.

Estas funciones son útiles cuando se necesita extraer una parte específica de una cadena de texto, como los primeros caracteres de un nombre o los últimos dígitos de un número de teléfono. Pueden ser utilizadas en las cláusulas `SELECT`, `WHERE` y otras cláusulas de consulta para manipular y filtrar datos de manera efectiva.

Es importante tener en cuenta que tanto la función `LEFT` como la función `RIGHT` trabajan con cadenas de texto y devuelven una nueva cadena con la parte extraída. La longitud especificada debe ser un valor numérico y debe estar dentro del rango de la longitud de la cadena original.

Recuerda que estas funciones están disponibles en SQL Server, pero pueden variar ligeramente en otros sistemas de gestión de bases de datos.

[🔼](#índice)

---

## **112. Función LEN**

La función `LEN` en SQL Server se utiliza para obtener la longitud (número de caracteres) de una cadena de texto. Esta función retorna un número entero que representa la cantidad de caracteres en la cadena.

Aquí tienes una explicación detallada de la función `LEN`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `LEN` es la siguiente:

`LEN(cadena)`

- **cadena:** es la cadena de texto de la cual se desea obtener la longitud.

Ejemplo:

```
USE Northwind;
GO

SELECT LEN(CompanyName) AS Longitud
FROM Customers;
```

En este ejemplo, se utiliza la función `LEN` para obtener la longitud del campo "`CompanyName`" en la tabla "`Customers`". Esto devolverá la cantidad de caracteres de cada nombre de la compañía en la tabla.

Es importante tener en cuenta que la función `LEN` solo cuenta los caracteres en una cadena de texto y no incluye espacios en blanco o caracteres especiales. Por ejemplo, si una cadena tiene un espacio al final, ese espacio no se contabiliza en la longitud.

La función `LEN` es útil en situaciones en las que necesitas conocer la longitud de una cadena de texto, como verificar si una columna cumple con una longitud máxima permitida o realizar cálculos basados en la longitud de los valores.

Recuerda que la función `LEN` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **113. Funciones LOWER y UPPER**

Las funciones `LOWER` y `UPPER` en SQL Server se utilizan para convertir el texto en minúsculas y mayúsculas, respectivamente. Estas funciones son útiles cuando se necesita normalizar o estandarizar el formato del texto almacenado en una base de datos.

Aquí tienes una explicación detallada de cada una de estas funciones, junto con ejemplos utilizando la base de datos Northwind:

1. **Función LOWER:**

La función `LOWER` se utiliza para convertir un texto en minúsculas. La sintaxis de la función `LOWER` es la siguiente:

`LOWER(cadena)`

- **cadena:** es la cadena de texto que se desea convertir a minúsculas.

Ejemplo:

```
USE Northwind;
GO

SELECT LOWER(ContactName) AS ContactoEnMinusculas
FROM Customers;
```

En este ejemplo, se utiliza la función `LOWER` para convertir el campo "`ContactName`" en minúsculas en la tabla "`Customers`". Esto devolverá el nombre de contacto en minúsculas para cada registro de la tabla.

2. **Función UPPER:**

La función `UPPER` se utiliza para convertir un texto en mayúsculas. La sintaxis de la función `UPPER` es la siguiente:

`UPPER(cadena)`

- **cadena:** es la cadena de texto que se desea convertir a mayúsculas.

Ejemplo:

```
USE Northwind;
GO

SELECT UPPER(City) AS CiudadEnMayusculas
FROM Customers;
```

En este ejemplo, se utiliza la función `UPPER` para convertir el campo "`City`" en mayúsculas en la tabla "`Customers`". Esto devolverá el nombre de la ciudad en mayúsculas para cada registro de la tabla.

Estas funciones son útiles cuando se necesita normalizar el formato del texto en una base de datos. Pueden ser utilizadas en las cláusulas `SELECT`, `WHERE` y otras cláusulas de consulta para manipular y comparar datos de manera efectiva, sin importar el formato original en el que se encuentren.

Es importante tener en cuenta que las funciones `LOWER` y `UPPER` solo afectan a los caracteres alfabéticos en una cadena de texto y no tienen ningún efecto en caracteres numéricos o especiales. Además, estas funciones son independientes del idioma y funcionarán correctamente en diferentes configuraciones regionales.

Recuerda que estas funciones están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **114. Función REPLACE**

La función `REPLACE` en SQL Server se utiliza para reemplazar todas las apariciones de una subcadena específica dentro de una cadena de texto por otra subcadena. Esta función es útil cuando se necesita modificar o corregir datos almacenados en una base de datos.

Aquí tienes una explicación detallada de la función `REPLACE`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `REPLACE` es la siguiente:

`REPLACE(cadena, subcadena_a_reemplazar, nueva_subcadena)`

- **cadena:** es la cadena de texto en la que se realizará el reemplazo.
- **subcadena_a_reemplazar:** es la subcadena que se buscará en la cadena para ser reemplazada.
- **nueva_subcadena:** es la subcadena que se utilizará como reemplazo.

Ejemplo:

```
USE Northwind;
GO

SELECT REPLACE(CompanyName, ' Inc.', ' Incorporated') AS CompaniaModificada
FROM Customers;
```

En este ejemplo, se utiliza la función `REPLACE` para reemplazar todas las apariciones de la subcadena " `Inc.`" en el campo "`CompanyName`" de la tabla "`Customers`" por la subcadena " `Incorporated`". Esto devolverá el nombre de la compañía modificado para cada registro de la tabla.

Es importante tener en cuenta que la función `REPLACE` realiza el reemplazo de manera sensible a mayúsculas y minúsculas. Esto significa que distingue entre mayúsculas y minúsculas al buscar la subcadena en la cadena original. Si se desea realizar un reemplazo insensible a mayúsculas y minúsculas, se pueden utilizar combinaciones de las funciones `UPPER` y `LOWER` junto con la función `REPLACE`.

La función `REPLACE` es útil cuando se necesita corregir o modificar datos almacenados en una base de datos. Puede ser utilizada en las cláusulas `SELECT`, `UPDATE` y otras cláusulas de consulta para realizar reemplazos en tiempo real y garantizar la integridad y precisión de los datos.

Recuerda que la función `REPLACE` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **115. Función REPLICATE**

La función `REPLICATE` en SQL Server se utiliza para repetir una cadena de texto un número determinado de veces. Esta función es útil cuando se necesita generar valores repetidos o rellenar campos con un patrón específico.

Aquí tienes una explicación detallada de la función `REPLICATE`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `REPLICATE` es la siguiente:

`REPLICATE(cadena, cantidad)`

- **cadena:** es la cadena de texto que se desea repetir.
- **cantidad:** es el número de veces que se desea repetir la cadena.

Ejemplo:

```
USE Northwind;
GO

SELECT REPLICATE('*', 10) AS Asteriscos
FROM Customers;
```

En este ejemplo, se utiliza la función `REPLICATE` para generar una cadena de texto que consiste en el carácter '`*`' repetido 10 veces. Esto devolverá una columna llamada "`Asteriscos`" con 10 asteriscos en cada fila de la tabla "`Customers`".

La función `REPLICATE` es especialmente útil cuando se combina con otras funciones y se utiliza en consultas o actualizaciones de datos. Por ejemplo, se puede utilizar para generar un número específico de espacios en blanco, completar campos con valores predeterminados o crear patrones repetitivos para generar datos de prueba.

Es importante tener en cuenta que la función `REPLICATE` no se limita a caracteres individuales y puede repetir cadenas de texto completas. Por lo tanto, se pueden generar patrones más complejos utilizando cadenas más largas.

Recuerda que la función `REPLICATE` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **116. Funciones LTRIM y RTRIM**

Las funciones `LTRIM` y `RTRIM` en SQL Server se utilizan para eliminar los espacios en blanco iniciales (`LTRIM`) y finales (`RTRIM`) de una cadena de texto, respectivamente. Estas funciones son útiles cuando se necesita limpiar y normalizar los valores almacenados en una base de datos.

Aquí tienes una explicación detallada de cada una de estas funciones, junto con ejemplos utilizando la base de datos Northwind:

1. **Función LTRIM:**

La función `LTRIM` se utiliza para eliminar los espacios en blanco iniciales de una cadena de texto. La sintaxis de la función `LTRIM` es la siguiente:

`LTRIM(cadena)`

- **cadena:** es la cadena de texto de la cual se eliminarán los espacios en blanco iniciales.

Ejemplo:

```
USE Northwind;
GO

SELECT LTRIM(ContactName) AS ContactoSinEspaciosIniciales
FROM Customers;
```

En este ejemplo, se utiliza la función `LTRIM` para eliminar los espacios en blanco iniciales del campo "`ContactName`" en la tabla "`Customers`". Esto devolverá el nombre de contacto sin espacios en blanco al principio para cada registro de la tabla.

2. **Función RTRIM:**

La función `RTRIM` se utiliza para eliminar los espacios en blanco finales de una cadena de texto. La sintaxis de la función `RTRIM` es la siguiente:

`RTRIM(cadena)`

- **cadena:** es la cadena de texto de la cual se eliminarán los espacios en blanco finales.

Ejemplo:

```
USE Northwind;
GO

SELECT RTRIM(ContactName) AS ContactoSinEspaciosFinales
FROM Customers;
```

En este ejemplo, se utiliza la función `RTRIM` para eliminar los espacios en blanco finales del campo "`ContactName`" en la tabla "`Customers`". Esto devolverá el nombre de contacto sin espacios en blanco al final para cada registro de la tabla.

Estas funciones son útiles cuando se necesita limpiar y normalizar los valores de las cadenas de texto en una base de datos. Pueden ser utilizadas en las cláusulas `SELECT`, `WHERE` y otras cláusulas de consulta para manipular y comparar datos de manera efectiva, sin considerar los espacios en blanco innecesarios.

Es importante tener en cuenta que las funciones `LTRIM` y `RTRIM` solo eliminan los espacios en blanco iniciales y finales de una cadena de texto. Si se desean eliminar los espacios en blanco en cualquier posición dentro de la cadena, se puede utilizar la función `REPLACE` junto con la función `LTRIM` o `RTRIM`.

Recuerda que estas funciones están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **117. Función CONCAT**

La función `CONCAT` en SQL Server se utiliza para concatenar o unir varias cadenas de texto en una sola cadena. Esta función es útil cuando se necesita combinar datos de diferentes columnas o constantes en una expresión de texto.

Aquí tienes una explicación detallada de la función `CONCAT`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `CONCAT` es la siguiente:

`CONCAT(valor1, valor2, ...)`

- **valor1, valor2, ...:** son los valores que se desean concatenar. Pueden ser columnas de la tabla, constantes o expresiones.

Ejemplo:

```
USE Northwind;
GO

SELECT CONCAT(FirstName, ' ', LastName) AS NombreCompleto
FROM Employees;
```

En este ejemplo, se utiliza la función `CONCAT` para combinar los valores de las columnas "`FirstName`" y "`LastName`" en la tabla "`Employees`" y generar una columna llamada "`NombreCompleto`" que contenga el nombre completo de cada empleado.

La función `CONCAT` permite concatenar múltiples valores en el orden especificado y no requiere ningún separador adicional entre los valores. En el ejemplo anterior, se utiliza un espacio en blanco entre las columnas "`FirstName`" y "`LastName`" para separar los nombres y apellidos en la cadena resultante.

Es importante tener en cuenta que la función `CONCAT` maneja automáticamente los valores `NULL` y los convierte en una cadena vacía. Esto significa que si alguno de los valores pasados a `CONCAT` es `NULL`, la función devolverá una cadena sin incluir ese valor `NULL`.

La función `CONCAT` es especialmente útil cuando se necesitan combinar datos de diferentes columnas en una única cadena, como en el ejemplo del nombre completo. También se puede utilizar para crear mensajes personalizados, generar identificadores únicos o construir consultas dinámicas.

Recuerda que la función `CONCAT` está disponible en SQL Server 2012 y versiones posteriores. Si estás utilizando una versión anterior, puedes utilizar la función de concatenación más antigua, que es el operador `+`. Sin embargo, la función `CONCAT` es preferible ya que proporciona un manejo más robusto de los valores `NULL` y tiene una sintaxis más clara.

[🔼](#índice)

---

## **118. Función GETDATE y GETUTCDATE**

La función `GETDATE` y `GETUTCDATE` en SQL Server se utilizan para obtener la fecha y hora actual en el sistema local y en el tiempo universal coordinado (UTC), respectivamente. Estas funciones son útiles para registrar la fecha y hora en que se realizan operaciones, realizar cálculos de tiempo y generar valores de fecha y hora en consultas.

Aquí tienes una explicación detallada de cada una de estas funciones, junto con ejemplos utilizando la base de datos Northwind:

1. **Función GETDATE:**

La función `GETDATE` se utiliza para obtener la fecha y hora actual en el sistema local. La sintaxis de la función `GETDATE` es la siguiente:

`GETDATE()`

Ejemplo:

```
USE Northwind;
GO

SELECT GETDATE() AS FechaYHoraLocal;
```

En este ejemplo, se utiliza la función `GETDATE` para obtener la fecha y hora actual del sistema local y se muestra en una columna llamada "`FechaYHoraLocal`".

2. **Función GETUTCDATE:**

La función `GETUTCDATE` se utiliza para obtener la fecha y hora actual en el tiempo universal coordinado (UTC). La sintaxis de la función `GETUTCDATE` es la siguiente:

`GETUTCDATE()`

Ejemplo:

```
USE Northwind;
GO

SELECT GETUTCDATE() AS FechaYHoraUTC;
```

En este ejemplo, se utiliza la función `GETUTCDATE` para obtener la fecha y hora actual en UTC y se muestra en una columna llamada "`FechaYHoraUTC`".

Es importante tener en cuenta que la función `GETDATE` devuelve la fecha y hora en la zona horaria del servidor SQL Server, que puede diferir de la zona horaria del cliente o del usuario. Si se necesita una consistencia en la zona horaria, se recomienda utilizar la función `GETUTCDATE` para obtener la fecha y hora en UTC y luego convertirla según sea necesario.

Estas funciones son útiles para registrar la fecha y hora en que se realizan operaciones en la base de datos, generar valores de fecha y hora en consultas y realizar cálculos de tiempo, como la diferencia entre dos fechas.

Recuerda que estas funciones están disponibles en SQL Server y son compatibles con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **119. Función DATEADD**

La función `DATEADD` en SQL Server se utiliza para agregar o restar una cantidad específica de tiempo a una fecha y hora determinada. Esta función es útil cuando se necesita calcular nuevas fechas basadas en una fecha de origen y un intervalo de tiempo determinado.

Aquí tienes una explicación detallada de la función `DATEADD`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `DATEADD` es la siguiente:

`DATEADD(intervalo, cantidad, fecha)`

- **intervalo:** es la unidad de tiempo que se desea agregar o restar. Puede ser uno de los siguientes valores: year, quarter, month, day, week, hour, minute, second, millisecond, microsecond o nanosecond.
- **cantidad:** es la cantidad de intervalos de tiempo que se desea agregar o restar. Puede ser un valor positivo para agregar tiempo o un valor negativo para restar tiempo.
- **fecha:** es la fecha y hora de origen a la cual se le agregarán o restarán intervalos de tiempo.

Ejemplo:

```
USE Northwind;
GO

SELECT DATEADD(day, 7, OrderDate) AS FechaEntrega
FROM Orders;
```

En este ejemplo, se utiliza la función `DATEADD` para agregar 7 días a la columna "`OrderDate`" en la tabla "`Orders`". Esto generará una columna llamada "`FechaEntrega`" que mostrará la fecha de entrega estimada de cada pedido, que es 7 días después de la fecha de pedido original.

La función `DATEADD` permite realizar cálculos avanzados de fechas y es especialmente útil cuando se necesitan generar fechas futuras o pasadas basadas en una fecha de origen y un intervalo de tiempo. Puedes utilizar diferentes unidades de tiempo, como días, meses, años, horas, minutos, etc., según tus necesidades.

Además, la función `DATEADD` es flexible y puede combinar diferentes intervalos de tiempo para realizar cálculos más complejos. Por ejemplo, puedes agregar años y meses a una fecha o sumar horas y minutos a una hora específica.

Recuerda que la función `DATEADD` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

## **120. Función DATEDIFF**

La función `DATEDIFF` en SQL Server se utiliza para calcular la diferencia entre dos fechas en una unidad de tiempo específica. Esta función es útil cuando se necesita determinar la cantidad de tiempo transcurrido entre dos fechas, como la diferencia en días, meses, años, horas, minutos, etc.

Aquí tienes una explicación detallada de la función `DATEDIFF`, junto con un ejemplo utilizando la base de datos Northwind:

La sintaxis de la función `DATEDIFF` es la siguiente:

`DATEDIFF(intervalo, fecha_inicio, fecha_fin)`

- \*\*intervalo: es la unidad de tiempo en la cual se desea calcular la diferencia entre las dos fechas. Puede ser uno de los siguientes valores: `year`, `quarter`, `month`, `day`, `week`, `hour`, `minute`, `second`, `millisecond`, `microsecond` o `nanosecond`.
- **fecha_inicio:** es la fecha y hora inicial del cálculo.
- **fecha_fin:** es la fecha y hora final del cálculo.

Ejemplo:

```
USE Northwind;
GO

SELECT DATEDIFF(day, OrderDate, ShippedDate) AS DiasTranscurridos
FROM Orders;
```

En este ejemplo, se utiliza la función `DATEDIFF` para calcular la diferencia en días entre las columnas "`OrderDate`" y "`ShippedDate`" en la tabla "`Orders`". Esto generará una columna llamada "`DiasTranscurridos`" que mostrará la cantidad de días que han pasado entre la fecha de pedido y la fecha de envío para cada pedido.

La función `DATEDIFF` permite calcular la diferencia entre dos fechas en diferentes unidades de tiempo, según las necesidades. Puedes obtener la diferencia en años, meses, días, horas, minutos, segundos, milisegundos, microsegundos o nanosegundos.

Es importante tener en cuenta que la función `DATEDIFF` devuelve un número entero que representa la diferencia en la unidad de tiempo especificada. Si necesitas una precisión fraccionaria, puedes utilizar otras funciones de fecha y hora para realizar cálculos más detallados.

Recuerda que la función `DATEDIFF` está disponible en SQL Server y es compatible con otros sistemas de gestión de bases de datos. Sin embargo, las funciones similares pueden tener nombres ligeramente diferentes en otros sistemas.

[🔼](#índice)

---

| **Inicio**            | **atrás 11**                | **Siguiente 13**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./11_Consultas_SQL.md) | [⏩](./13_Consultas_SQL.md) |
