| **Inicio**            | **atrás 20**                | **Siguiente 22**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./20_Consultas_SQL.md) | [⏩](./22_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                  |
| -------------------------------------------------------------------------------------------------------- |
| [201. Definición de estructura de dimensiones](#201-definición-de-estructura-de-dimensiones)             |
| [202. Estructura de un cubo de información](#202-estructura-de-un-cubo-de-información)                   |
| [203. Elaboración de medidas](#203-elaboración-de-medidas)                                               |
| [204. Relación entre dimensiones y grupo de medidas](#204-relación-entre-dimensiones-y-grupo-de-medidas) |
| [205. Medidas calculadas a través de sentencias MDX](#205-medidas-calculadas-a-través-de-sentencias-mdx) |
| [206. Elaboración de KPIs](#206-elaboración-de-kpis)                                                     |
| [207. Introducción a consultas DAX](#207-introducción-a-consultas-dax)                                   |
| [208. Configuración para la instalación de SSRS](#208-configuración-para-la-instalación-de-ssrs)         |
| [209. Creación de informes agrupados y subreportes](#209-creación-de-informes-agrupados-y-subreportes)   |
| [210. Definición de parámetros simples y en cascada](#210-definición-de-parámetros-simples-y-en-cascada) |

---

# **Tutorial de SQL**

## **201. Definición de estructura de dimensiones**

La estructura de dimensiones es una parte fundamental en la construcción de un modelo de datos multidimensional utilizando SQL Server Analysis Services (SSAS). Las dimensiones representan las características o atributos mediante las cuales se analizará y organizará la información en un cubo OLAP. A continuación, te proporcionaré una explicación detallada de la estructura de dimensiones en SSAS, junto con ejemplos.

1. **¿Qué es una dimensión en SSAS?**

En SSAS, una dimensión es una representación estructurada de los atributos o características que describen los datos en un cubo OLAP. Las dimensiones proporcionan contextos adicionales y jerarquías que permiten a los usuarios analizar y agrupar los datos en diferentes niveles de detalle. Cada dimensión se compone de una o más tablas de la base de datos subyacente, donde cada tabla representa un nivel diferente de la jerarquía.

2. **Estructura de dimensiones en SSAS:**

La estructura de dimensiones en SSAS se compone de los siguientes elementos clave:

- **Tablas de dimensiones:** Son las tablas de la base de datos subyacente que contienen los atributos y jerarquías relacionados. Cada tabla representa un nivel diferente de la jerarquía y puede contener columnas adicionales que proporcionan información adicional sobre los atributos.

- **Jerarquías:** Son estructuras de niveles anidados que representan la relación entre los atributos en una dimensión. Por ejemplo, en una dimensión de tiempo, puedes tener una jerarquía que va desde el año hasta el día, donde el año es el nivel superior y el día es el nivel más bajo.

- **Atributos:** Son las características o elementos que se utilizan para describir y organizar los datos en una dimensión. Cada atributo se representa como una columna en una tabla de dimensiones y puede tener propiedades adicionales, como etiquetas, claves, formatos de visualización, etc.

- **Relaciones:** Son las asociaciones o vínculos entre las tablas de dimensiones y las tablas de hechos en un cubo OLAP. Las relaciones establecen cómo se relacionan los datos en una dimensión con los datos en una tabla de hechos.

**Ejemplo de estructura de dimensiones en SSAS:**

Supongamos que estás construyendo un cubo OLAP para analizar datos de ventas. Tienes una tabla de dimensiones llamada "DimProducto" que contiene información sobre los productos, como su nombre, categoría, proveedor, etc. Además, tienes una tabla de dimensiones llamada "DimTiempo" que contiene información sobre el tiempo, como el año, el trimestre, el mes, etc. A continuación, te muestro cómo sería la estructura de dimensiones para estas dos tablas:

- **DimProducto:**

**Atributos:** ProductoID, NombreProducto, Categoría, Proveedor, etc.

- **DimTiempo:**

**Atributos:** FechaID, Fecha, Año, Trimestre, Mes, etc.

En este ejemplo, la tabla "DimProducto" representa una dimensión de producto y la tabla "DimTiempo" representa una dimensión de tiempo. Puedes establecer una relación entre estas tablas de dimensiones y las tablas de hechos en tu cubo OLAP para analizar las ventas por producto y por período de tiempo.

3. **Ventajas de la estructura de dimensiones en SSAS:**

La estructura de dimensiones en SSAS ofrece varias ventajas, como:

**Organización y análisis eficiente de los datos:** Las dimensiones permiten organizar los datos de manera lógica y jerárquica, lo que facilita su análisis y exploración en diferentes niveles de detalle.

- **Mayor comprensión y contexto de los datos:** Las dimensiones proporcionan información adicional sobre los atributos, lo que ayuda a los usuarios a comprender y contextualizar los datos.

- **Capacidad de navegación y desglose:** Las jerarquías en las dimensiones permiten a los usuarios navegar y desglosar los datos de manera intuitiva, desde el nivel más alto hasta el más bajo.

- **Mejor rendimiento de consulta:** La estructura de dimensiones optimiza el rendimiento de las consultas, ya que los datos se organizan de manera eficiente y se pueden utilizar índices y agregaciones.

En resumen, la estructura de dimensiones en SSAS es fundamental para organizar y analizar los datos en un cubo OLAP. Las dimensiones proporcionan contextos adicionales, jerarquías y atributos que permiten a los usuarios explorar y comprender mejor los datos.

![estructura de dimensiones](../../img/estructura%20de%20dimensiones.jpg "estructura de dimensiones")

[🔼](#índice)

---

## **202. Estructura de un cubo de información**

La estructura de un cubo de información se refiere a la forma en que se organizan y modelan los datos en un entorno de análisis multidimensional. Un cubo de información es una representación lógica de los datos que permite a los usuarios realizar consultas y análisis en diferentes dimensiones y niveles de agregación. A continuación, te proporcionaré una explicación detallada de la estructura de un cubo de información, junto con ejemplos.

1. **Elementos clave de la estructura de un cubo de información:**

Los cubos de información se componen de los siguientes elementos clave:

- **Dimensiones:** Las dimensiones representan las características o atributos mediante los cuales se analizará y organizará la información en el cubo. Por ejemplo, en un cubo de ventas, las dimensiones pueden ser Producto, Tiempo y Ubicación.

- **Jerarquías:** Las jerarquías representan la estructura de niveles anidados dentro de una dimensión. Por ejemplo, en la dimensión de Tiempo, puedes tener una jerarquía que va desde el año hasta el día, donde el año es el nivel superior y el día es el nivel más bajo.

- **Medidas:** Las medidas son los valores numéricos que se analizarán en el cubo. Por ejemplo, en un cubo de ventas, las medidas pueden ser Ventas Totales, Costo, Ganancia, etc.

- **Niveles de agregación:** Los niveles de agregación representan diferentes niveles de resumen de datos en una dimensión. Por ejemplo, en la dimensión de Tiempo, puedes tener niveles de agregación a nivel anual, trimestral, mensual, etc.

**Ejemplo de estructura de un cubo de información:**

Supongamos que estás construyendo un cubo de información para analizar datos de ventas. En este caso, podrías tener las siguientes dimensiones y jerarquías:

- **Dimensión de Producto:**

**Jerarquía de Producto:** Categoría > Subcategoría > Producto

- **Dimensión de Tiempo:**

**Jerarquía de Tiempo:** Año > Trimestre > Mes > Día
Además, podrías tener medidas como Ventas Totales, Costo, Ganancia, etc.

En este ejemplo, los usuarios podrían realizar consultas y análisis en el cubo de información para obtener información sobre las ventas por categoría de producto, por período de tiempo y aplicar diferentes niveles de agregación según sea necesario.

2. **Beneficios de la estructura de un cubo de información:**

La estructura de un cubo de información ofrece varios beneficios, entre ellos:

- **Análisis multidimensional:** Los usuarios pueden analizar los datos en diferentes dimensiones y niveles de agregación, lo que les permite obtener información más detallada o realizar análisis de alto nivel según sus necesidades.

- **Desglose y navegación intuitiva:** Las jerarquías permiten a los usuarios desglosar los datos en diferentes niveles y realizar un análisis detallado desde una perspectiva de "arriba hacia abajo" o de "abajo hacia arriba".

- **Rendimiento optimizado:** La estructura de un cubo de información está diseñada para optimizar el rendimiento de las consultas y los cálculos, lo que permite respuestas rápidas a las consultas y análisis complejos.

- **Mayor comprensión de los datos:** La estructura del cubo facilita la comprensión de los datos al proporcionar una representación lógica y organizada de la información.

En resumen, la estructura de un cubo de información se basa en dimensiones, jerarquías, medidas y niveles de agregación para permitir consultas y análisis multidimensionales. Proporciona una forma intuitiva y eficiente de analizar los datos desde diferentes perspectivas y niveles de detalle.

![Estructura de un cubo](../../img/Estructura%20de%20un%20cubo.jpg "Estructura de un cubo")

[🔼](#índice)

---

## **203. Elaboración de medidas**

En SSAS (SQL Server Analysis Services), la elaboración de medidas se refiere al proceso de definir y calcular las métricas o medidas que se utilizarán en un cubo de información. Las medidas representan los valores numéricos que se analizarán y agregan en el cubo. A continuación, te proporcionaré una explicación detallada de cómo elaborar medidas en SSAS, junto con ejemplos.

1. **Definición de medidas:**

En SSAS, las medidas se definen en función de las necesidades específicas del negocio. Pueden ser medidas simples, como una suma o un conteo, o medidas más complejas que involucran cálculos personalizados. Al definir una medida, es importante considerar el contexto y los requisitos de análisis.

2. **Elaboración de medidas en SSAS:**

En SSAS, las medidas se elaboran en el diseño del cubo utilizando el lenguaje MDX (Multidimensional Expressions). A continuación se muestra un ejemplo de cómo elaborar una medida de ventas totales en un cubo de información de ventas:

```
CREATE MEMBER CURRENTCUBE.[Measures].[Ventas Totales]
AS
SUM([DimTiempo].[Año].CurrentMember, [DimProducto].[Producto].CurrentMember, [Measures].[Ventas]),
FORMAT_STRING = "#,##0.00";
```

En este ejemplo, la medida "`Ventas Totales`" se calcula como la suma de las ventas para cada combinación de año y producto en el cubo. La función `SUM` se utiliza para realizar la agregación y la medida se asigna a un formato de visualización específico.

3. **Medidas calculadas:**

Además de las medidas simples, `SSAS` permite la creación de medidas calculadas, que son medidas derivadas que se calculan en función de otras medidas existentes. Estas medidas se definen utilizando expresiones `MDX`. A continuación se muestra un ejemplo de cómo elaborar una medida calculada de margen de beneficio en un cubo de información de ventas:

```
CREATE MEMBER CURRENTCUBE.[Measures].[Margen de Beneficio]
AS
([Measures].[Ganancia] / [Measures].[Ventas]) * 100,
FORMAT_STRING = "#,##0.00%";
```

En este ejemplo, la medida "`Margen de Beneficio`" se calcula dividiendo la ganancia entre las ventas y multiplicando el resultado por 100. La medida se asigna a un formato de porcentaje para su visualización adecuada.

4. **Utilización de funciones MDX:**

En el proceso de elaboración de medidas, se pueden utilizar diversas funciones `MDX` para realizar cálculos más complejos. Algunas de las funciones comunes incluyen `SUM`, `COUNT`, `AVG`, `MAX`, `MIN`, entre otras. Estas funciones permiten realizar operaciones matemáticas, agregaciones y filtrado de datos según sea necesario.

En resumen, la elaboración de medidas en SSAS implica definir y calcular las métricas que se utilizarán en un cubo de información. Las medidas pueden ser simples o calculadas, y se definen utilizando el lenguaje MDX. Estas medidas proporcionan los valores numéricos que se analizarán y agregan en el cubo.

[🔼](#índice)

---

## **204. Relación entre dimensiones y grupo de medidas**

En SSAS (SQL Server Analysis Services), la relación entre dimensiones y grupos de medidas es fundamental para organizar y analizar los datos en un cubo de información. Las dimensiones representan las características o atributos por los cuales se desea analizar los datos, mientras que los grupos de medidas contienen las métricas o medidas que se utilizarán en el análisis. A continuación, te proporcionaré una explicación detallada de la relación entre dimensiones y grupos de medidas en SSAS, junto con ejemplos.

1. **Dimensiones:**

Las dimensiones en SSAS representan las entidades o categorías por las cuales se desea analizar los datos. Estas dimensiones pueden incluir atributos como Producto, Tiempo, Ubicación, Cliente, etc. Las dimensiones proporcionan contextos y filtros para el análisis de los datos y permiten realizar desgloses y segmentaciones de información.

Por ejemplo, supongamos que estamos construyendo un cubo de información para analizar las ventas. Podríamos tener una dimensión de Producto con atributos como Categoría, Subcategoría y Producto. Otra dimensión podría ser la dimensión de Tiempo, con atributos como Año, Mes y Día.

2. **Grupos de medidas:**

Los grupos de medidas en SSAS contienen las métricas o medidas que se utilizarán en el análisis de los datos. Estas medidas representan los valores numéricos que se analizarán y agregan en el cubo de información. Algunos ejemplos de medidas comunes podrían ser Ventas Totales, Ganancia, Costo, etc.

Es importante tener en cuenta que las medidas deben estar relacionadas lógicamente con las dimensiones correspondientes para permitir un análisis significativo. Esto se logra mediante la definición de relaciones entre las dimensiones y los grupos de medidas.

3. **Relación entre dimensiones y grupos de medidas:**

La relación entre dimensiones y grupos de medidas se establece mediante la configuración de relaciones en el diseño del cubo. Estas relaciones especifican cómo se conectan las dimensiones con los grupos de medidas y cómo se deben realizar los cálculos y agregaciones.

Por ejemplo, en un cubo de ventas, podemos tener una relación entre la dimensión de Producto y el grupo de medidas que contiene las métricas de ventas. Esto permitirá analizar las ventas por diferentes atributos de productos, como categoría, subcategoría o producto específico.

Además, las dimensiones pueden tener relaciones entre sí, como la relación entre la dimensión de Producto y la dimensión de Tiempo. Esto permitirá realizar análisis de ventas por producto en diferentes períodos de tiempo.

4. **Utilización en el análisis:**

La relación entre dimensiones y grupos de medidas permite realizar análisis multidimensional en el cubo de información. Los usuarios pueden seleccionar dimensiones y aplicar filtros para enfocarse en un subconjunto específico de datos. Luego, pueden utilizar las medidas relacionadas para realizar cálculos y análisis en función de esas dimensiones.

Por ejemplo, un usuario puede seleccionar la dimensión de Producto y la dimensión de Tiempo para analizar las ventas de un producto específico a lo largo del tiempo. Luego, pueden utilizar medidas como Ventas Totales, Ganancia, etc., para obtener información detallada sobre el rendimiento de ese producto en diferentes períodos de tiempo.

En resumen, la relación entre dimensiones y grupos de medidas en SSAS es fundamental para el análisis multidimensional en un cubo de información. Las dimensiones representan las características o atributos por los cuales se desea analizar los datos, mientras que los grupos de medidas contienen las métricas o medidas utilizadas en el análisis. La configuración de relaciones entre dimensiones y grupos de medidas permite un análisis significativo y contextualizado de los datos.

[🔼](#índice)

---

## **205. Medidas calculadas a través de sentencias MDX**

En SSAS (SQL Server Analysis Services), puedes crear medidas calculadas utilizando el lenguaje MDX (Multidimensional Expressions). Las medidas calculadas te permiten realizar cálculos personalizados basados en otras medidas existentes en el cubo de información. A continuación, te proporcionaré una explicación detallada de cómo crear medidas calculadas utilizando sentencias MDX en SSAS, junto con ejemplos.

1. **Sintaxis básica de una medida calculada:**

La sintaxis básica para crear una medida calculada en MDX es la siguiente:

`CREATE MEMBER [Dimensión].[Medidas].[NombreMedidaCalculada] AS [ExpresiónMDX];`

- `[Dimensión]` se refiere a la dimensión a la que pertenece la medida calculada.
- `[Medidas]` se refiere al grupo de medidas en el que se creará la medida calculada.
- `[NombreMedidaCalculada]` es el nombre que le darás a la medida calculada.
- `[ExpresiónMDX]` es la expresión MDX que define cómo se calculará la medida calculada.

**Ejemplo de medida calculada simple:**

Supongamos que tenemos un cubo de información de ventas con una medida existente llamada "Ventas" y queremos crear una medida calculada llamada "Descuento" que represente el 10% de las ventas. El código MDX para crear esta medida calculada sería el siguiente:

`CREATE MEMBER [DimProducto].[Medidas].[Descuento] AS [DimProducto].[Medidas].[Ventas] * 0.1;`

En este ejemplo, la medida calculada "Descuento" se calcula multiplicando la medida existente "Ventas" por 0.1 para obtener el 10% del valor de las ventas.

**Ejemplo de medida calculada utilizando funciones MDX:**

Las medidas calculadas también pueden involucrar el uso de funciones MDX para realizar cálculos más complejos. Por ejemplo, supongamos que queremos crear una medida calculada llamada "Margen de beneficio" que represente el margen de beneficio de las ventas. El código MDX para crear esta medida calculada podría ser el siguiente:

`CREATE MEMBER [DimProducto].[Medidas].[Margen de beneficio] AS ([DimProducto].[Medidas].[Ventas] - [DimProducto].[Medidas].[Costo]) / [DimProducto].[Medidas].[Ventas];`

En este ejemplo, la medida calculada "Margen de beneficio" se calcula restando la medida de costo de la medida de ventas y luego dividiendo el resultado por la medida de ventas.

2. **Utilización de condicionales en medidas calculadas:**

Las medidas calculadas también pueden incluir condicionales para realizar cálculos basados en ciertas condiciones. Por ejemplo, supongamos que queremos crear una medida calculada llamada "Total de ventas positivas" que represente la suma de las ventas solo si son mayores que cero. El código MDX para crear esta medida calculada sería el siguiente:

`CREATE MEMBER [DimProducto].[Medidas].[Total de ventas positivas] AS IIF([DimProducto].[Medidas].[Ventas] > 0, [DimProducto].[Medidas].[Ventas], 0);`

En este ejemplo, utilizamos la función `IIF` para evaluar si la medida de ventas es mayor que cero. Si es verdadero, se utiliza la medida de ventas en el cálculo, de lo contrario, se establece en cero.

Estos son solo algunos ejemplos de cómo crear medidas calculadas utilizando sentencias MDX en SSAS. Puedes combinar diferentes funciones y operadores MDX para crear medidas calculadas más complejas según tus necesidades de análisis.

[🔼](#índice)

---

## **206. Elaboración de KPIs**

Los KPIs (Key Performance Indicators) o Indicadores Clave de Desempeño son medidas utilizadas para evaluar el rendimiento y el logro de objetivos en una organización. Los KPIs proporcionan una manera efectiva de medir el progreso y el éxito en áreas críticas de negocio. A continuación, te proporcionaré una explicación detallada de cómo elaborar KPIs, junto con ejemplos.

1. **Identificación de objetivos clave:**

El primer paso en la elaboración de KPIs es identificar los objetivos clave de tu negocio. Estos objetivos deben ser específicos, medibles, alcanzables, relevantes y con un tiempo definido (SMART). Por ejemplo, si eres una empresa de comercio electrónico, algunos objetivos clave podrían ser aumentar las ventas, mejorar la satisfacción del cliente o reducir los tiempos de entrega.

2. **Selección de métricas relevantes:**

Una vez que hayas identificado tus objetivos clave, debes seleccionar las métricas relevantes que te permitirán evaluar el rendimiento en relación a esos objetivos. Estas métricas deben ser cuantificables y estar directamente relacionadas con los objetivos establecidos. Por ejemplo, si el objetivo es aumentar las ventas, puedes seleccionar métricas como el ingreso total, el número de pedidos o el valor promedio de cada transacción.

3. **Definición de umbrales o metas:**

Los KPIs también requieren la definición de umbrales o metas que te permitan evaluar si estás alcanzando los objetivos establecidos. Estos umbrales deben ser realistas y representar el nivel de rendimiento deseado. Por ejemplo, si el objetivo es mejorar la satisfacción del cliente, puedes establecer una meta del 90% de satisfacción en las encuestas de posventa.

4. **Presentación visual de los KPIs:**

Es importante presentar los KPIs de manera visual y fácilmente comprensible. Esto puede hacerse a través de paneles de control, tableros o informes que muestren de forma clara y concisa el rendimiento en relación a los objetivos establecidos. Los gráficos, indicadores de colores y comparativas son herramientas útiles para visualizar los KPIs de manera efectiva.

5. **Monitoreo y análisis continuo:**

Los KPIs deben ser monitoreados y analizados de forma continua para evaluar el progreso y tomar decisiones informadas. Esto implica realizar un seguimiento regular de las métricas, comparar los resultados con los umbrales establecidos y realizar análisis para identificar tendencias, patrones o áreas de mejora. Con base en estos análisis, se pueden tomar acciones correctivas o realizar ajustes en la estrategia.

**Ejemplo:**

Supongamos que una empresa de telecomunicaciones tiene el objetivo de aumentar la retención de clientes. Algunos KPIs relevantes podrían ser:

- **Tasa de retención de clientes:** Porcentaje de clientes existentes que continúan utilizando los servicios de la empresa en un período determinado.

- **Nivel de satisfacción del cliente:** Evaluación de la satisfacción de los clientes a través de encuestas o puntuaciones.

- **Promedio de tiempo de respuesta a solicitudes de servicio:** Tiempo promedio que tarda la empresa en responder a las solicitudes de servicio de los clientes.

Estos KPIs pueden ser monitoreados en un tablero de control que muestre el rendimiento actual en relación a los objetivos establecidos. Por ejemplo, se puede establecer una meta de retención de clientes del 90% y una meta de satisfacción del cliente del 85%.

En resumen, la elaboración de KPIs implica identificar objetivos clave, seleccionar métricas relevantes, definir umbrales o metas, presentar visualmente los KPIs y realizar un monitoreo y análisis continuo. Los KPIs ayudan a medir el rendimiento y a tomar decisiones informadas para mejorar el desempeño de la organización.

![Elaboración de KPIs](../../img/Elaboraci%C3%B3n%20de%20KPIs.png "Elaboración de KPIs")

[🔼](#índice)

---

## **207. Introducción a consultas DAX**

Las consultas DAX (Data Analysis Expressions) son un lenguaje utilizado en Microsoft Power BI, Power Pivot y Analysis Services para realizar cálculos y consultas en modelos de datos. DAX permite realizar operaciones avanzadas de análisis y manipulación de datos en tiempo real. A continuación, te proporcionaré una explicación detallada de las consultas DAX, junto con ejemplos.

1. **Sintaxis básica:**

La sintaxis básica de una consulta DAX consiste en una función seguida de paréntesis que contiene los argumentos de la función. Por ejemplo, la función `SUM` se utiliza para sumar los valores de una columna en una tabla y tiene la siguiente sintaxis: `SUM(nombre_columna)`.

2. **Filtrado de datos:**

`DAX` permite filtrar datos utilizando la función `FILTER`. Esta función toma una tabla como argumento y devuelve una nueva tabla filtrada según una condición especificada. Por ejemplo, la siguiente consulta DAX devuelve la suma de los ingresos solo para los productos de la categoría "`Electrónica`":

`SUMX(FILTER(tabla_productos, tabla_productos[categoria] = "Electrónica"), tabla_productos[ingresos])`

3. **Cálculos agregados:**

`DAX` ofrece funciones para realizar cálculos agregados, como `SUM`, `AVERAGE`, `MIN`, `MAX`, `COUNT`, entre otros. Estas funciones se utilizan para realizar operaciones matemáticas en columnas o medidas. Por ejemplo, la siguiente consulta `DAX` calcula el promedio de ventas mensuales:

`AVERAGE(tabla_ventas[ventas])`

4. **Creación de medidas:**

DAX permite crear medidas personalizadas que realizan cálculos basados en las columnas existentes en una tabla. Estas medidas se pueden utilizar para agregar información adicional en un informe. Por ejemplo, la siguiente consulta DAX crea una medida que calcula la ganancia total de ventas:

`ganancia_total = SUM(tabla_ventas[ventas]) - SUM(tabla_ventas[gastos])`

5. **Funciones de tiempo:**

DAX incluye funciones para realizar cálculos basados en fechas y tiempo. Estas funciones permiten realizar análisis de series temporales y realizar cálculos basados en períodos específicos. Por ejemplo, la función `DATEADD` se utiliza para agregar o restar días, meses o años a una fecha. La siguiente consulta DAX calcula el total de ventas de los últimos 3 meses:

`TOTALYTD(SUM(tabla_ventas[ventas]), tabla_ventas[fecha], "3 Months")`

Estos son solo algunos ejemplos de cómo se utilizan las consultas DAX para realizar cálculos y consultas en modelos de datos. DAX ofrece una amplia gama de funciones y capacidades para realizar análisis avanzados y obtener información significativa de los datos.

[🔼](#índice)

---

## **208. Configuración para la instalación de SSRS**

La instalación de SQL Server Reporting Services (SSRS) implica realizar una serie de configuraciones para garantizar un funcionamiento adecuado. A continuación, te proporcionaré una explicación detallada de las configuraciones necesarias, junto con ejemplos.

1. **Verificar los requisitos del sistema:**

Antes de comenzar la instalación de SSRS, es importante verificar los requisitos del sistema para asegurarse de que el servidor cumpla con los requerimientos mínimos. Estos requisitos incluyen la versión y edición de SQL Server, el sistema operativo compatible, los servicios y características adicionales requeridos, y los permisos de usuario necesarios.

2. **Configurar la instancia de SQL Server:**

Si aún no tienes una instancia de SQL Server instalada, debes realizar la instalación de SQL Server antes de proceder con la instalación de SSRS. Durante la instalación de SQL Server, asegúrate de seleccionar los componentes de Reporting Services para habilitar su funcionalidad.

3. **Configurar la instancia de SSRS:**

Una vez que hayas instalado SQL Server y habilitado Reporting Services, deberás configurar la instancia de SSRS. Esto implica realizar los siguientes pasos:

- **Abrir el Administrador de Configuración de Reporting Services:** Puedes encontrarlo en el menú de inicio o buscando "Reporting Services Configuration Manager".

- **Conectar a la instancia de SQL Server:** En el Administrador de Configuración, selecciona la instancia de SQL Server en la lista desplegable "Conectar a una instancia de informes".

- **Configurar el servicio de informes:** En la pestaña "Servicio de informes", especifica el nombre de la instancia de informes y el puerto que se utilizará para acceder al servicio. También puedes configurar las opciones de autenticación y seguridad según tus necesidades.

- **Configurar la base de datos de informes:** En la pestaña "Base de datos", selecciona si deseas crear una base de datos de informes o si ya tienes una existente que deseas utilizar. Si estás creando una nueva base de datos, proporciona un nombre y configura las opciones adicionales según tus preferencias.

- **Configurar el acceso web:** En la pestaña "Acceso web", especifica las opciones de autenticación y configuración de HTTPS para el acceso web a los informes.

4. **Verificar la configuración:**

Una vez que hayas realizado la configuración en el Administrador de Configuración de Reporting Services, verifica que todo esté configurado correctamente. Puedes hacerlo probando el acceso al Portal web de informes a través de un navegador web. Intenta acceder al portal utilizando la URL especificada durante la configuración (por ejemplo, http://localhost/Reports) y verifica que puedas ver y ejecutar informes.

Estos son los pasos básicos para configurar la instalación de SQL Server Reporting Services (SSRS). Recuerda que la configuración específica puede variar dependiendo de tu entorno y requisitos. Asegúrate de seguir las guías y documentación oficial de Microsoft para obtener instrucciones detalladas y actualizadas.

[🔼](#índice)

---

## **209. Creación de informes agrupados y subreportes**

La creación de informes agrupados y subinformes en SQL Server Reporting Services (SSRS) permite organizar y presentar datos de manera jerárquica y estructurada. A continuación, te proporcionaré una explicación detallada de cómo crear informes agrupados y subinformes, junto con ejemplos.

1. **Informes agrupados:**

Los informes agrupados se utilizan para resumir y mostrar datos agrupados en función de una o más columnas. Estos informes son útiles cuando se necesita presentar datos de forma jerárquica, como totales por categorías o regiones. A continuación, se muestra un ejemplo de cómo crear un informe agrupado:

- Abre SQL Server Data Tools (SSDT) o el diseñador de informes de SSRS.

- Crea un nuevo informe y agrega un origen de datos adecuado, como una conexión a una base de datos.

- Arrastra y suelta los campos relevantes desde el origen de datos al área de diseño del informe.

- Selecciona los campos que deseas utilizar para agrupar los datos y arrástralos a la sección "Filas" o "Columnas" en el área de diseño.

- Agrega los campos de datos que deseas mostrar dentro de cada grupo en la sección correspondiente del área de diseño.

- Configura cualquier cálculo o agregación necesario, como sumas o promedios, utilizando expresiones o funciones de SSRS.

- Ajusta el diseño del informe según tus preferencias, incluyendo encabezados, pies de página y formatos visuales.

- Previsualiza y verifica el informe para asegurarte de que los datos se muestren correctamente agrupados.

2. **Subinformes:**

Los subinformes se utilizan para incluir informes secundarios dentro de un informe principal. Los subinformes son útiles cuando se necesita presentar información detallada o adicional relacionada con los datos principales. A continuación, se muestra un ejemplo de cómo crear un subinforme:

- Abre SQL Server Data Tools (SSDT) o el diseñador de informes de SSRS.

- Crea un nuevo informe para el informe principal y otro informe para el subinforme.

- Configura los datos y diseño del informe principal como se describió anteriormente.

- En el informe principal, arrastra y suelta un objeto "Subinforme" desde la caja de herramientas al área de diseño.

- Configura la propiedad "Ruta de acceso del informe" del subinforme para especificar la ubicación del informe secundario.

- Configura los parámetros del subinforme si es necesario, para filtrar los datos o pasar valores desde el informe principal al subinforme.

- Personaliza el diseño y formato del subinforme según tus necesidades.

Previsualiza y verifica el informe principal para asegurarte de que el subinforme se muestra correctamente y está vinculado correctamente a los datos principales.

Recuerda que los informes agrupados y subinformes en SSRS ofrecen una amplia gama de opciones de diseño y funcionalidad. Puedes personalizar aún más los informes utilizando expresiones, variables y otras características avanzadas de SSRS.

[🔼](#índice)

---

## **210. Definición de parámetros simples y en cascada**

En SQL Server Reporting Services (SSRS), los parámetros son elementos importantes que permiten a los usuarios filtrar y personalizar los datos en un informe. Hay dos tipos principales de parámetros: parámetros simples y parámetros en cascada. A continuación, te proporcionaré una explicación detallada de cada uno de ellos, junto con ejemplos.

1. **Parámetros simples:**

Los parámetros simples son aquellos que permiten a los usuarios seleccionar un único valor de una lista predefinida. Estos parámetros son útiles cuando se desea filtrar los datos de acuerdo con una opción específica. A continuación, se muestra un ejemplo de cómo crear un parámetro simple:

- Abre SQL Server Data Tools (SSDT) o el diseñador de informes de SSRS.

- Crea un nuevo informe y agrega un origen de datos adecuado, como una conexión a una base de datos.

- En el área de diseño del informe, ve a la pestaña "Parámetros" en la parte inferior del panel de informes.

- Haz clic en "Agregar parámetro" y proporciona un nombre descriptivo para el parámetro.

- Define el tipo de dato del parámetro, como texto, fecha o número, y establece cualquier valor predeterminado o restricciones necesarias.

- Define los valores posibles para el parámetro. Puedes obtenerlos de una consulta SQL, de una lista estática o de una consulta de datos existente.

- Utiliza el parámetro en las consultas y expresiones del informe para filtrar los datos según la selección del usuario.

- Previsualiza y verifica el informe para asegurarte de que el parámetro funcione correctamente y filtre los datos de acuerdo con la selección del usuario.

2. **Parámetros en cascada:**

Los parámetros en cascada son aquellos que dependen de la selección de otro parámetro. Estos parámetros están vinculados y su lista de valores se actualiza dinámicamente en función de la selección realizada en el parámetro anterior. Son útiles cuando se necesita filtrar datos en múltiples niveles o jerarquías. A continuación, se muestra un ejemplo de cómo crear parámetros en cascada:

- Sigue los mismos pasos anteriores para crear los parámetros simples iniciales.

- Crea un segundo parámetro que se basará en la selección del primer parámetro.

- Define los valores posibles para el segundo parámetro utilizando una consulta SQL que tome como entrada la selección del primer parámetro.

- Utiliza el segundo parámetro en las consultas y expresiones del informe para filtrar los datos según la selección del usuario en ambos parámetros.

- Previsualiza y verifica el informe para asegurarte de que los parámetros en cascada funcionen correctamente y los datos se filtren según las selecciones del usuario.

Los parámetros simples y en cascada ofrecen flexibilidad y capacidad de personalización en los informes de SSRS. Puedes utilizar expresiones y funciones adicionales para ajustar aún más el comportamiento de los parámetros y adaptarlos a tus necesidades específicas.

**Tipos de reportes matriz y gráficos**

En SQL Server Reporting Services (SSRS), existen diferentes tipos de reportes que se pueden utilizar para presentar datos de manera efectiva. Dos de los tipos más comunes son los reportes matriz y los reportes gráficos. A continuación, te proporcionaré una explicación detallada de cada uno de ellos, junto con ejemplos.

1. **Reportes matriz:**

Los reportes matriz son útiles cuando se desea presentar datos en una estructura de tabla bidimensional, donde las filas y columnas representan diferentes categorías y los valores se muestran en las intersecciones. Este tipo de reporte es especialmente útil cuando se desea realizar comparaciones entre diferentes elementos. A continuación, se muestra un ejemplo de cómo crear un reporte matriz:

- Abre SQL Server Data Tools (SSDT) o el diseñador de informes de SSRS.

- Crea un nuevo informe y agrega un origen de datos adecuado, como una conexión a una base de datos.

- Arrastra y suelta un objeto "Tabla" desde la caja de herramientas al área de diseño del informe.

- Configura las columnas de la tabla para representar las diferentes categorías o elementos que deseas mostrar.

- Configura las filas de la tabla para representar las diferentes subcategorías o elementos adicionales.

- Configura las celdas de la tabla para mostrar los valores correspondientes a la intersección de las filas y columnas.

- Aplica formatos y estilos visuales según tus preferencias para mejorar la legibilidad del reporte.

- Previsualiza y verifica el informe para asegurarte de que los datos se muestren correctamente en la estructura de matriz.

2. **Reportes gráficos:**

Los reportes gráficos son útiles para visualizar datos de manera más intuitiva y comprensible utilizando gráficos y visualizaciones visuales. Permiten identificar patrones, tendencias y comparaciones de manera más rápida y efectiva. A continuación, se muestra un ejemplo de cómo crear un reporte gráfico:

- Abre SQL Server Data Tools (SSDT) o el diseñador de informes de SSRS.

- Crea un nuevo informe y agrega un origen de datos adecuado, como una conexión a una base de datos.

- Arrastra y suelta un objeto "Gráfico" desde la caja de herramientas al área de diseño del informe.

- Configura los datos del gráfico seleccionando la fuente de datos y los campos relevantes.

- Selecciona el tipo de gráfico que mejor se adapte a tus necesidades, como gráfico de barras, gráfico circular, gráfico de líneas, etc.

- Configura las series y categorías del gráfico utilizando los campos de datos adecuados.

- Personaliza los ejes, leyendas, títulos y otros aspectos visuales del gráfico según tus preferencias.

- Previsualiza y verifica el informe para asegurarte de que el gráfico muestre los datos de manera clara y efectiva.

Los reportes matriz y los reportes gráficos son solo algunos ejemplos de los tipos de informes disponibles en SSRS. Dependiendo de tus necesidades y los datos que deseas presentar, puedes explorar otros tipos de informes, como informes de tabla, informes de lista, informes de matriz combinada, etc.

**Ordenamiento condicional**

El ordenamiento condicional, también conocido como ordenamiento personalizado o ordenamiento basado en condiciones, se refiere a la capacidad de ordenar los datos en una consulta SQL en función de una condición específica en lugar de simplemente ordenarlos alfabéticamente o numéricamente. Esto permite establecer reglas personalizadas para determinar el orden de los resultados de una consulta. A continuación, te proporcionaré una explicación detallada con ejemplos.

Supongamos que tienes una tabla llamada "`Productos`" con las siguientes columnas: "`Nombre`" (cadena de texto) y "`Stock`" (entero). Quieres ordenar los productos de acuerdo con las siguientes reglas:

- Los productos con stock disponible deben aparecer primero en el resultado.
- Los productos con stock agotado deben aparecer después de los productos disponibles, pero antes de los productos restantes.
- Para lograr esto, puedes utilizar una cláusula "ORDER BY" en tu consulta SQL junto con una expresión condicional. Aquí tienes un ejemplo de cómo lograrlo:

```
SELECT Nombre, Stock
FROM Productos
ORDER BY
    CASE
        WHEN Stock > 0 THEN 1 -- Productos con stock disponible
        WHEN Stock = 0 THEN 2 -- Productos agotados
        ELSE 3 -- Otros productos
    END;
```

En este ejemplo, utilizamos la expresión condicional `CASE` dentro de la cláusula "`ORDER BY`". La expresión `CASE` evalúa la columna "`Stock`" y asigna un valor numérico a cada fila según la condición correspondiente. Luego, ordenamos los resultados en función de esos valores numéricos, lo que asegura que los productos disponibles aparezcan primero, seguidos de los productos agotados y finalmente los demás productos.

El resultado de la consulta mostrará los productos ordenados de acuerdo con las reglas establecidas. Por ejemplo:

```
Nombre      | Stock
--------------------
Producto A  | 5
Producto B  | 0
Producto C  | 2
Producto D  | 0
Producto E  | 10
```

En este resultado, los productos disponibles (stock > 0) se muestran primero, seguidos de los productos agotados (stock = 0) y, finalmente, los productos con otros valores de stock.

El ordenamiento condicional te permite personalizar el orden de los resultados de una consulta según tus necesidades y reglas específicas. Puedes utilizar expresiones condicionales más complejas con múltiples condiciones para definir reglas de ordenamiento más elaboradas.

**Aplicación de pie de páginas y cabeceras**

La aplicación de pie de páginas y cabeceras en informes o documentos es una práctica común para agregar información adicional, como números de página, fechas, títulos o logotipos, que se muestra de manera consistente en todas las páginas. A continuación, te proporcionaré una explicación detallada sobre cómo aplicar pie de páginas y cabeceras en informes, junto con ejemplos utilizando SQL Server Reporting Services (SSRS).

Para comenzar, asumamos que estás creando un informe utilizando el diseñador de informes de SSRS. Aquí tienes los pasos para aplicar pie de página y cabecera:

1. **Abrir el informe en el diseñador de informes:**

- Inicia el diseñador de informes de SSRS (SQL Server Data Tools o Report Builder).
- Abre el informe existente o crea uno nuevo.

2. **Agregar el pie de página y la cabecera:**

- Haz clic derecho en el área del informe y selecciona "Propiedades del informe".
- En las propiedades del informe, selecciona la pestaña "Encabezado y pie de página".
- Activa la opción "Mostrar encabezado" y/o "Mostrar pie de página" según tus necesidades.
- En el área de diseño, aparecerán una cabecera y un pie de página predeterminados.

3. **Personalizar el contenido de la cabecera y el pie de página:**

- Haz clic en la cabecera o el pie de página en el área de diseño para seleccionarlo.
- Utiliza las herramientas de formato y diseño para agregar texto, imágenes o elementos adicionales según tus necesidades.
- Puedes agregar elementos estáticos, como títulos o logotipos, utilizando las herramientas de diseño del informe.
- También puedes agregar elementos dinámicos, como números de página o fechas, utilizando expresiones o variables.

4. **Configurar propiedades adicionales:**

- Haz clic derecho en la cabecera o el pie de página y selecciona "Propiedades del objeto".
- En las propiedades, puedes ajustar la altura, el ancho, el alineamiento y otras opciones para personalizar la apariencia.

5. **Previsualizar el informe:**

- Guarda el informe y previsualízalo para ver cómo se muestra el encabezado y el pie de página en las diferentes páginas.
- Asegúrate de que la información en el encabezado y el pie de página se actualice correctamente en todas las páginas, como los números de página consecutivos.

Aquí tienes un ejemplo de cómo se vería un informe con pie de página y cabecera en SSRS:

```
-----------------------------------
|          Título del informe      |
-----------------------------------
|      Cabecera personalizada      |
-----------------------------------
|    Datos del informe              |
|    ...
|    ...
|    ...
|                                  |
|                                  |
|    ...
|    ...
|                                  |
|                                  |
|                                  |
-----------------------------------
|   Pie de página personalizado    |
-----------------------------------
```

En este ejemplo, el informe tiene un título en la parte superior, seguido de una cabecera personalizada que muestra información adicional. El cuerpo del informe contiene los datos y se extiende a lo largo de múltiples páginas. En la parte inferior de cada página, se muestra un pie de página personalizado, que puede incluir números de página, fechas u otra información relevante.

Recuerda que las opciones y configuraciones específicas pueden variar según la versión y la herramienta que estés utilizando para crear informes. Sin embargo, el concepto básico de aplicar pie de página y cabecera sigue siendo el mismo.

[🔼](#índice)

---

| **Inicio**            | **atrás 20**                | **Siguiente 22**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./20_Consultas_SQL.md) | [⏩](./22_Consultas_SQL.md) |
