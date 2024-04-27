| **Inicio**            | **atrás 16**                | **Siguiente 18**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./16_Consultas_SQL.md) | [⏩](./18_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                          |
| ------------------------------------------------------------------------------------------------ |
| [161. ¿Qué es SQL?](#161-¿qué-es-sql)                                                            |
| [162. Consultas con restricciones](#162-consultas-con-restricciones)                             |
| [163. Filtrar y Ordenar resultados de consultas](#163-filtrar-y-ordenar-resultados-de-consultas) |
| [164. Consultas de varias tablas con JOIN](#164-consultas-de-varias-tablas-con-join)             |
| [165. Consulta con Expresiones](#165-consulta-con-expresiones)                                   |
| [166. Consultas con agregados](#166-consultas-con-agregados)                                     |
| [167. Orden de ejecución de una consulta](#167-orden-de-ejecución-de-una-consulta)               |
| [168. Actualización de filas](#168-actualización-de-filas)                                       |
| [169. Modificación de tablas](#169-modificación-de-tablas)                                       |
| [170. Subconsultas](#170-subconsultas)                                                           |

---

# **Tutorial de SQL**

## **161. ¿Qué es SQL?**

SQL, o lenguaje de consulta estructurado, es un lenguaje diseñado para permitir a usuarios técnicos y no técnicos consultar, manipular y transformar datos de una base de datos relacional. Y debido a su simplicidad, las bases de datos SQL brindan almacenamiento seguro y escalable para millones de sitios web y aplicaciones móviles.

> **¿Sabías?**
>
> Existen muchas bases de datos SQL populares, incluidas SQLITE, MYSQL, Postgres, Oracle y Microsoft SQL Server. Todos ellos admiten el estándar de lenguaje SQL común, que es lo que enseñará este sitio, pero cada implementación puede diferir en las características adicionales y los tipos de almacenamiento que admite.

**Bases de datos relacionales**

Antes de aprender la sintaxis SQL, es importante tener un modelo de lo que realmente es una base de datos relacional. Una base de datos relacional representa una colección de tablas relacionadas (bidimensionales). Cada una de las tablas es similar a una hoja de cálculo de Excel, con un número fijo de columnas con nombre (los atributos o propiedades de la tabla) y cualquier número de filas de datos.

Por ejemplo, si el Departamento de Vehículos Motorizados tuviera una base de datos, podría encontrar una tabla que contenga todos los vehículos conocidos que conducen las personas en el estado. Es posible que esta tabla necesite almacenar el nombre del modelo, el tipo, la cantidad de ruedas y la cantidad de puertas de cada vehículo, por ejemplo.

**Tabla: Vehículos**

| **Identificación** | **Haz un Modelo** | **# Ruedas** | **# Puertas** | **Tipo**    |
| ------------------ | ----------------- | ------------ | ------------- | ----------- |
| 1                  | Ford Focus        | 4            | 4             | Sedán       |
| 2                  | Tesla Roadster    | 4            | 2             | Deportes    |
| 3                  | ninja kawakasi    | 2            | 0             | Motocicleta |
| 4                  | McLaren Fórmula 1 | 4            | 0             | Carrera     |
| 5                  | Tesla S           | 4            | 4             | Sedán       |

En dicha base de datos, puede encontrar tablas relacionadas adicionales que contienen información como una lista de todos los conductores registrados en el estado, los tipos de licencias de conducir que se pueden otorgar o incluso infracciones de tránsitos para cada conductor.

Al aprender SQL, el objetivo es aprender a responder preguntas específicas sobre estos datos, como "¿Qué tipos de vehículos hay en la carretera con menos de cuatro ruedas?" o "¿Cuántos modelos de automóviles produce Tesla?", para ayudarnos a tomar mejores decisiones en el futuro.

**Consultas SELECT**

Para recuperar datos de una base de datos SQL, necesitamos escribir **SELECT** declaraciones, a las que a menudo se hace referencia coloquialmente como consultas. Una consulta en sí misma es solo una declaración que declara qué datos estamos buscando, dónde encontrarlos en la base de datos y, opcionalmente, cómo transformarlos antes de que se devuelvan. Sin embargo, tiene una sintaxis específica, que es la que aprenderemos en los siguientes ejercicios.

Como mencionamos en la introducción, puede pensar en una tabla en SQL como un tipo de entidad (es decir, perros), y cada fila de esa tabla como una instancia específica de ese tipo (es decir, un pug, un beagle, un pug de diferentes colores, etc.). Esto significa que las columnas representarían las propiedades comunes compartidas por todas las instancias de esa entidad (es decir, color del pelaje, longitud de la cola, etc.).

y dada una tabla de datos, la consulta más básica que podríamos escribir sería una que seleccione un par de columnas (propiedades) de la tabla con todas las filas (instancias).

```
SELECT column, another_column, ........
FROM mytable;
```

El resultado de esta consulta será un conjunto bidimensional de filas y columnas, efectivamente una copia de la tabla, pero solo las columnas que solicitamos.

Si queremos recuperar absolutamente todas las columnas de datos de una tabla. podemos usar la \* taquigrafía asterisco () en lugar de enumerar todos los nombres de las columnas individualmente.

```
SELECT *
FROM mytable;
```

Esta consulta, en particular, es realmente útil porque es una forma sencilla de inspeccionar una tabla volcando todos a la vez.

**Ejercicio**

Usaremos una base de datos con datos sobre algunas de las películas clásicas de Pixar para la mayoría de nuestros ejercicios. Este primer ejercicio solo involucrará la tabla **Movies** y las consulta predeterminada a continuación muestra actualmente todas las propiedades de cada película. Para continuar con la siguiente lección, modifique la consulta para encontrar la informacion exacta que necesitamos para cada tarea.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

---

**Ejercicio 1: Tareas**

- **Encuentra el title de cada película.**

```
SELECT Title FROM Movies;
```

- **Encuentra el director de cada película.**

```
SELECT Director FROM Movies;
```

- **Encuentra el title y director de cada película.**

```
SELECT Title, Director FROM Movies;
```

- **Encuentra el title y year de cada película.**

```
SELECT Title, Year FROM Movies;
```

- **Encuentra all la información de cada película.**

```
SELECT * FROM Movies;
```

[🔼](#índice)

---

## **162. Consultas con restricciones**

Ahora sabemos cómo seleccionar columnas de datos específicas de una tabla, pero si tuviera una tabla con cien millones de filas de datos, leer todas las filas sería ineficiente y quizás incluso imposible.

Para evitar que se devuelvan ciertos resultados, necesitamos usar una **WHERE** cláusula en la consulta. La cláusula se aplica a cada fila de datos verificando valores de columna específicos para determinar si deben incluirse en los resultados o no.

```
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

Se pueden construir cláusulas más complejas uniendo numerosas palabras clave **AND** lógicas **OR** (es decir, num_wheels >= 4 AND puertas <=2). Y a continuación se muestran algunos operadores útiles que puede utilizar para datos numéricos (es decir, enteros o de punto flotante):

| **Operador**        | **Condición**                                                 | **Ejemplo de SQL**                        |
| ------------------- | ------------------------------------------------------------- | ----------------------------------------- |
| =, !=, < <=, >, >=  | Operadores numéricos estándar                                 | col_name != 4                             |
| BETWEEN … AND …     | El número está dentro del rango de dos valores (inclusive)    | (inclusive) col_name BETWEEN 1.5 AND 10.5 |
| NOT BETWEEN … AND … | El número no está dentro del rango de dos valores (inclusive) | col_name NOT BETWEEN 1 AND 10             |
| IN (…)              | El número existe en una lista.                                | col_name IN (2, 4, 6)                     |
| NOT IN (…)          | El número no existe en una lista                              | col_name NOT IN (1, 3, 5)                 |

Además de hacer que los resultados sean más fáciles de entender, escribir cláusulas para restringir el conjunto de filas devueltas también permite que la consulta se ejecute más rápido debido a la reducción de datos innecesarios que se devuelven.

> **¿Sabias?**
>
> Como ya habrás notado, SQL no requiere que escribas las palabras clave en mayúsculas, pero como convención, ayuda a las personas a distinguir las palabras clave SQL de los nombres de columnas y tablas, y hace que la consulta sea más fácil de leer.

**Ejercicio**

Usando las restricciones correctas, encuentre la información que necesitamos en la tabla **Movies** para cada tarea a continuación.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

---

**Ejercicio 2: Tareas**

- **Encuentra la película con una fila id de 6.**

```
SELECT Id, Title FROM Movies
WHERE Id = 6;
```

- **Encuentra las películas estrenadas en la year década de 2000 y 2010.**

```
SELECT Title, Year FROM Movies
WHERE Year BETWEEN 2000 AND 2010;
```

- **Encuentra las películas no estrenadas en la year década de 2000 y 2010.**

```
SELECT Title, Year FROM Movies
WHERE Year < 2000 OR Year > 2010;
```

- **Encuentra las primeras 5 películas de Pixar y su estreno year**

```
SELECT Title, Year FROM Movies
WHERE Year <= 2003;
```

**Consultas con restricciones**

Al escribir **WHERE** cláusulas con columnas que contienen datos de texto, SQL admiten una serie de operadores útiles para hacer cosas como la comparación de cadenas que no distingue entre mayúsculas y minúsculas y la coincidencia de patrones comodín. A continuación mostramos algunos operadores comunes específicos de datos de texto:

| **Operador** | **Condición**                                                                                                                 | **Ejemplo**                                                        |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| =            | Comparación de cadenas exactas que distinguen entre mayúsculas y minúsculas ( observe que el único es igual )                 | col_name = "abc"                                                   |
| != or <>     | Comparación de desigualdad de cadenas exactas que distingue entre mayúsculas y minúsculas                                     | col_name != "abcd"                                                 |
| LIKE         | Comparación de cadenas exactas que no distinguen entre mayúsculas y minúsculas                                                | col_name LIKE "ABCD"                                               |
| NOT LIKE     | Comparación de desigualdad de cadenas exactas que no distingue entre mayúsculas y minúsculas                                  | col_name NOT LIKE "ABCD"                                           |
| %            | Se usa en cualquier parte de una cadena para hacer coincidir una secuencia de cero o más caracteres (solo con LIKE o NO LIKE) | col_name LIKE "%AT%" (matches "AT", "ATTIC", "CAT" or even "BATS") |
| \_           | Se usa en cualquier parte de una cadena para que coincida con un solo carácter (solo con LIKE o NO LIKE)                      | col*name LIKE "AN*" (matches "AND", but not "AN")                  |
| IN (…)       | La cadena existe en una lista.                                                                                                | col_name IN ("A", "B", "C")                                        |
| NOT IN (…)   | La cadena no existe en una lista                                                                                              | col_name NOT IN ("D", "E", "F")                                    |

> **¿Sabías?**
>
> Todas las cadenas deben estar entre comillas para que el analizador de consultas pueda distinguir las palabras de la cadena de las palabras clave SQL.

Debemos tener en cuenta que, si bien la mayoría de las implementaciones de bases de datos son bastante eficientes cuando se utilizan estos operadores, es mejor dejar la búsqueda de texto completo en bibliotecas dedicadas como Apache Lucene o Sphinx. Estas bibliotecas están diseñadas específicamente para realizar búsquedas de texto completo y, como resultado, son más eficientes y pueden admitir una variedad más amplia de funciones de búsqueda, incluida la internacionalización y consultas avanzadas.

**Ejercicio**

Aquí está nuevamente la definición de una consulta con una **WHERE** cláusula, continúe e intente escribir algunas consultas con los operadores anteriores para limitar los resultados a la información que necesitamos en las tareas siguientes.

```
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

---

**Ejercicio 3: Tareas**

- **Encuentra todas las películas de Toy Story**

```SELECT Title, Director FROM Movies
WHERE Title LIKE "Toy Story%";
```

- **Encuentra todas las películas dirigidas por John Lasseter**

```
SELECT Title, Director FROM Movies
WHERE Director = "John Lasseter";
```

- **Encuentra todas las películas (y directores) no dirigidas por John Lasseter**

```
SELECT Title, Director FROM Movies
WHERE Director != "John Lasseter";
```

- **Encuentra todas las películas de WALL-**

```
SELECT * FROM Movies
WHERE Title LIKE "WALL-_";
```

[🔼](#índice)

---

## **163. Filtrar y Ordenar resultados de consultas**

Aunque los datos de una base de datos pueden ser únicos, los resultados de una consulta en particular pueden no serlo; tomemos nuestra tabla de Películas, por ejemplo, se pueden estrenar muchas películas diferentes el mismo año. En tales casos, SQL proporciona una manera conveniente de descartar filas que tienen un valor de columna duplicado nediante la **DISTINCT** palabra clave.

```
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

Dado que la **DISTINCT** palabra clave eliminará ciegamente filas duplicadas, en una lección futura aprenderemos cómo descartar duplicados en función de columnas específicas mediante la agrupación y la **GROUP BY** cláusula.

**Resultados del pedido**

A diferencia de nuestra tabla cuidadosamente ordenada de las últimas lecciones, la mayoría de los datos en bases de datos reales se agregan sin ningún orden de columnas en particular. Como resultado, puede resultar difícil leer y comprender los resultados de una consulta a medida que el tamaño de una tabla aumenta a miles o incluso millones de filas.

Para ayudar con esto, SQL proporciona una manera de ordenar los resultados por una columna determinada en orden ascendente o descendente utilizando la **ORDER BY** cláusula.

```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

Cuando **ORDER BY** se especifica una cláusula, cada fila se ordena alfanuméricamente según el valor de la columna especificada. En algunas bases de datos, también puede especificar una intercalación para ordenar mejor los datos que contienen texto internacional.

**Limitar los resultados a un subconjunto**

Otra cláusula que se usa comúnmente con la **ORDER BY** cláusula son las cláusulas **LIMIT** y **OFFSET**, que son una optimización útil para indicar a la base de datos el subconjunto de los resultados que le interesan.

Reducirá **LIMIT** el número de filas a devolver y el opcional **OFFSET** especificará desde dónde empezar a contar el número de filas.

```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

Si piensa en sitios web como Reddit o Pinterest, la página principal es una lista de enlaces ordenados por popularidad y tiempo, y cada página posterior puede representarse mediante
conjuntos de enlaces en diferentes posiciones en la base de datos. Al utilizar estas cláusulas, la base de datos puede ejecutar consultas de manera más rápida y eficiente al procesar y devolver solo el contenido solicitado.

> ¿Sabías?
>
> Si tiene curiosidad sobre cuándo se aplican **LIMIT** y **OFFSET** en relación con las otras partes de una consulta, generalmente se hacen al final después de que se hayan aplicado las otras cláusulas. Tocaremos más sobre esto en la lección 12: Orden de ejecución después de presentar algunas partes más de la consulta.

**Ejercicio**

Hay algunos conceptos en esta lección, pero todos son bastante sencillos de aplicar. Para darle vida a las cosas, hemos codificado la tabla **Películas** en el ejercicio para imitar mejor el tipo de datos que podría ver en la vida real. Intente utilizar las palabras clave y cláusulas necesarias presentadas anteriormente en sus consultas.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

---

**Ejercicio 4: Tareas**

- **Enumere todos los directores de las películas de Pixar (alfabéticamente), sin duplicados**

```
SELECT DISTINCT Director FROM Movies
ORDER BY director ASC;
```

- **Enumere las últimas cuatro películas de Pixar estrenadas (ordenadas de más reciente a menos)**

```
SELECT Title, Year FROM Movies
ORDER BY Year DESC
LIMIT 4;
```

- **Enumere las cinco primeras películas de Pixar ordenadas alfabéticamente**

```
SELECT Title FROM Movies
ORDER BY Title ASC
LIMIT 5;
```

- **Enumere las próximas cinco películas de Pixar ordenadas alfabéticamente**

```
SELECT Title FROM Movies
ORDER BY Title ASC
LIMIT 5 OFFSET 5;
```

**Revisión de SQL: Consultas SELECT simples**

Ahora que ha probado cómo escribir una consulta básica, necesita practicar la redacción de consultas que resulvan problemas reales.

```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

**Ejercicio**

En el siguiente ejercicio, trabajará con una tabla diferente. En cambio, esta tabla contiene información sobre algunas de las ciudades más pobladas de América del Norte, incluida su población y ubicación geoespacial en el mundo.

> ¿Sabías?
>
> Las latitudes positivas corresponden al hemisferio norte y las longitudes positivas corresponden al hemisferio oriental. Dado que América del Norte está al norte del ecuador y al oeste del primer meridiano, todas las ciudades de la lista tienen latitudes positivas y longitudes negativas.

Intente escribir algunas consultas para encontrar la información solicitada en las tareas que conoce. Es posible que debe utilizar una combinación diferente de cláusulas en su consulta para cada tarea. Una vez que haya terminado, continúe con la siguiente lección para aprender sobre consultas que abarcan varias tablas.

**Table: North_american_cities**

| **City**            | **Country**   | **Population** | **Latitude** | **Longitude** |
| ------------------- | ------------- | -------------- | ------------ | ------------- |
| Guadalajara         | Mexico        | 1500800        | 20.659699    | -103.349609   |
| Toronto             | Canada        | 2795060        | 43.653226    | -79.383184    |
| Houston             | United States | 2195914        | 29.760427    | -95.369803    |
| New York            | United States | 8405837        | 40.712784    | -74.005941    |
| Philadelphia        | United States | 1553165        | 39.952584    | -75.165222    |
| Havana              | Cuba          | 2106146        | 23.05407     | -82.345189    |
| Mexico City         | Mexico        | 8555500        | 19.432608    | -99.133208    |
| Phoenix             | United States | 1513367        | 33.448377    | -112.074037   |
| Los Angeles         | United States | 3884307        | 34.052234    | -118.243685   |
| Ecatepec de Morelos | Mexico        | 1742000        | 19.601841    | -99.050674    |
| Montreal            | Canada        | 1717767        | 45.501689    | -73.567256    |
| Chicago             | United States | 2718782        | 41.878114    | -87.629798    |

**Revisión 1: Tareas**

- **Lista todas las ciudades canadienses y sus poblaciones.**

```
SELECT city, population FROM north_american_cities
WHERE country = "Canada";
```

- **Ordene todas las ciudades de Estados Unidos por su latitud de norte a sur**

```
SELECT city, latitude FROM north_american_cities
WHERE country = "United States"
ORDER BY latitude DESC;
```

- **Enumere todas las ciudades al oeste de Chicago, ordenadas de oeste a este**

```
SELECT city, longitude FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude ASC;
```

- **Enumere las dos ciudades más grandes de México (por población)**

```
SELECT city, population FROM north_american_cities
WHERE country LIKE "Mexico"
ORDER BY population DESC
LIMIT 2;
```

- **Enumere la tercera y cuarta ciudad más grande (por población) de los Estados Unidos y su población.**

```
SELECT city, population FROM north_american_cities
WHERE country LIKE "United States"
ORDER BY population DESC
LIMIT 2 OFFSET 2;
```

[🔼](#índice)

---

## **164. Consultas de varias tablas con JOIN**

Hasta ahora, hemos estado trabajando con una sola tabla, pero los datos de entidades en el mundo real a menudo se dividen en partes y se almacenan en múltiples tablas ortogonales mediante un proceso conocido como normalización.

**Normalización de base de datos**

La normalización de la base de datos es útil porque minimiza los datos duplicados en cualquier tabla y permite que los datos de la base de datos crezcan independientemente unos de otros (es decir, los tipos de motores de automóviles oueden crecer independientemente de cada tipo de automóvil).

Como compensación, las consultas se vuelven un poco más complejas ya que deben poder encontrar datos de diferentes partes de la base de datos y pueden surgir problemas de rendimiento cuando se trabaja con muchas tablas grandes.

Para responder preguntas sobre una entidad que tiene datos que abarcan varias tablas en una base de datos normalizada, necesitamos aprender a escribir una consulta que pueda combinar todos esos datos y extraer exactamente la información que necesitamos.

**Consultas de varias tablas con JOIN**

Las tablas que comparten información sobre única entidad deben tener una clave principal que identifique esa entidad de forma única en toda la base de datos. Un tipo de clave principal común es un número entero que se incrementa automaticamente (porque ahorra espacio), pero también puede ser una cadena, un valor hash, siempre que sea único.

Al usar la **JOIN** clásusula en una consulta, podemos combinar datos de filas en dos tablas separadas usando esta clave única. La primera de las combinaciones que presentaremos es **INNER JOIN**.

```
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

Es **INNER JOIN** un proceso que hace coincidir filas de la primera tabla y la segunda tabla que tienen la misma clave (Según lo definido por la **ON** restricción) para crear una fila de resultado con las columnas combinadas de ambas tablas. Una vez unidas las tablas se aplican las demás cláusulas que aprendimos anteriormente.

![sql joins](../../img/sqljoin.jpeg "sql joins")

> ¿Sabías?
>
> Es posible que vea consultas en las que **INNER JOIN** esté escrito simplemente como **JOIN**. Estos dos son equivalentes, pero continuaremos refiriéndonos a estas uniones como uniones internas porque hacen que la consulta sea más fácil de leer una vez que comience a usar otros tipos de uniones que se presentarán en la siguiente lección.

**Ejercicio**

Hemos agregado una nueva tabla a la base de datos de Pixar que puedas intentar practicar algunas uniones. La tabla **BoxOffice** almacena información sobre las calificaciones y las ventas de cada película de Pixar en particular, y la columna **Movie_id** en esa tabla se corresponde con la columna **id** en la tabla películas 1 a 1. Intente resolver las siguientes tareas utilizando lo **INNER JOIN** presentado anteriormente.

**Table: Movies**

| **Id** | **Title**      | **Director**  | **Year** | **Length_minutes** |
| ------ | -------------- | ------------- | -------- | ------------------ |
| 1      | Toy Story      | John Lasseter | 1995     | 81                 |
| 2      | A Bug's Life   | John Lasseter | 1998     | 95                 |
| 3      | Toy Story 2    | John Lasseter | 1999     | 93                 |
| 4      | Monsters, Inc. | Pete Docter   | 2001     | 92                 |

**Table: Boxoffice**

| **Movie_id** | **Rating** | **Domestic_sales** | **International_sales** |
| ------------ | ---------- | ------------------ | ----------------------- |
| 5            | 8.2        | 380843261          | 555900000               |
| 14           | 7.4        | 268492764          | 475066843               |
| 8            | 8          | 206445654          | 417277164               |
| 12           | 6.4        | 191452396          | 368400000               |
| 3            | 7.9        | 245852179          | 239163000               |
| 6            | 8          | 261441092          | 370001000               |
| 9            | 8.5        | 223808164          | 297503696               |
| 11           | 8.4        | 415004880          | 648167031               |
| 1            | 8.3        | 191796233          | 170162503               |
| 7            | 7.2        | 244082982          | 217900167               |
| 10           | 8.3        | 293004164          | 438338580               |
| 4            | 8.1        | 289916256          | 272900000               |
| 2            | 7.2        | 162798565          | 200600000               |
| 13           | 7.2        | 237283207          | 3017                    |

**Ejercicio 6: Tareas**

- **Encuentra las ventas nacionales e internacionales de cada película.**

```
SELECT title, domestic_sales, international_sales
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;
```

- **Muestre las cifras de ventas de cada película que obtuvo mejores resultados a nivel internacional que a nivel nacional.**

```
SELECT title, domestic_sales, international_sales
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;
```

- **Enumere todas las películas por clasificación en orden descendente.**

```
SELECT title, rating
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id
ORDER BY rating DESC;
```

**Uniones Externas**

Dependiendo de cómo desee analizar los datos, la **INNER JOIN** lección que utilizamos la última lección podría no ser suficiente porque la tabla resultante solo contiene datos que pertenecen a ambas tablas.

Si las dos tablas tienen datos asimétricos, lo que puede suceder fácilemente cuando los datos se ingresan en diferentes etapas, entonces tendríamos que usar un **LEFT JOIN** en su lugar para asegurarnos de que los datos que necesita no queden fuera de los resultados. **RIGHT JOIN**, **FULL JOIN**.

```
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

Al igual que **INNER JOIN** estas tres nuevas uniones, deben especificar en qué columna unir los datos.

Al unir la tabla A con la tabla B, **LEFT JOIN** simplemente incluye filas de A independientemente de si se encuentra una fila coincidente en B. Es **RIGHT JOIN** lo mismo, pero al revés, manteniendo las filas en B independientemente de si se encuentra una coincidencia en A. Finalmente, a **FULL JOIN** simplemente significa que las filas de ambas tablas se mantienen, independientemente de si existe una fila coincidente en la otra tabla.

Cuando utilice cualquier de estas nievas uniones, probablemente tendrá que escribir lógica adicional para tratar con **NULL** en el resultado y las restricciones (más sobre esto en la próxima lección).

![JOIN'S](../../img/sqljoin.jpeg "JOIN'S")

> ¿Sabías?
>
> Es posib le que vea consultas con estas combinaciones escritas como **LEFT OUTER JOIN**, **RIGHT OUTER JOIN** o **FULL OUTER JOIN**, pero la **OUTER** palabra clave realmente se mantiene para compatibilidad con SQL-92 y estas consultas son simplemente equivalentes a **LEFT JOIN**, **RIGHT JOIN** y **FULL JOIN** respectivamente.

**Ejercicio**

En este ejercicio, trabajará con una nueva tabla que almacena datos ficticios sobre los empleados en el estudio de cine y sus edificios de oficinas asignados. Algunos de los edificios son nuevos, por lo que aún no tienen empleados, pero de todos modos necesitamos encontrar información sobre ellos.

Dado que la base de datos SQL de nuestro navegador es algo limitada, **LEFT JOIN** en el siguiente ejercicio solo se admite.

**Table: Buildings**

| **Building_name** | **Capacity** |
| ----------------- | ------------ |
| 1e                | 24           |
| 1w                | 32           |
| 2e                | 16           |
| 2w                | 20           |

**Table: Employees**

| **Role** | **Name**   | **Building** | **Years_employed** |
| -------- | ---------- | ------------ | ------------------ |
| Engineer | Becky A.   | 1e           | 4                  |
| Engineer | Dan B.     | 1e           | 2                  |
| Engineer | Sharon F.  | 1e           | 6                  |
| Engineer | Dan M.     | 1e           | 4                  |
| Engineer | Malcom S.  | 1e           | 1                  |
| Artist   | Tylar S.   | 2w           | 2                  |
| Artist   | Sherman D. | 2w           | 8                  |
| Artist   | Jakob J.   | 2w           | 6                  |
| Artist   | Lillia A.  | 2w           | 7                  |
| Artist   | Brandon J. | 2w           | 7                  |
| Manager  | Scott K.   | 1e           | 9                  |
| Manager  | Shirlee M. | 1e           | 3                  |
| Manager  | Daria O.   | 2w           | 6                  |

**Ejercicio 7: Tareas**

- **Encuentre la lista de todos los edificios que tienen empleados.**

```
SELECT DISTINCT building FROM employees;
```

- **Encuentra la lista de todos los edificios y su capacidad.**

```
SELECT * FROM buildings;
```

- **Enumere todos los edificios y las distintas funciones de los empleados en cada edificio (incluidos los edificios vacíos)**

```
SELECT DISTINCT building_name, role
FROM buildings
  LEFT JOIN employees
    ON building_name = building;
```

**Una breve nota sobre NULL**

Como prometimos en la última lección, hablaremos rápidamente sobre **NULL** los valores en una base de datos SQL. Siempre es bueno reducir la posibilidad de **NULL** valores en las bases de datos porque requieren atención especial al construir consultas, restricciones (ciertas funciones se comportan de manera diferente con valores nulos) y al procesar los resultados.

Una alternativa a **NULL** los valores en su base de datos es tener valores predeterminados apropiados para el tipo de datos, como 0 para datos numéricos, cadenas vacías para datos de texto, etc. Pero si su base de datos necesita almacenar datos incompletos, entonces los **NULL** valores pueden ser apropiados si los valores predeterminados sesgará el análisis posterior (por ejemplo, al tomar promedios de datos numéricos).

A veces, tampoco es posible evitar **NULL** valores, como vimos en la última lección al unir externamente dos tablas con datos asimétricos. En estos casos, puede probar los **NULL** valores de una columna en una **WHERE** cláusula utilizando la restricción **IS NULL** o **IS NOT NULL**.

```
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```

**Ejercicio**

Este ejercicio será una especie de repaso de las últimas lecciones. Estamos usando la misma tabla de Empleados y Edificios de la última lección, pero hemos contratado a algunos personas más, a quienes aún no se les ha asignado un edificio.

**Table: Buildings**

| **Building_name** | **Capacity** |
| ----------------- | ------------ |
| 1e                | 24           |
| 1w                | 32           |
| 2e                | 16           |
| 2w                | 20           |

**Table: Employees**

| **Role** | **Name**   | **Building** | **Years_employed** |
| -------- | ---------- | ------------ | ------------------ |
| Engineer | Becky A.   | 1e           | 4                  |
| Engineer | Dan B.     | 1e           | 2                  |
| Engineer | Sharon F.  | 1e           | 6                  |
| Engineer | Dan M.     | 1e           | 4                  |
| Engineer | Malcom S.  | 1e           | 1                  |
| Artist   | Tylar S.   | 2w           | 2                  |
| Artist   | Sherman D. | 2w           | 8                  |
| Artist   | Jakob J.   | 2w           | 6                  |
| Artist   | Lillia A.  | 2w           | 7                  |
| Artist   | Brandon J. | 2w           | 7                  |
| Manager  | Scott K.   | 1e           | 9                  |
| Manager  | Shirlee M. | 1e           | 3                  |
| Manager  | Daria O.   | 2w           | 6                  |
| Engineer | Yancy I.   |              | 0                  |
| Artist   | Oliver P.  |              | 0                  |

**Ejercicio 8: Tareas**

- **Encuentre el nombre y la función de todos los empleados que no han sido asignados a un edificio**

```
SELECT name, role FROM employees
WHERE building IS NULL;
```

- **Encuentre los nombres de los edificios que no tienen empleados.**

```
SELECT DISTINCT building_name
FROM buildings
  LEFT JOIN employees
    ON building_name = building
WHERE role IS NULL;
```

[🔼](#índice)

---

## **165. Consulta con Expresiones**

Además de consultar y hacer referencia a datos de columnas sin procesar con SQL, también puede usar expresiones para escribir una lógica más compleja en los valores de las columnas en una consulta. Estas expresiones pueden usar funciones matemáticas y de cadena junto con aritmética básica para transformar valores cuando se ejecuta la consulta, como se muestra en este ejemplo de física.

```
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```

Cada base de datos tiene su propio conjunto compatible de funciones matemáticas, de cadena y de fecha que se pueden usar en una consulta, que puede encontrar en sus respectivos documentos.

El uso de expresiones puede ahorrar tiempo y un posprocesamiento adicional de los datos del resultado, pero también puede hacer que la consulta sea más difícil de leer, por lo que recomendamos que cuando se utilizan expresiones en la parte de la consulta, también se les dé un alias **SELECT**
descriptivo. utilizando la palabra clave **AS**

```
SELECT col_expression AS expr_description, …
FROM mytable;
```

Además de las expresiones, las columnas normales e incluso las tablas también pueden tener alias para que sea más fácil hacer referencia a ellas en el resultadi y como parte de la simplificación de consultas más complejas.

```
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;
```

**Ejercicio**

Tendrás que usar expresiones para transformar los datos de BoxOffice en algo más fácil de entender para las siguientes tareas.

**Table: Movies**

| **Id** | **Title**      | **Director**  | **Year** | **Length_minutes** |
| ------ | -------------- | ------------- | -------- | ------------------ |
| 1      | Toy Story      | John Lasseter | 1995     | 81                 |
| 2      | A Bug's Life   | John Lasseter | 1998     | 95                 |
| 3      | Toy Story 2    | John Lasseter | 1999     | 93                 |
| 4      | Monsters, Inc. | Pete Docter   | 2001     | 92                 |

**Table: Boxoffice**

| **Movie_id** | **Rating** | **Domestic_sales** | **International_sales** |
| ------------ | ---------- | ------------------ | ----------------------- |
| 5            | 8.2        | 380843261          | 555900000               |
| 14           | 7.4        | 268492764          | 475066843               |
| 8            | 8          | 206445654          | 417277164               |
| 12           | 6.4        | 191452396          | 368400000               |
| 3            | 7.9        | 245852179          | 239163000               |
| 6            | 8          | 261441092          | 370001000               |
| 9            | 8.5        | 223808164          | 297503696               |
| 11           | 8.4        | 415004880          | 648167031               |
| 1            | 8.3        | 191796233          | 170162503               |
| 7            | 7.2        | 244082982          | 217900167               |
| 10           | 8.3        | 293004164          | 438338580               |
| 4            | 8.1        | 289916256          | 272900000               |
| 2            | 7.2        | 162798565          | 200600000               |
| 13           | 7.2        | 237283207          | 301700000               |

**Ejercicio 9: Tareas**

- **Enumere todas las películas y sus ventas combinadas en millones de dólares.**

```
SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;
```

- **Enumere todas las películas y sus calificaciones en porcentaje.**

```
SELECT title, rating * 10 AS rating_percent
FROM movies
  JOIN boxoffice
    ON movies.id = boxoffice.movie_id;
```

- **Enumere todas las películas que se estrenaron en años pares.**

```
SELECT title, year
FROM movies
WHERE year % 2 = 0;
```

[🔼](#índice)

---

## **166. Consultas con agregados**

Además de las expresiones simples que presentamos en la última lección, SQL también admite el uso de expresiones (o funciones) agregadas que le permiten resumir información sobre un grupo de filas de datos. Con la base de datos de Pixar que ha estado utilizando, se pueden utilizar funciones agregadas para responder preguntas como "¿Cuántas películas ha producido Pixar?" o "¿Cuál es la película de Pixar con mayor recaudación cada año?".

```
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression;
```

Sin una agrupación específica, cada función agregada se ejecutará en todo el conjunto de filas de resultados y devolverá un valor único. Y al igual que las expresiones normales, darle un alias a sus funciones agregadas garantiza que los resultados serán más fáciles de leer y procesar.

**Funciones agregadas comunes**

A continuación se muestran algunas funciones agregadas comunes que usaremos en nuestros ejemplos:

| **Función**              | **Descripción**                                                                                                                                                                                                             |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| COUNT(\*), COUNT(column) | Una función común que se utiliza para contar el número de filas del grupo si no se especifica ningún nombre de columna. De lo contrario, cuente el número de filas del grupo con valores no NULL en la columna especificada |
| MIN(column)              | Encuentra el valor numérico más pequeño en la columna especificada para todas las filas del grupo.                                                                                                                          |
| MAX(column)              | Encuentra el valor numérico más grande en la columna especificada para todas las filas del grupo.                                                                                                                           |
| AVG(column)              | Encuentra el valor numérico promedio en la columna especificada para todas las filas del grupo.                                                                                                                             |
| SUM(column)              | Encuentra la suma de todos los valores numéricos en la columna especificada para las filas del grupo.                                                                                                                       |

**Funciones agregadas agrupadas**

Además de agregar en todas las filas, puede aplicar las funciones agregadas a grupos individuales de datos dentro de ese grupo (es decir, ventas de taquilla para películas de comedia o de acción).

Esto crearía tantos resultados como grupos únicos definidos en la **GROUP BY** Cláusula.

```
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression
GROUP BY column;
```

La **Group BY** Cláusula funciona agrupando filas que tienen el mismo valor en la columna especificada.

**Ejercicio**

Para este ejercicio. vamos a trabajar con nuestra tabla Empleados. Observe cómo las filas de esta tabla tiene datos compartidos, lo que nos dará la oportunidad de utilizar funciones agregadas para resumir algunas métricas de alto nivel sobre los equipos. Adelante, inténtalo.

**Table: Employees**

| **Role** | **Name**   | **Building** | **Years_employed** |
| -------- | ---------- | ------------ | ------------------ |
| Engineer | Becky A.   | 1e           | 4                  |
| Engineer | Dan B.     | 1e           | 2                  |
| Engineer | Sharon F.  | 1e           | 6                  |
| Engineer | Dan M.     | 1e           | 4                  |
| Engineer | Malcom S.  | 1e           | 1                  |
| Artist   | Tylar S.   | 2w           | 2                  |
| Artist   | Sherman D. | 2w           | 8                  |
| Artist   | Jakob J.   | 2w           | 6                  |
| Artist   | Lillia A.  | 2w           | 7                  |
| Artist   | Brandon J. | 2w           | 7                  |
| Manager  | Scott K.   | 1e           | 9                  |
| Manager  | Shirlee M. | 1e           | 3                  |
| Manager  | Daria O.   | 2w           | 6                  |

**Ejercicio 10: Tareas**

- **Encuentre el tiempo más largo que un empleado ha estado en el estudio**

```
SELECT MAX(years_employed) as Max_years_employed
FROM employees;
```

- **Para cada puesto, encuentre el número promedio de años empleados por los empleados en ese puesto.**

```
SELECT role, AVG(years_employed) as Average_years_employed
FROM employees
GROUP BY role;
```

- **Encuentre el número total de años de empleados trabajados en cada edificio.**

```
SELECT building, SUM(years_employed) as Total_years_employed
FROM employees
GROUP BY building;
```

**Consultas con agregados**

Nuestras consultas se están volviendo bastante complejas, pero casi hemos presentado todas las partes importantes de una **SELECT** consulta. Una cosa que quizás hayas notado es que si la **GROUP BY** cláusula se ejecuta después de la **WHERE** cláusula (que filtra las filas que se van a agrupar), ¿cómo filtramos exactamente las filas agrupadas?

Afortunadamente, SQL nos permite hacer esto agregando una **HAVING** cláusula adicional que se usa específicamente con la **GROUP BY** cláusula para permitirnos filtrar filas agrupadas del conjunto de resultados.

```
SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHERE condition
GROUP BY column
HAVING group_condition;
```

Las **HAVING** restricciones de la cláusula se escriben de la misma manera que las **WHERE** restricciones de la cláusula y se aplican a las filas agrupadas. Con nuestros ejemplos, esto puede no parecer una construcción particularmente útil, pero si imagina datos millones de filas con diferentes propiedades, a menudo es necesario poder aplicar restricciones adicionales para entender rápidamente los datos.

> **¿Sabías?**
>
> Si no está utilizando la cláusula "GROUP BY", una simple cláusula "WHERE" será suficiente.

**Ejercicio**

Para este ejercicio, profundizará en los datos de los empleados en el estudio de cine. Piensa en las diferentes cláusulas que quieres para cada tarea.

**Table: Employees**

| **Role** | **Name**   | **Building** | **Years_employed** |
| -------- | ---------- | ------------ | ------------------ |
| Engineer | Becky A.   | 1e           | 4                  |
| Engineer | Dan B.     | 1e           | 2                  |
| Engineer | Sharon F.  | 1e           | 6                  |
| Engineer | Dan M.     | 1e           | 4                  |
| Engineer | Malcom S.  | 1e           | 1                  |
| Artist   | Tylar S.   | 2w           | 2                  |
| Artist   | Sherman D. | 2w           | 8                  |
| Artist   | Jakob J.   | 2w           | 6                  |
| Artist   | Lillia A.  | 2w           | 7                  |
| Artist   | Brandon J. | 2w           | 7                  |
| Manager  | Scott K.   | 1e           | 9                  |
| Manager  | Shirlee M. | 1e           | 3                  |
| Manager  | Daria O.   | 2w           | 6                  |

**Ejercicio 11: Tareas**

- **Encuentra la cantidad de artistas en el estudio (sin cláusula HAVING )**

```
SELECT role, COUNT(*) as Number_of_artists
FROM employees
WHERE role = "Artist";
```

- **Encuentre la cantidad de empleados de cada rol en el estudio.**

```
SELECT role, COUNT(*)
FROM employees
GROUP BY role;
```

- **Encuentre el número total de años empleados por todos los ingenieros.**

```
SELECT role, SUM(years_employed)
FROM employees
GROUP BY role
HAVING role = "Engineer";
```

[🔼](#índice)

---

## **167. Orden de ejecución de una consulta**

Ahora que tenemos una idea de todas las partes de una consulta, podemos hablar de cómo encajan todas en el contexto de una consulta completa.

```
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

Cada consulta comienza encontrando los datos que necesitamos en una base de datos y luego filtrándolos hasta convertirlos en algo que pueda procesarse y comprenderse lo más rápido posible. Debido a que cada parte de la consulta se ejecuta secuencialmente, es importante comprender el orden de ejecución para saber a qué resultados se puede acceder y dónde.

**Orden de ejecución de la consulta**

**1. FROM y JOINs**

La **FROM** cláusula y las subsiguientes **JOIN** se ejecutan primero para determinar el conjunto de datos de trabajo total que se está consultando. Esto incluye subconsultas en esta cláusula y puede provocar que se creen tablas temporales internas que contengan todas las columnas y filas de las tablas que se unen.

**2.WHERE**

Una vez que tenemos el conjunto total de datos de trabajo, las **WHERE** restricciones de primer paso se aplican a las filas individuales y las filas que no satisfacen la restricción se descartan. Cada una de las restricciones solo puede acceder a columnas directamente desde las tablas solicitadas en la **FROM** cláusula. Los alias en la **SELECT** parte de la consulta no son accesibles en la mayoría de las bases de datos, ya que pueden incluir expresiones que dependen de partes de la consulta que aún no se han ejecutado.

**3.GROUP BY**

Las filas restantes después **WHERE** de aplicar las restricciones se agrupan según valores comunes en la columna especificada en la **GROUP BY** cláusula. Como resultado de la agrupación, solo habrá tantas filas como valores únicos en esa columna. Implícitamente, esto significa que solo debería necesitar usar esto cuando tenga funciones agregadas en su consulta.

**4.HAVING**

Si la consulta tiene una **GROUP BY** cláusula, las restricciones de la **HAVING** cláusula se aplican a las filas agrupadas y se descartan las filas agrupadas que no satisfacen la restricción. Al igual que la **WHERE** cláusula, tampoco se puede acceder a los alias desde este paso en la mayoría de las bases de datos.

**5.SELECT**

**SELECT** Finalmente se calculan todas las expresiones de la parte de la consulta.

**6.DISTINCT**

**DISTINCT** De las filas restantes, se descartarán las filas con valores duplicados en la columna marcada como .

**7.ORDER BY**

Si la cláusula especifica un orden **ORDER BY**, las filas se ordenan según los datos especificados en orden ascendente o descendente. Dado que se han calculado todas las expresiones de la **SELECT** parte de la consulta, puede hacer referencia a los alias en esta cláusula.

**8. LIMIT/OFFSET**

Finalmente, las filas que quedan fuera del rango especificado por **LIMIT** y **OFFSET** se descartan, dejando el conjunto final de filas que se devolverá de la consulta.

**Conclusión**

No todas las consultas necesitan tener todas las partes que enumeramos anteriormente, pero una de las razones por las que SQL es tan flexible es que permite a los desarrolladores y analistas de datos manipular datos rápidamente sin tener que escribir código adicional, todo simplemente usando las cláusulas anteriores.

**Ejercicio**

Aquí terminan nuestras lecciones sobre **SELECT** consultas, ¡felicidades por llegar hasta aquí! Este ejercicio intentará poner a prueba su comprensión de las consultas, así que no se desanime si las encuentra desafiantes. Trata de dar lo mejor.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

**Table: Boxoffice**

| **Movie_id** | **Rating** | **Domestic_sales** | **International_sales** |
| ------------ | ---------- | ------------------ | ----------------------- |
| 5            | 8.2        | 380843261          | 555900000               |
| 14           | 7.4        | 268492764          | 475066843               |
| 8            | 8          | 206445654          | 417277164               |
| 12           | 6.4        | 191452396          | 368400000               |
| 3            | 7.9        | 245852179          | 239163000               |
| 6            | 8          | 261441092          | 370001000               |
| 9            | 8.5        | 223808164          | 297503696               |
| 11           | 8.4        | 415004880          | 648167031               |
| 1            | 8.3        | 191796233          | 170162503               |
| 7            | 7.2        | 244082982          | 217900167               |
| 10           | 8.3        | 293004164          | 438338580               |
| 4            | 8.1        | 289916256          | 272900000               |
| 2            | 7.2        | 162798565          | 200600000               |
| 13           | 7.2        | 237283207          | 301700000               |

**Ejercicio 12: Tareas**

- **Calcula el número de películas que ha dirigido cada director.**

```
SELECT director, COUNT(id) as Num_movies_directed
FROM movies
GROUP BY director;
```

- **Encuentre el total de ventas nacionales e internacionales que se pueden atribuir a cada director.**

```
SELECT director, SUM(domestic_sales + international_sales) as Cumulative_sales_from_all_movies
FROM movies
    INNER JOIN boxoffice
        ON movies.id = boxoffice.movie_id
GROUP BY director;
```

**Insertar filas**

Hemos dedicado bastantes lecciones sobre cómo consultar datos en una base de datos, por lo que es hora de comenzar a aprender un poco sobre esquemas SQL y cómo agregar nuevos datos.

**¿Qué es un esquema?**

Anteriormente describimos una tabla en una base de datos como un conjunto bidimensional de filas y columnas, donde las columnas son las propiedades y las filas son instancias de la entidad en la tabla. En SQL, el esquema de la base de datos es lo que describe la estructura de cada tabla y los tipos de datos que puede contener cada columna de la tabla.

**Ejemplo: subconsulta correlacionada**

Por ejemplo, en nuestra tabla Películas , los valores de la columna Año deben ser un número entero y los valores de la columna Título deben ser una cadena.

Esta estructura fija es lo que permite que una base de datos sea eficiente y consistente a pesar de almacenar millones o incluso miles de millones de filas.

**Insertando nuevos datos**

Al insertar datos en una base de datos, necesitamos usar una **INSERT** declaración que declare en qué tabla escribir, las columnas de datos que estamos completando y una o más filas de datos a insertar. En general, cada fila de datos que inserte debe contener valores para cada columna correspondiente de la tabla. Puede insertar varias filas a la vez simplemente enumerándolas secuencialmente.

```
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;

```

En algunos casos, si tiene datos incompletos y la tabla contiene columnas que admiten valores predeterminados, puede insertar filas solo con las columnas de datos que tiene especificándolas explícitamente.

```
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),
      …;

```

En estos casos, la cantidad de valores debe coincidir con la cantidad de columnas especificadas. A pesar de que se trata de una declaración más detallada de escribir, insertar valores de esta manera tiene la ventaja de ser compatible con versiones posteriores. Por ejemplo, si agrega una nueva columna a la tabla con un valor predeterminado, no **INSERT** será necesario cambiar ninguna declaración codificada para adaptarse a ese cambio.

Además, puedes utilizar expresiones matemáticas y de cadena con los valores que vayas insertando.
Esto puede resultar útil para garantizar que todos los datos insertados tengan un formato determinado.

```
INSERT INTO boxoffice
(movie_id, rating, sales_in_millions)
VALUES (1, 9.9, 283742034 / 1000000);
```

**Ejercicio**

En este ejercicio, jugaremos como ejecutivos de estudio y agregaremos algunas películas a Películas de nuestro portafolio. En esta tabla, el **ID** es un número entero que se incrementa automáticamente, por lo que puede intentar insertar una fila solo con las otras columnas definidas.

Dado que las siguientes lecciones modificarán la base de datos, tendrás que ejecutar manualmente cada consulta una vez que estén listas.

**Table: Movies**

| **Id** | **Title**    | **Director**  | **Year** | **Length_minutes** |
| ------ | ------------ | ------------- | -------- | ------------------ |
| 1      | Toy Story    | John Lasseter | 1995     | 81                 |
| 2      | A Bug's Life | John Lasseter | 1998     | 95                 |
| 3      | Toy Story 2  | John Lasseter | 1999     | 93                 |

**Table: Boxoffice**

| **Movie_id** | **Rating** | **Domestic_sales** | **International_sales** |
| ------------ | ---------- | ------------------ | ----------------------- |
| 3            | 7.9        | 245852179          | 239163000               |
| 1            | 8.3        | 191796233          | 170162503               |
| 2            | 7.2        | 162798565          | 200600000               |

**Ejercicio 13: Tareas**

- **Agrega la nueva producción del estudio, Toy Story 4 a la lista de películas (puedes usar cualquier director)**

```
INSERT INTO movies VALUES (4, "Toy Story 4", "El Directore", 2015, 90);
```

- **¡Toy Story 4 ha sido lanzado con gran éxito de crítica! Tenía una calificación de 8,7 y ganó 340 millones a nivel nacional y 270 millones a nivel internacional . Agregue el registro a la BoxOfficetabla.**

```
INSERT INTO boxoffice VALUES (4, 8.7, 340000000, 270000000);
```

[🔼](#índice)

---

## **168. Actualización de filas**

Además de agregar nuevos datos, una tarea común es actualizar los datos existentes, lo que se puede hacer mediante una **UPDATE** declaración. De manera similar a la **INSERT** declaración, debe especificar exactamente qué tabla, columnas y filas actualizar. Además, los datos que está actualizando deben coincidir con el tipo de datos de las columnas del esquema de la tabla.

```
UPDATE mytable
SET column = value_or_expr,
    other_column = another_value_or_expr,
    …
WHERE condition;
```

La declaración funciona tomando múltiples pares de columna/valor y aplicando esos cambios a todas y cada una de las filas que satisfacen la restricción de la **WHERE** cláusula.

**Teniendo cuidado**

La mayoría de las personas que trabajan con SQL cometerán errores al actualizar los datos en un momento u otro. Ya sea que se trate de actualizar el conjunto incorrecto de filas en una base de datos de producción o de omitir accidentalmente la **WHERE** cláusula (lo que hace que la actualización se aplique a todas las filas), debe tener mucho cuidado al construir **UPDATE** declaraciones.

Un consejo útil es escribir siempre la restricción primero y probarla en una **SELECT** consulta para asegurarse de que está actualizando las filas correctas, y solo luego escribir los pares de columna/valor para actualizar.

**Ejercicio**

Parece que parte de la información de nuestra base de datos de películas puede ser incorrecta, así que continúa y corrígela mediante los ejercicios siguientes.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | El Directore   | 1998 95  |
| 3      | Toy Story 2         | John Lasseter  | 1899     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 8         | El Directore   | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

**Ejercicio 14: Tareas**

- **El director de Bichos está equivocado, en realidad fue dirigida por John Lasseter**

```
UPDATE movies
SET director = "John Lasseter"
WHERE id = 2;
```

- **El año en que se lanzó Toy Story 2 es incorrecto, en realidad se lanzó en 1999.**

```
UPDATE movies
SET year = 1999
WHERE id = 3;
```

- **¡Tanto el título como el director de Toy Story 8 son incorrectos! El título debería ser "Toy Story 3" y fue dirigida por Lee Unkrich**

```
UPDATE movies
SET title = "Toy Story 3", director = "Lee Unkrich"
WHERE id = 11;
```

**Eliminar filas**

Cuando necesite eliminar datos de una tabla en la base de datos, puede utilizar una **DELETE** declaración que describa la tabla sobre la que actuar y las filas de la tabla que eliminará a través de la **WHERE** cláusula.

```
DELETE FROM mytable
WHERE condition;
```

Si decide omitir la **WHERE** restricción, se eliminan todas las filas, lo cual es una manera rápida y fácil de borrar una tabla por completo (si es intencional).

**Teniendo mucho cuidado**

Al igual que la **UPDATE** declaración de la lección anterior, se recomienda ejecutar **SELECT** primero la restricción en una consulta para asegurarse de eliminar las filas correctas. Sin una copia de seguridad o una base de datos de prueba adecuada, es muy fácil eliminar datos irrevocablemente, así que siempre lea sus **DELETE** declaraciones dos veces y ejecútelas una vez.

**Ejercicio**

Es necesario limpiar un poco la base de datos, así que intente eliminar algunas filas en las tareas siguientes.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

**Ejercicio 15: Tareas**

- **Esta base de datos se está volviendo demasiado grande, eliminemos todas las películas que se estrenaron antes de 2005.**

```
DELETE FROM movies
where year < 2005;
```

- **Andrew Stanton también dejó el estudio, así que elimine todas las películas dirigidas por él.**

```
DELETE FROM movies
where director = "Andrew Stanton";
```

**Crear tablas**

Cuando tenga nuevas entidades y relaciones para almacenar en su base de datos, puede crear una nueva tabla de base de datos usando la **CREATE TABLE** declaración.

```
CREATE TABLE IF NOT EXISTS mytable (
    column DataType TableConstraint DEFAULT default_value,
    another_column DataType TableConstraint DEFAULT default_value,
    …
);
```

La estructura de la nueva tabla está definida por su esquema de tabla , que define una serie de columnas. Cada columna tiene un nombre, el tipo de datos permitidos en esa columna, una restricción de tabla opcional sobre los valores que se insertan y un valor predeterminado opcional.

Si ya existe una tabla con el mismo nombre, la implementación de SQL generalmente arrojará un error, por lo que para suprimir el error y omitir la creación de una tabla, si existe, puede usar la **IF NOT EXISTS** cláusula.

**Tipos de datos de tabla**

Diferentes bases de datos admiten diferentes tipos de datos, pero los tipos comunes admiten números, cadenas y otras cosas diversas como fechas, valores booleanos o incluso datos binarios. A continuación se muestran algunos ejemplos que podría utilizar en código real.

| **Tipo de datos**                              | **Descripción**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| INTEGER, BOOLEAN                               | Los tipos de datos enteros pueden almacenar valores enteros completos como el recuento de un número o una edad. En algunas implementaciones, el valor booleano simplemente se representa como un valor entero de solo 0 o 1.                                                                                                                                                                                                                                                                                 |
| FLOAT, DOUBLE, REAL                            | Los tipos de datos de punto flotante pueden almacenar datos numéricos más precisos, como mediciones o valores fraccionarios. Se pueden utilizar diferentes tipos dependiendo de la precisión de coma flotante requerida para ese valor.                                                                                                                                                                                                                                                                      |
| CHARACTER(num_chars), VARCHAR(num_chars), TEXT | Los tipos de datos basados ​​en texto pueden almacenar cadenas y texto en todo tipo de configuraciones regionales. La distinción entre los distintos tipos suele contribuir a la eficiencia de la base de datos al trabajar con estas columnas. Tanto el tipo CHARACTER como el VARCHAR (carácter variable) se especifican con la cantidad máxima de caracteres que pueden almacenar (los valores más largos pueden truncarse), por lo que puede ser más eficiente almacenar y consultar con tablas grandes. |
| DATE, DATETIME                                 | SQL también puede almacenar marcas de fecha y hora para realizar un seguimiento de series temporales y datos de eventos. Puede resultar complicado trabajar con ellos, especialmente cuando se manipulan datos en zonas horarias.                                                                                                                                                                                                                                                                            |
| BLOB                                           | Finalmente, SQL puede almacenar datos binarios en blobs directamente en la base de datos. Estos valores suelen ser opacos para la base de datos, por lo que normalmente hay que almacenarlos con los metadatos correctos para volver a consultarlos.                                                                                                                                                                                                                                                         |

**restricciones de tabla**

No vamos a profundizar demasiado en las restricciones de la tabla en esta lección, pero cada columna puede tener restricciones de tabla adicionales que limitan los valores que se pueden insertar en esa columna. Esta no es una lista completa, pero mostrará algunas restricciones comunes que pueden resultarle útiles.

| **Restricción**    | **Descripción**                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PRIMARY KEY        | Esto significa que los valores de esta columna son únicos y cada valor se puede utilizar para identificar una sola fila en esta tabla.                                                                                                                                                                                                                                                                                 |
| AUTOINCREMENT      | Para valores enteros, esto significa que el valor se completa e incrementa automáticamente con cada inserción de fila. No es compatible con todas las bases de datos.                                                                                                                                                                                                                                                  |
| UNIQUE             | Esto significa que los valores de esta columna deben ser únicos, por lo que no puede insertar otra fila con el mismo valor en esta columna que otra fila de la tabla. Se diferencia de la `CLAVE PRIMARIA` en que no tiene que ser una clave para una fila de la tabla.                                                                                                                                                |
| NOT NULL           | Esto significa que el valor insertado no puede ser "NULL".                                                                                                                                                                                                                                                                                                                                                             |
| CHECK (expression) | Esto le permite ejecutar una expresión más compleja para probar si los valores insertados son válidos. Por ejemplo, puedes comprobar que los valores sean positivos, o mayores que un tamaño específico, o que comiencen con un prefijo determinado, etc.                                                                                                                                                              |
| FOREIGN KEY        | Se trata de una comprobación de coherencia que garantiza que cada valor de esta columna corresponda a otro valor de una columna de otra tabla. Por ejemplo, si hay dos tablas, una que enumera a todos los empleados por ID y otra que enumera su información de nómina, la "LLAVE EXTRANJERA" puede garantizar que cada fila de la tabla de nómina corresponda a un empleado válido en la lista maestra de empleados. |

**Un ejemplo**

A continuación se muestra un esquema de ejemplo para la tabla Películas que hemos estado usando en las lecciones hasta ahora.

```
CREATE TABLE movies (
    id INTEGER PRIMARY KEY,
    title TEXT,
    director TEXT,
    year INTEGER,
    length_minutes INTEGER
);
```

**Ejercicio**

En este ejercicio, necesitará crear una nueva tabla en la que podamos insertar algunas filas nuevas.

```
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);
```

**Ejercicio 16: Tareas**

Cree una nueva tabla nombrada Databasecon las siguientes columnas:
– NameUna cadena (texto) que describe el nombre de la base de datos
– VersionUn número (punto flotante) de la última versión de esta base de datos
– Download_countUn recuento entero del número de veces que se descargó esta base de datos
Esta tabla no tiene restricciones.

[🔼](#índice)

---

## **169. Modificación de tablas**

A medida que sus datos cambian con el tiempo, SQL le proporciona una manera de actualizar sus tablas y esquemas de bases de datos correspondientes utilizando la **ALTER TABLE** declaración para agregar, eliminar o modificar columnas y restricciones de tablas.

**Agregar columnas**

La sintaxis para agregar una nueva columna es similar a la sintaxis al crear nuevas filas en la **CREATE TABLE** declaración. Debe especificar el tipo de datos de la columna junto con las posibles restricciones de la tabla y los valores predeterminados que se aplicarán tanto a las filas existentes como a las nuevas. En algunas bases de datos como MySQL, incluso puedes especificar dónde insertar la nueva columna usando las cláusulas **FIRST** o **AFTER**, aunque esta no es una característica estándar.

```
ALTER TABLE mytable
ADD column DataType OptionalTableConstraint
    DEFAULT default_value;
```

**Eliminando columnas**

Eliminar columnas es tan fácil como especificar la columna que se eliminará; sin embargo, algunas bases de datos (incluida SQLite) no admiten esta función. En su lugar, es posible que tengas que crear una nueva tabla y migrar los datos.

```
ALTER TABLE mytable
DROP column_to_be_deleted;
```

**Cambiar el nombre de la tabla**

Si necesita cambiar el nombre de la tabla, también puede hacerlo utilizando la **RENAME TO** cláusula de la declaración.

```
ALTER TABLE mytable
RENAME TO new_table_name;
```

**Otros cambios**

Cada implementación de base de datos admite diferentes métodos para alterar sus tablas, por lo que siempre es mejor consultar los documentos de su base de datos antes de continuar: MySQL , Postgres , SQLite , Microsoft SQL Server .

**Ejercicio**

Nuestros ejercicios utilizan una implementación que solo admite la adición de nuevas columnas, así que pruébelo a continuación.

**Table: Movies**

| **Id** | **Title**           | **Director**       | **Year** | **Length_minutes** |
| ------ | ------------------- | ------------------ | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter      | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter      | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter      | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter        | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton     | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird          | 2004     | 116                |
| 7      | Cars                | John Lasseter      | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird          | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton     | 2008     | 104                |
| 10     | Up                  | Pete Docter        | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich        | 2010     | 103                |
| 12     | Cars 2              | John Lasseter 2011 | 120      |
| 13     | Brave               | Brenda Chapman     | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon        | 2013     | 110                |

**Ejercicio 17: Tareas**

- **Agregue una columna llamada Aspect_ratio con un tipo de datos FLOAT para almacenar la relación de aspecto en la que se lanzó cada película.**

```
ALTER TABLE Movies
  ADD COLUMN Aspect_ratio FLOAT DEFAULT 2.39;
```

- **Agregue otra columna denominada Idioma con un tipo de datos TEXTO para almacenar el idioma en el que se estrenó la película. Asegúrese de que el idioma predeterminado para este idioma sea el inglés.**

```
ALTER TABLE Movies
  ADD COLUMN Language TEXT DEFAULT "English";
```

**Eliminación de tablas**

En algunos casos excepcionales, es posible que desee eliminar una tabla completa, incluidos todos sus datos y metadatos, y para hacerlo, puede usar la **DROP TABLE** declaración, que difiere de la **DELETE** declaración en que también elimina por completo el esquema de la tabla de la base de datos.

```
DROP TABLE IF EXISTS mytable;
```

Al igual que la **CREATE TABLE** declaración, la base de datos puede generar un error si la tabla especificada no existe y, para suprimir ese error, puede utilizar la **IF EXISTS** cláusula.

Además, si tiene otra tabla que depende de las columnas de la tabla que está eliminando (por ejemplo, con una **FOREIGN KEY** dependencia), primero tendrá que actualizar todas las tablas dependientes para eliminar las filas dependientes o eliminar esas tablas por completo.

**Ejercicio**

Hemos llegado al final de nuestros ejercicios, así que vamos a limpiar eliminando todas las tablas con las que hemos trabajado.

**Table: Movies**

| **Id** | **Title**           | **Director**   | **Year** | **Length_minutes** |
| ------ | ------------------- | -------------- | -------- | ------------------ |
| 1      | Toy Story           | John Lasseter  | 1995     | 81                 |
| 2      | A Bug's Life        | John Lasseter  | 1998     | 95                 |
| 3      | Toy Story 2         | John Lasseter  | 1999     | 93                 |
| 4      | Monsters, Inc.      | Pete Docter    | 2001     | 92                 |
| 5      | Finding Nemo        | Andrew Stanton | 2003     | 107                |
| 6      | The Incredibles     | Brad Bird      | 2004     | 116                |
| 7      | Cars                | John Lasseter  | 2006     | 117                |
| 8      | Ratatouille         | Brad Bird      | 2007     | 115                |
| 9      | WALL-E              | Andrew Stanton | 2008     | 104                |
| 10     | Up                  | Pete Docter    | 2009     | 101                |
| 11     | Toy Story 3         | Lee Unkrich    | 2010     | 103                |
| 12     | Cars 2              | John Lasseter  | 2011     | 120                |
| 13     | Brave               | Brenda Chapman | 2012     | 102                |
| 14     | Monsters University | Dan Scanlon    | 2013     | 110                |

**Table: Boxoffice**

| **Movie_id** | **Rating** | **Domestic_sales** | **International_sales** |
| ------------ | ---------- | ------------------ | ----------------------- |
| 5            | 8.2        | 380843261          | 555900000               |
| 14           | 7.4        | 268492764          | 475066843               |
| 8            | 8          | 206445654          | 417277164               |
| 12           | 6.4        | 191452396          | 368400000               |
| 3            | 7.9        | 245852179          | 239163000               |
| 6            | 8          | 261441092          | 370001000               |
| 9            | 8.5        | 223808164          | 297503696               |
| 11           | 8.4        | 415004880          | 648167031               |
| 1            | 8.3        | 191796233          | 170162503               |
| 7            | 7.2        | 244082982          | 217900167               |
| 10           | 8.3        | 293004164          | 438338580               |
| 4            | 8.1        | 289916256          | 272900000               |
| 2            | 7.2        | 162798565          | 200600000               |
| 13           | 7.2        | 237283207          | 301700000               |

**Ejercicio 18: Tareas**

- **Lamentablemente, hemos llegado al final de nuestras lecciones. Limpiemos eliminando la tabla de Películas.**

```
DROP TABLE Movies;
```

- **Y suelte la mesa de BoxOffice también.**

```
DROP TABLE BoxOffice;
```

[🔼](#índice)

---

## **170. Subconsultas**

Es posible que haya notado que incluso con una consulta completa, hay muchas preguntas que no podemos responder sobre nuestros datos sin una publicación o procesamiento previo adicional. En estos casos, puede realizar varias consultas y procesar los datos usted mismo, o puede crear una consulta más compleja utilizando subconsultas SQL.

**Ejemplo: subconsulta general**

Digamos que su empresa tiene una lista de todos los Asociados de Ventas, con datos sobre los ingresos que genera cada Asociado y su salario individual. Los tiempos son difíciles y ahora desea saber cuáles de sus Asociados le están costando a la empresa más que el ingreso promedio generado por Asociado.

Primero, necesitaría calcular los ingresos promedio que generan todos los Asociados:

```
SELECT AVG(revenue_generated)
FROM sales_associates;
```

Y luego, usando ese resultado, podemos comparar los costos de cada uno de los Asociados con ese valor. Para usarlo como subconsulta, podemos escribirlo directamente en la **WHERE** cláusula de la consulta:

```
SELECT *
FROM sales_associates
WHERE salary >
   (SELECT AVG(revenue_generated)
    FROM sales_associates);
```

A medida que se ejecuta la restricción, el salario de cada Asociado se comparará con el valor consultado en la subconsulta interna.

Se puede hacer referencia a una subconsulta en cualquier lugar donde se pueda hacer referencia a una tabla normal. Dentro de una **FROM** cláusula, puede realizar **JOIN** subconsultas con otras tablas, dentro de una restricción **WHERE** o **HAVING**, puede probar expresiones con los resultados de la subconsulta, e incluso en expresiones de la **SELECT** cláusula, que le permiten devolver datos directamente desde la subconsulta. Generalmente se ejecutan en el mismo orden lógico que la parte de la consulta en la que aparecen, como se describió en la última lección.

Debido a que las subconsultas se pueden anidar, cada subconsulta debe estar completamente entre paréntesis para establecer la jerarquía adecuada. De lo contrario, las subconsultas pueden hacer referencia a cualquier tabla de la base de datos y hacer uso de las construcciones de una consulta normal (aunque algunas implementaciones no permiten que las subconsultas utilicen **LIMIT** o **OFFSET**).

**Subconsultas correlacionadas**

Un tipo de subconsulta más potente es la subconsulta correlacionada en la que la consulta interna hace referencia a una columna o alias de la consulta externa y depende de ella. A diferencia de las subconsultas anteriores, cada una de estas consultas internas debe ejecutarse para cada una de las filas de la consulta externa, ya que la consulta interna depende de la fila de consulta externa actual.

**Ejemplo: subconsulta correlacionada**

En lugar de la lista anterior solo de Asociados de Ventas, imagine si tiene una lista general de Empleados, sus departamentos (ingeniería, ventas, etc.), ingresos y salario. Esta vez, está buscando en toda la empresa los empleados que se desempeñan peor que el promedio en su departamento.

Para cada empleado, deberá calcular su costo en relación con los ingresos promedio generados por todas las personas de su departamento. Para tomar el promedio del departamento, la subconsulta necesitará saber en qué departamento se encuentra cada empleado:

```
SELECT *
FROM employees
WHERE salary >
   (SELECT AVG(revenue_generated)
    FROM employees AS dept_employees
    WHERE dept_employees.department = employees.department);
```

Este tipo de consultas complejas pueden ser poderosas, pero también difíciles de leer y comprender, por lo que debes tener cuidado al usarlas. Si es posible, intente asignar alias significativos a las tablas y valores temporales. Además, las subconsultas correlacionadas pueden ser difíciles de optimizar, por lo que las características de rendimiento pueden variar entre diferentes bases de datos.

**Pruebas de existencia**

Cuando introdujimos **WHERE** restricciones en la Lección 2: Consultas con restricciones , el **IN** operador se usó para probar si el valor de la columna en la fila actual existía en una lista fija de valores. En consultas complejas, esto se puede ampliar mediante subconsultas para probar si existe un valor de columna en una lista dinámica de valores.

```
SELECT *, …
FROM mytable
WHERE column
    IN/NOT IN (SELECT another_column
               FROM another_table);
```

Al hacer esto, observe que la subconsulta interna debe seleccionar un valor de columna o expresión para producir una lista con la que se pueda probar el valor de la columna externa. Este tipo de restricción es poderosa cuando las restricciones se basan en datos actuales.

**uniones, intersecciones y excepciones**

Cuando se trabaja con varias tablas, el operador **UNION** y **UNION ALL** le permite agregar los resultados de una consulta a otra, asumiendo que tienen el mismo número de columnas, orden y tipo de datos. Si usa **UNION** sin **ALL**, las filas duplicadas entre las tablas se eliminarán del resultado.

```
SELECT column, another_column
   FROM mytable
UNION / UNION ALL / INTERSECT / EXCEPT
SELECT other_column, yet_another_column
   FROM another_table
ORDER BY column DESC
LIMIT n;
```

En el orden de las operaciones definido en la Lección 12: Orden de ejecución , **UNION** ocurre antes de **ORDER BY** y **LIMIT**. No es común usar **UNION** correos electrónicos, pero si tiene datos en diferentes tablas que no se pueden unir ni procesar, puede ser una alternativa a realizar múltiples consultas en la base de datos.

De manera similar a **UNION**, el **INTERSECT** operador se asegurará de que solo se devuelvan las filas que sean idénticas en ambos conjuntos de resultados, y el **EXCEPT** operador se asegurará de que solo se devuelvan las filas del primer conjunto de resultados que no estén en el segundo. Esto significa que el **EXCEPT** operador depende del orden de las consultas, como **LEFT JOIN** y **RIGHT JOIN**.

Ambos **INTERSECT** y **EXCEPT** también descartan filas duplicadas después de sus respectivas operaciones, aunque algunas bases de datos también admiten **INTERSECT ALL** y **EXCEPT ALL** permiten retener y devolver duplicados.

[🔼](#índice)

---

| **Inicio**            | **atrás 16**                | **Siguiente 18**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./16_Consultas_SQL.md) | [⏩](./18_Consultas_SQL.md) |
