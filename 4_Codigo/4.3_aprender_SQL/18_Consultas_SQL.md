| **Inicio**            | **atrás 17**                | **Siguiente 19**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./17_Consultas_SQL.md) | [⏩](./19_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------ |
| [171. ¿Qué es inteligencia de negocios?](#171-¿qué-es-inteligencia-de-negocios)                                                      |
| [172. Proceso de inteligencia de negocios](#172-proceso-de-inteligencia-de-negocios)                                                 |
| [173. Tradicional vs BI Moderno](#173-tradicional-vs-bi-moderno)                                                                     |
| [174. Evolución en el análisis](#174-evolución-en-el-análisis)                                                                       |
| [175. Perfil de un experto en Inteligencia de Negocios](#175-perfil-de-un-experto-en-inteligencia-de-negocios)                       |
| [176. ¿Qué es un base de datos?](#176-¿qué-es-un-base-de-datos)                                                                      |
| [177. Modelamiento de datos](#177-modelamiento-de-datos)                                                                             |
| [178. Modelamiento transaccional vs Modelamiento multidimensional](#178-modelamiento-transaccional-vs-modelamiento-multidimensional) |
| [179. Definición de dimensión y métricas](#179-definición-de-dimensión-y-métricas)                                                   |
| [180. Normalización de los datos](#180-normalización-de-los-datos)                                                                   |

---

# **Tutorial de SQL**

## **171. ¿Qué es inteligencia de negocios?**

La inteligencia de negocios, también conocida como business intelligence en inglés, se refiere al conjunto de procesos, tecnologías y herramientas utilizadas para recopilar, analizar y presentar datos e información empresarial de manera que permita tomar decisiones estratégicas y operativas informadas. Es un campo que combina aspectos de la gestión de datos, el análisis estadístico y la visualización de información.

La inteligencia de negocios se enfoca en convertir grandes volúmenes de datos en conocimiento útil para la toma de decisiones. A través de diversas técnicas y herramientas, se extraen, transforman y cargan los datos desde diferentes fuentes (como bases de datos, sistemas transaccionales, redes sociales, etc.) hacia un almacén centralizado llamado data warehouse. Una vez allí, los datos se organizan y se preparan para su análisis.

Luego de la etapa de preparación, los datos son analizados utilizando técnicas de minería de datos, análisis estadístico y modelado predictivo. Estas técnicas permiten identificar patrones, tendencias y relaciones ocultas en los datos, lo que brinda información valiosa para comprender el desempeño empresarial, detectar oportunidades y problemas, y tomar decisiones estratégicas.

La visualización de datos es otro aspecto clave de la inteligencia de negocios. Los resultados del análisis se presentan de manera visual a través de tableros de control interactivos, gráficos y reportes personalizados. Esto facilita la comprensión de la información y la comunicación efectiva de los hallazgos a diferentes niveles de la organización.

A continuación, te daré algunos ejemplos para ilustrar cómo se aplica la inteligencia de negocios en diferentes áreas:

1. **Ventas:** Una empresa puede utilizar la inteligencia de negocios para analizar las ventas por región, producto o cliente, identificar patrones de compra, identificar productos con mayor demanda, evaluar el rendimiento de los vendedores y pronosticar las ventas futuras.

2. **Marketing:** Una empresa puede utilizar la inteligencia de negocios para analizar el comportamiento de los clientes en campañas de marketing, identificar segmentos de mercado rentables, medir el retorno de inversión de las actividades de marketing y personalizar las estrategias de marketing en función de los perfiles de los clientes.

3. **Operaciones:** Una empresa puede utilizar la inteligencia de negocios para analizar los procesos operativos, identificar cuellos de botella o ineficiencias, optimizar la cadena de suministro, gestionar el inventario y mejorar la calidad de los productos.

4. **Recursos humanos:** Una empresa puede utilizar la inteligencia de negocios para analizar los datos del personal, como la rotación de empleados, la satisfacción laboral, el rendimiento y la productividad, para identificar tendencias y tomar decisiones informadas sobre la gestión del talento y la planificación de la fuerza laboral.

En resumen, la inteligencia de negocios es un conjunto de procesos y herramientas que permiten transformar datos en información valiosa para la toma de decisiones empresariales. Ayuda a las organizaciones a comprender su desempeño, identificar oportunidades y problemas, y tomar decisiones estratégicas basadas en datos.

![inteligencia de negocios](../../img/inteligencia%20de%20negocios.png "inteligencia de negocios")

[🔼](#índice)

---

## **172. Proceso de inteligencia de negocios**

Los procesos de inteligencia de negocios son una serie de actividades y etapas que se llevan a cabo para obtener información valiosa y aplicable a partir de los datos empresariales. Estos procesos permiten transformar datos en conocimiento accionable, que respalda la toma de decisiones estratégicas y operativas. A continuación, te explicaré cada una de las etapas del proceso de inteligencia de negocios, junto con ejemplos para ilustrar su aplicación:

1. **Extracción de datos:** En esta etapa, se recopilan los datos necesarios de diferentes fuentes, como bases de datos, sistemas transaccionales, archivos, redes sociales, entre otros. Los datos pueden ser estructurados (por ejemplo, tablas en una base de datos) o no estructurados (por ejemplo, texto libre en comentarios de redes sociales). Un ejemplo sería extraer los datos de ventas de un sistema ERP para su análisis.

2. **Transformación de datos:** Después de la extracción, los datos pueden requerir procesos de limpieza y transformación. Esto implica la estandarización, corrección de errores, eliminación de duplicados y la normalización de los datos para garantizar su calidad y coherencia. Por ejemplo, si se tienen datos de clientes en diferentes formatos y sistemas, se pueden fusionar y estandarizar para tener una única vista coherente de los clientes.

3. **Carga de datos:** En esta etapa, los datos transformados se cargan en un almacén de datos centralizado, como un data warehouse. Aquí, los datos se organizan y estructuran para facilitar su análisis. Por ejemplo, los datos de ventas, marketing y finanzas se pueden cargar en un almacén de datos común para su posterior análisis integrado.

4. **Análisis de datos:** En esta etapa, se aplican técnicas y herramientas de análisis de datos para extraer información y conocimiento relevante. Esto puede implicar el uso de técnicas de minería de datos, análisis estadístico, modelado predictivo y análisis de tendencias. Por ejemplo, se pueden utilizar técnicas de segmentación de clientes para identificar grupos de clientes con características similares y comprender mejor sus preferencias y comportamientos de compra.

5. **Visualización de datos:** Una vez que se obtienen los resultados del análisis, es importante presentarlos de manera visual y comprensible. Esto implica la creación de tableros interactivos, gráficos y reportes que permitan a los usuarios explorar los datos y extraer información relevante de manera intuitiva. Por ejemplo, se pueden crear gráficos de barras y líneas para visualizar las tendencias de ventas por producto y región.

6. **Toma de decisiones:** Finalmente, la información obtenida a través del análisis de datos se utiliza para tomar decisiones estratégicas y operativas informadas. Por ejemplo, si el análisis de datos revela que un producto específico tiene un bajo rendimiento en una región determinada, se pueden tomar decisiones sobre la estrategia de marketing o el ajuste del inventario en esa región.

Es importante destacar que estos procesos no son lineales y pueden repetirse de forma iterativa a medida que se adquiere más conocimiento y se generan nuevas preguntas o desafíos empresariales. Además, las tecnologías y herramientas de inteligencia de negocios, como los sistemas de gestión de bases de datos, los software de análisis y las plataformas de visualización, facilitan y automatizan estos procesos para agilizar el flujo de información y toma de decisiones basada en datos.

![Proceso de inteligencia de negocios](../../img/Proceso%20de%20inteligencia%20de%20negocios.png "Proceso de inteligencia de negocios")

[🔼](#índice)

---

## **173. Tradicional vs BI Moderno**

La diferencia entre el enfoque tradicional de inteligencia de negocios (BI) y el enfoque moderno de BI radica en las técnicas, tecnologías y enfoques utilizados para recopilar, analizar y presentar la información empresarial. A continuación, te explicaré las características distintivas de cada enfoque, junto con ejemplos para ilustrar las diferencias:

1. **Enfoque tradicional de BI:**

- **Recopilación de datos estructurados:** El enfoque tradicional de BI se centra principalmente en datos estructurados provenientes de fuentes internas de la empresa, como sistemas transaccionales y bases de datos. Estos datos suelen almacenarse en un almacén de datos centralizado.
- **Informes y análisis estáticos:** Se generan informes estáticos y predefinidos que se actualizan periódicamente. Estos informes siguen una estructura fija y no permiten una exploración interactiva de los datos.
- **Análisis retrospectivo:** El análisis se enfoca principalmente en comprender el desempeño pasado de la empresa. Las métricas y los indicadores clave de rendimiento (KPI) se utilizan para evaluar el rendimiento histórico.
- **Visualización limitada:** La visualización de datos suele ser básica, con gráficos simples y tablas estáticas. La interactividad y personalización son limitadas.

**Ejemplo:** En un enfoque tradicional de BI, una empresa puede generar un informe mensual de ventas que muestra las cifras de ventas por producto y región. El informe se basa en datos históricos y sigue un formato estático, sin permitir una exploración adicional o análisis interactivo.

2. **Enfoque moderno de BI:**

- **Recopilación de datos estructurados y no estructurados:** El enfoque moderno de BI incluye tanto datos estructurados como no estructurados, provenientes de diversas fuentes internas y externas a la empresa. Estos datos pueden incluir datos de redes sociales, datos de sensores, datos en tiempo real, entre otros.
- **Análisis en tiempo real:** El análisis se realiza en tiempo real o cerca de tiempo real, lo que permite tomar decisiones más rápidas y oportunas. Los informes y análisis son dinámicos y se actualizan automáticamente.
- **Análisis predictivo y prescriptivo:** Además del análisis retrospectivo, se utilizan técnicas avanzadas como el modelado predictivo y prescriptivo para predecir tendencias futuras y recomendar acciones específicas.
- **Visualización interactiva y personalizada:** Se utilizan herramientas de visualización modernas que permiten la interactividad y la personalización. Los usuarios pueden explorar los datos, realizar análisis ad hoc y crear visualizaciones personalizadas.
- **Automatización y machine learning:** Se aplican técnicas de automatización y machine learning para agilizar y optimizar los procesos de BI. Esto incluye la automatización de tareas de extracción, transformación y carga de datos, así como la detección de patrones y anomalías en los datos.

**Ejemplo:** En un enfoque moderno de BI, una empresa puede utilizar análisis en tiempo real para monitorear las menciones de su marca en las redes sociales. Se utilizan técnicas de procesamiento del lenguaje natural para extraer sentimientos y opiniones de los comentarios de los clientes en tiempo real. Los resultados se visualizan en un tablero interactivo que muestra el sentimiento general hacia la marca y permite identificar problemas o tendencias emergentes.

En resumen, el enfoque tradicional de BI se centra en datos estructurados, informes estáticos y análisis retrospectivo, mientras que el enfoque moderno de BI abarca una gama más amplia de datos, análisis en tiempo real, análisis predictivo y prescriptivo, visualización interactiva y automatización. El enfoque moderno de BI permite una toma de decisiones más ágil y basada en datos en un entorno empresarial cada vez más dinámico y complejo.

[🔼](#índice)

---

## **174. Evolución en el análisis**

El análisis ha experimentado una notable evolución a lo largo del tiempo, impulsada por los avances tecnológicos y la necesidad de comprender mejor los datos empresariales. A continuación, te proporcionaré una explicación detallada de la evolución en el análisis, junto con ejemplos que ilustran cada etapa:

1. **Análisis descriptivo:** Esta etapa inicial del análisis se centra en describir y resumir los datos existentes. Se utilizan técnicas básicas de estadística descriptiva para calcular medidas como promedios, sumas, máximos, mínimos y contar frecuencias. Los informes estáticos y los cuadros de mando se utilizan para presentar los resultados.

**Ejemplo:** Una empresa realiza un análisis descriptivo de sus ventas trimestrales, calculando la suma total de las ventas, el promedio de ventas por mes y la región con las ventas más altas.

2. **Análisis exploratorio:** En esta etapa, se busca comprender mejor los datos y descubrir patrones, tendencias y relaciones ocultas. Se utilizan técnicas como gráficos, diagramas de dispersión y análisis de correlación para explorar la relación entre las variables. El análisis exploratorio permite identificar áreas de interés y generar hipótesis para un análisis más profundo.

**Ejemplo:** Una empresa realiza un análisis exploratorio de sus datos de clientes, utilizando gráficos de dispersión para examinar la relación entre la edad de los clientes y el gasto promedio. Descubre que los clientes más jóvenes tienden a gastar menos que los clientes de mayor edad.

3. **Análisis predictivo:** En esta etapa, se utilizan técnicas estadísticas y modelos matemáticos para predecir eventos o resultados futuros. Se emplean algoritmos de aprendizaje automático (machine learning) para entrenar modelos en datos históricos y hacer predicciones basadas en nuevos datos. El análisis predictivo es útil para tomar decisiones informadas y anticiparse a las tendencias futuras.

**Ejemplo:** Una empresa utiliza el análisis predictivo para predecir la demanda de productos en función de factores como el histórico de ventas, las campañas de marketing y las condiciones económicas. Esto ayuda a la empresa a optimizar su inventario y planificar la producción de manera más eficiente.

4. **Análisis prescriptivo:** En esta etapa avanzada del análisis, se generan recomendaciones y acciones específicas basadas en los resultados del análisis. Se emplean técnicas de optimización y simulación para identificar las mejores acciones a tomar en función de diferentes escenarios y restricciones. El análisis prescriptivo ayuda a tomar decisiones más efectivas y a optimizar los resultados empresariales.

**Ejemplo:** Una empresa utiliza el análisis prescriptivo para optimizar su cadena de suministro. El análisis sugiere las rutas de envío más eficientes, el mejor momento para realizar pedidos y la asignación óptima de recursos para maximizar la eficiencia y minimizar los costos de transporte.

Es importante destacar que estas etapas del análisis no son necesariamente lineales y pueden superponerse en la práctica. Además, con los avances tecnológicos y la adopción de técnicas más avanzadas, como el análisis en tiempo real y el análisis de big data, el análisis continúa evolucionando para brindar una mayor capacidad de comprensión y toma de decisiones en el entorno empresarial.

![Evolución en el análisis](../../img/Evoluci%C3%B3n%20en%20el%20an%C3%A1lisis.webp "Evolución en el análisis")

[🔼](#índice)

---

## **175. Perfil de un experto en Inteligencia de Negocios**

El perfil de un experto en inteligencia de negocios (BI) abarca una combinación de habilidades técnicas, conocimientos de negocios y capacidad analítica. Aquí tienes una explicación detallada de las características clave y ejemplos del perfil de un experto en inteligencia de negocios:

1. **Conocimiento de negocios:** Un experto en BI debe comprender profundamente el funcionamiento de la empresa y los aspectos clave de su industria. Debe tener conocimientos de los procesos empresariales, los indicadores clave de rendimiento (KPI) relevantes y los desafíos específicos que enfrenta la organización. Esto permite al experto en BI alinear el análisis y las soluciones con los objetivos y las necesidades del negocio.

**Ejemplo:** Un experto en BI en una empresa minorista debe entender el ciclo de vida de los productos, el comportamiento del consumidor, las tendencias de la industria y los desafíos relacionados con la gestión del inventario y la fidelización de los clientes.

2. **Habilidades técnicas:** Un experto en BI debe tener habilidades técnicas sólidas para manejar las herramientas y tecnologías utilizadas en el análisis de datos y la generación de informes. Esto incluye el conocimiento de bases de datos, lenguajes de consulta (por ejemplo, SQL), herramientas de extracción y transformación de datos (por ejemplo, ETL), y herramientas de visualización y análisis de datos.

**Ejemplo:** Un experto en BI utiliza herramientas como Tableau, Power BI o QlikView para visualizar y analizar datos, y utiliza lenguajes de consulta como SQL para extraer y manipular datos de bases de datos.

3. **Capacidad analítica:** Un experto en BI debe ser capaz de analizar datos de manera efectiva para extraer información valiosa y relevante. Esto incluye habilidades en minería de datos, estadísticas, modelado predictivo y técnicas de análisis avanzadas. El experto en BI debe poder identificar patrones, tendencias y relaciones en los datos y utilizarlos para generar conocimientos accionables.

**Ejemplo:** Un experto en BI aplica técnicas de segmentación de clientes para identificar grupos de clientes con características similares y desarrollar estrategias de marketing personalizadas.

4. **Pensamiento estratégico:** Un experto en BI debe tener una visión estratégica y ser capaz de traducir los datos en información relevante para la toma de decisiones estratégicas. Debe comprender cómo los análisis y los informes pueden influir en las decisiones empresariales y ayudar a lograr los objetivos estratégicos de la organización.

**Ejemplo:** Un experto en BI utiliza análisis de datos para identificar nuevas oportunidades de mercado, evaluar la viabilidad de proyectos y desarrollar planes de acción estratégicos.

5. **Comunicación efectiva:** Un experto en BI debe tener habilidades de comunicación efectivas para traducir los resultados del análisis en informes y presentaciones comprensibles para audiencias no técnicas. Debe ser capaz de explicar los hallazgos y las recomendaciones en un lenguaje claro y persuasivo.

**Ejemplo:** Un experto en BI presenta los resultados de un análisis de mercado a la alta dirección de la empresa, explicando las conclusiones y recomendaciones de manera clara y convincente.

En resumen, un experto en inteligencia de negocios combina un conocimiento profundo del negocio, habilidades técnicas, capacidad analítica, pensamiento estratégico y habilidades de comunicación efectiva. Este perfil permite al experto en BI aprovechar los datos para generar información valiosa y apoyar la toma de decisiones basada en datos en una organización.

[🔼](#índice)

---

## **176. ¿Qué es un base de datos?**

Una base de datos es un sistema organizado y estructurado para almacenar, gestionar y recuperar grandes cantidades de información de manera eficiente. En una base de datos, los datos se organizan en tablas compuestas por filas y columnas, donde cada fila representa un registro y cada columna representa un atributo o campo de datos. A continuación, te proporcionaré una explicación detallada de los componentes y ejemplos de una base de datos:

- **Tablas:** Las tablas son la estructura fundamental de una base de datos. Cada tabla está compuesta por filas y columnas. Cada fila representa un registro único en la base de datos y contiene los valores de cada atributo correspondiente. Cada columna representa un atributo o campo específico y define el tipo de datos que se puede almacenar en esa columna.

**Ejemplo:**

Tabla "Clientes":

| ID  | Nombre | Edad | Ciudad    |
| --- | ------ | ---- | --------- |
| 1   | Ana    | 35   | Madrid    |
| 2   | Pedro  | 28   | Barcelona |
| 3   | Laura  | 42   | Valencia  |

- **Registros:** Un registro se refiere a una fila en una tabla y representa una entidad o instancia específica de información. Cada registro contiene valores para cada atributo o campo definido en la tabla.

**Ejemplo:**

En la tabla "`Clientes`", cada fila representa un registro que contiene información sobre un cliente específico. Por ejemplo, el registro con ID 1 representa a Ana, una cliente de 35 años de edad que vive en Madrid.

- **Atributos o campos:** Los atributos o campos representan las características o propiedades de una entidad que se almacenan en la base de datos. Cada campo tiene un nombre único y un tipo de datos específico que define el tipo de información que puede almacenar.

**Ejemplo:**

En la tabla "`Clientes`", los atributos o campos son "`ID`", "`Nombre`", "`Edad`" y "`Ciudad`". Cada uno de ellos almacena información específica, como el identificador del cliente, su nombre, edad y ciudad de residencia.

- **Relaciones:** Las bases de datos relacionales permiten establecer relaciones entre tablas. Estas relaciones definen cómo los registros de una tabla se relacionan con los registros de otras tablas. Las relaciones se establecen mediante claves primarias y claves externas, lo que permite acceder y combinar datos de varias tablas.

**Ejemplo:**

En una base de datos de una tienda en línea, se pueden tener dos tablas: "`Pedidos`" y "`Productos`". La tabla "`Pedidos`" puede tener un campo llamado "`ID_Producto`" que actúa como una clave externa, relacionando cada pedido con el producto correspondiente en la tabla "`Productos`".

En resumen, una base de datos es una estructura organizada que permite almacenar y gestionar grandes cantidades de información. Está compuesta por tablas que contienen registros, cada uno de los cuales contiene valores para atributos o campos específicos. Las bases de datos facilitan el almacenamiento y la recuperación eficiente de datos, así como la realización de consultas y análisis complejos sobre la información almacenada.

[🔼](#índice)

---

## **177. Modelamiento de datos**

El modelamiento de datos es el proceso de diseñar la estructura y las relaciones de una base de datos antes de su implementación. Consiste en definir y organizar los diferentes elementos de datos y establecer cómo se relacionan entre sí. El objetivo del modelamiento de datos es crear un modelo conceptual y lógico que represente de manera precisa la información que se almacenará en la base de datos. A continuación, te proporcionaré una explicación detallada del modelamiento de datos con ejemplos:

1. **Modelo conceptual:** El modelo conceptual es una representación de alto nivel de los conceptos y relaciones clave en una base de datos. Se enfoca en capturar los requisitos del negocio y las entidades principales involucradas. Utiliza diagramas de entidad-relación (DER) para representar las entidades, los atributos y las relaciones entre ellas.

**Ejemplo:**

En un sistema de gestión de biblioteca, el modelo conceptual puede incluir entidades como "`Libro`", "`Autor`" y "`Usuario`". Las entidades tendrían atributos relevantes, como "`ISBN`" y "`Título`" para un libro, "`Nombre`" y "`Apellido`" para un autor, y "`Nombre`" y "`Dirección`" para un usuario. Las relaciones entre las entidades se establecen, como la relación entre "`Libro`" y "`Autor`" que indica qué autor escribió qué libro.

2. **Modelo lógico:** El modelo lógico se centra en la estructura y el esquema de la base de datos. Traduce el modelo conceptual en una representación más técnica utilizando diagramas de modelo relacional. Define las tablas, los campos, las claves primarias, las claves externas y las restricciones de integridad referencial.

**Ejemplo:**

En el modelo lógico de la base de datos de la biblioteca, se crearían tablas como "`Libro`", "`Autor`" y "`Usuario`". Cada tabla tendría columnas correspondientes a los atributos de las entidades, como "`ISBN`" y "`Título`" para la tabla "`Libro`". Se establecerían claves primarias, como el campo "`ISBN`" en la tabla "`Libro`", y claves externas, como el campo "`AutorID`" en la tabla "`Libro`" para establecer la relación con la tabla "`Autor`".

3. **Modelo físico:** El modelo físico se refiere a la implementación real de la base de datos en un sistema de gestión de bases de datos (SGBD). Define cómo se almacenan los datos en disco, los índices utilizados para acceder a los datos de manera eficiente y otras consideraciones de rendimiento. Puede incluir detalles técnicos como el tamaño y el tipo de datos, las restricciones de almacenamiento y las optimizaciones de consultas.

**Ejemplo:**

En el modelo físico de la base de datos de la biblioteca, se especificaría el tipo de datos para cada columna, como cadenas de caracteres para los títulos de los libros o enteros para los identificadores. También se establecerían índices en campos frecuentemente utilizados en búsquedas, como el campo "`Título`" en la tabla "`Libro`", para acelerar la recuperación de datos.

En resumen, el modelamiento de datos implica el diseño y la representación de la estructura y las relaciones de una base de datos. Comienza con un modelo conceptual que captura los requisitos del negocio, luego se traduce a un modelo lógico que define la estructura de la base de datos y, finalmente, se implementa en un modelo físico que especifica los detalles técnicos de la base de datos. Este proceso garantiza una base de datos bien diseñada y organizada que puede almacenar y gestionar la información de manera efectiva.

![Modelamiento de datos](../../img/Modelamiento%20de%20datos.jpg "Modelamiento de datos")

[🔼](#índice)

---

## **178. Modelamiento transaccional vs Modelamiento multidimensional**

El modelamiento transaccional y el modelamiento multidimensional son dos enfoques diferentes utilizados en el diseño de bases de datos para satisfacer diferentes necesidades de análisis y consulta. Aquí tienes una explicación detallada de cada uno con ejemplos:

1. **Modelamiento Transaccional:**

El modelamiento transaccional se enfoca en el almacenamiento y la gestión eficiente de transacciones y operaciones diarias en una base de datos. Es adecuado para entornos donde se realizan numerosas transacciones en tiempo real y se necesita mantener la integridad de los datos. En este enfoque, los datos se almacenan en tablas normalizadas para reducir la redundancia y garantizar la integridad de los datos.

**Ejemplo:**

Imagina una base de datos de una empresa de comercio electrónico. El modelamiento transaccional se utilizaría para almacenar y gestionar las transacciones diarias, como las órdenes de compra, los registros de clientes y los detalles de los productos. Las tablas estarían diseñadas de manera normalizada para evitar la redundancia y garantizar la consistencia de los datos.

Tabla "`Órdenes de compra`":

| ID Orden | ID Cliente | Fecha      | Total   |
| -------- | ---------- | ---------- | ------- |
| 1        | 101        | 2023-06-15 | $150.00 |
| 2        | 102        | 2023-06-16 | $75.50  |
| 3        | 103        | 2023-06-17 | $200.00 |

2. **Modelamiento Multidimensional:**

El modelamiento multidimensional se utiliza en entornos de análisis de datos y se enfoca en la representación eficiente de datos para consultas y análisis complejos. Se basa en la idea de estructurar los datos en torno a dimensiones y medidas. Las dimensiones representan las características de los datos que se utilizan para realizar análisis, mientras que las medidas son los valores numéricos que se analizan.

**Ejemplo:**

En el mismo contexto de la empresa de comercio electrónico, el modelamiento multidimensional se utilizaría para el análisis de datos. Se crearía un esquema de estrella o copo de nieve que incluiría una tabla de hechos y tablas de dimensiones. La tabla de hechos contendría las medidas numéricas, como el total de ventas, mientras que las tablas de dimensiones representarían características relacionadas con las ventas, como el tiempo, los productos y los clientes.

Tabla "`Hechos - Ventas`":

| ID Producto | ID Cliente | ID Tiempo | Total Ventas |
| ----------- | ---------- | --------- | ------------ |
| 1           | 101        | 1         | $150.00      |
| 2           | 102        | 2         | $75.50       |
| 3           | 103        | 3         | $200.00      |

Tabla "`Dimensión - Tiempo`":

| ID Tiempo | Fecha      | Mes | Año  |
| --------- | ---------- | --- | ---- |
| 1         | 2023-06-15 | Jun | 2023 |
| 2         | 2023-06-16 | Jun | 2023 |
| 3         | 2023-06-17 | Jun | 2023 |

En resumen, el modelamiento transaccional se centra en el almacenamiento y la gestión eficiente de transacciones diarias, mientras que el modelamiento multidimensional se enfoca en el análisis de datos y la representación eficiente de dimensiones y medidas para consultas complejas. La elección entre ambos enfoques depende de los requisitos específicos de la aplicación y los tipos de consultas y análisis que se realizarán en la base de datos.

![Modelamiento transaccional vs Modelamiento multidimensional](../../img/Modelamiento%20transaccional%20vs%20Modelamiento%20multidimensional.webp "Modelamiento transaccional vs Modelamiento multidimensional")

[🔼](#índice)

---

## **179. Definición de dimensión y métricas**

En el contexto del análisis de datos y la modelización multidimensional, las dimensiones y las métricas desempeñan roles fundamentales en la estructuración y el análisis de la información. A continuación, te proporciono una explicación detallada de cada uno con ejemplos:

1. **Dimensión:**

En el modelamiento multidimensional, una dimensión representa una característica o una categoría que describe los datos y proporciona un contexto para su análisis. Las dimensiones son atributos cualitativos y representan los ejes principales a lo largo de los cuales se analizan los datos. Pueden incluir información sobre productos, tiempo, ubicación, clientes u otras características relevantes.

**Ejemplo:**

Supongamos que estás analizando las ventas de una tienda en línea. Algunas posibles dimensiones en este caso podrían ser:

- **Dimensión "Producto":** Categorías de productos, como electrónica, ropa, muebles, etc.
- **Dimensión "Tiempo":** Año, mes, día o día de la semana en el que se realizó la venta.
- **Dimensión "Ubicación":** Región, ciudad o país donde se realizó la venta.
- **Dimensión "Cliente":** Información sobre los clientes, como edad, género o categoría de lealtad.

2. **Métrica:**

Las métricas, también conocidas como medidas o indicadores clave de rendimiento (KPI), son valores numéricos que se utilizan para cuantificar y evaluar aspectos específicos de los datos. Representan los valores que se analizan y agregan en función de las dimensiones seleccionadas. Las métricas son atributos cuantitativos y proporcionan información cuantificable y medible.

**Ejemplo:**

Siguiendo el ejemplo anterior, algunas posibles métricas relacionadas con las ventas podrían ser:

- **Métrica "Total de Ventas":** El monto total de ventas generado en un período específico.
- **Métrica "Cantidad de Unidades Vendidas":** El número total de unidades vendidas de un producto en particular.
- **Métrica "Ingresos Promedio por Cliente":** El promedio de ingresos generado por cada cliente.
- **Métrica "Tasa de Conversión":** El porcentaje de visitantes del sitio web que realizaron una compra.

En un modelo multidimensional, las métricas se almacenan en la tabla de hechos y se asocian con las dimensiones a través de claves externas. Esto permite realizar análisis cruzados y segmentar los datos en función de las dimensiones seleccionadas.

En resumen, las dimensiones representan características cualitativas que describen los datos y proporcionan contexto, mientras que las métricas son valores numéricos que cuantifican y evalúan aspectos específicos de los datos. Al combinar dimensiones y métricas, se pueden realizar análisis multidimensionales y obtener información valiosa para la toma de decisiones en diferentes áreas de negocio.

[🔼](#índice)

---

## **180. Normalización de los datos**

La normalización de datos es un proceso en el diseño de bases de datos que se utiliza para reducir la redundancia y garantizar la integridad de los datos. Consiste en aplicar reglas y técnicas para estructurar y organizar los datos en tablas relacionales de manera eficiente. La normalización se basa en la teoría de la forma normal, que establece ciertas reglas para eliminar la redundancia y las anomalías en el diseño de la base de datos. A continuación, te proporcionaré una explicación detallada de los diferentes niveles de normalización con ejemplos:

1. **Primera Forma Normal (1NF):**

En la `1NF`, se asegura que cada columna de una tabla contenga solo valores atómicos y no haya duplicados. Además, se establece una clave primaria única para cada registro.

**Ejemplo:**

Supongamos que tenemos una tabla de clientes con la siguiente estructura:

| ID Cliente | Nombre       | Teléfonos          |
| ---------- | ------------ | ------------------ |
| 1          | Juan Pérez   | 555-1234, 555-5678 |
| 2          | María López  | 555-7890           |
| 3          | Carlos Gómez | 555-4321, 555-8765 |

Para cumplir con la `1NF`, necesitaríamos dividir la columna "`Teléfonos`" en una tabla separada y establecer una clave primaria única para cada registro:

Tabla "`Clientes`":

| ID Cliente | Nombre       |
| ---------- | ------------ |
| 1          | Juan Pérez   |
| 2          | María López  |
| 3          | Carlos Gómez |

Tabla "`Teléfonos`":

| ID Cliente | Teléfono |
| ---------- | -------- |
| 1          | 555-1234 |
| 1          | 555-5678 |
| 2          | 555-7890 |
| 3          | 555-4321 |
| 3          | 555-8765 |

2. **Segunda Forma Normal (2NF):**

En la `2NF`, se busca eliminar la dependencia parcial, lo que significa que cada columna en una tabla debe depender completamente de la clave primaria.

**Ejemplo:**

Supongamos que tenemos una tabla de pedidos con la siguiente estructura:

| ID Pedido | ID Producto | Cantidad | Precio Unitario |
| --------- | ----------- | -------- | --------------- |
| 1         | 101         | 5        | $10.00          |
| 1         | 102         | 3        | $15.00          |
| 2         | 101         | 2        | $10.00          |

En este caso, "`Precio Unitario`" depende de "`ID Producto`" y no de la clave primaria "`ID Pedido`". Para cumplir con la `2NF`, dividiríamos la tabla en dos:

Tabla "`Pedidos`":

| ID Pedido | ID Producto | Cantidad |
| --------- | ----------- | -------- |
| 1         | 101         | 5        |
| 1         | 102         | 3        |
| 2         | 101         | 2        |

Tabla "`Productos`":

| ID Producto | Another header |
| ----------- | -------------- |
| 101         | $10.00         |
| 102         | $15.00         |

3. **Tercera Forma Normal (3NF):**

En la `3NF`, se busca eliminar la dependencia transitiva, lo que significa que no debe haber dependencias entre las columnas que no sean la clave primaria.

**Ejemplo:**

Supongamos que tenemos una tabla de empleados con la siguiente estructura:

| ID Empleado | Nombre       | Departamento | Jefe Departamento |
| ----------- | ------------ | ------------ | ----------------- |
| 1           | Juan Pérez   | Ventas       | 3                 |
| 2           | María López  | Finanzas     | 3                 |
| 3           | Carlos Gómez | Gerencia     | NULL              |

En este caso, "`Jefe Departamento`" depende de "`Departamento`" y no de la clave primaria "`ID Empleado`". Para cumplir con la `3NF`, dividiríamos la tabla en dos:

Tabla "`Empleados`":

| ID Empleado | Nombre       |
| ----------- | ------------ |
| 1           | Juan Pérez   |
| 2           | María López  |
| 3           | Carlos Gómez |

Tabla "`Departamentos`":

| Departamento | Jefe Departamento |
| ------------ | ----------------- |
| Ventas       | 3                 |
| Finanzas     | 3                 |
| Gerencia     | NULL              |

En resumen, la normalización de datos es un proceso para estructurar y organizar los datos en tablas relacionales, eliminando la redundancia y garantizando la integridad de los datos. Los diferentes niveles de normalización, como la `1NF`, `2NF` y `3NF`, se basan en reglas específicas para asegurar que los datos estén bien organizados y sean fáciles de mantener y consultar.

![Normalización de los datos](../../img/Normalizaci%C3%B3n%20de%20los%20datos.jpg "Normalización de los datos")

**Modelo Copo de Nieve, Estrella y Constelación. Introducción a Datamart y Datawarehouse**

El modelo Copo de Nieve, el modelo Estrella y el modelo Constelación son tres enfoques utilizados en el diseño de bases de datos para estructurar y organizar los datos en un entorno de Data Warehouse. Además, se suele utilizar el concepto de Data Mart, que es una versión más específica y especializada de un Data Warehouse. A continuación, te proporcionaré una explicación detallada de cada uno con ejemplos:

1. **Modelo Copo de Nieve:**

El modelo Copo de Nieve es una variante del modelo Estrella que se caracteriza por tener dimensiones normalizadas en lugar de dimensiones completamente desnormalizadas. En este modelo, las dimensiones se dividen en tablas más pequeñas y se establecen relaciones entre ellas, formando una estructura similar a un copo de nieve.

**Ejemplo:**

Supongamos que tenemos un Data Warehouse para analizar las ventas de una empresa. En el modelo Copo de Nieve, la tabla de hechos principal estaría conectada a las tablas de dimensiones, y estas a su vez estarían relacionadas con tablas de subdimensiones más detalladas.

Tabla de hechos "`Ventas`":

| ID Producto | ID Cliente | ID Tiempo | Cantidad | Monto Total |
| ----------- | ---------- | --------- | -------- | ----------- |
| 1           | 101        | 1         | 5        | $100.00     |
| 2           | 102        | 2         | 3        | $50.00      |
| 3           | 103        | 3         | 2        | $30.00      |

Tabla de dimensiones "`Productos`":

| ID Producto | Nombre     | Precio Unitario |
| ----------- | ---------- | --------------- |
| 1           | Producto A | $20.00          |
| 2           | Producto B | $10.00          |
| 3           | Producto C | $15.00          |

Tabla de subdimensiones "`Categorías`":

| ID Producto | ID Producto |
| ----------- | ----------- |
| 1           | Electrónica |
| 2           | Ropa        |
| 3           | Hogar       |

2. **Modelo Estrella:**

El modelo Estrella es uno de los modelos más comunes en el diseño de Data Warehouses. En este modelo, la tabla de hechos principal está conectada directamente a las tablas de dimensiones, formando una estructura en forma de estrella. Las dimensiones están completamente desnormalizadas, lo que significa que contienen todos los atributos necesarios para el análisis.

**Ejemplo:**

Siguiendo el ejemplo anterior, en el modelo Estrella, la tabla de hechos principal estaría directamente relacionada con las tablas de dimensiones, sin tablas de subdimensiones adicionales.

Tabla de hechos "Ventas":

| ID Producto | ID Cliente | ID Tiempo | Cantidad | Monto Total |
| ----------- | ---------- | --------- | -------- | ----------- |
| 1           | 101        | 1         | 5        | $100.00     |
| 2           | 102        | 2         | 3        | $50.00      |
| 3           | 103        | 3         | 2        | $30.00      |

Tabla de dimensiones "`Productos`":

| ID Producto | Nombre     | Precio Unitario | Categoría   |
| ----------- | ---------- | --------------- | ----------- |
| 1           | Producto A | $20.00          | Electrónica |
| 2           | Producto B | $10.00          | Ropa        |
| 3           | Producto C | $15.00          | Hogar       |

3. **Modelo Constelación:**

El modelo Constelación, también conocido como modelo Copo de Nieve Extendido, combina características de los modelos Copo de Nieve y Estrella. En este modelo, algunas dimensiones pueden estar desnormalizadas en forma de estrella, mientras que otras dimensiones más detalladas pueden estar normalizadas en forma de copo de nieve.

**Ejemplo:**

Siguiendo el ejemplo anterior, en el modelo Constelación, podríamos tener una dimensión como "`Clientes`" completamente desnormalizada en forma de estrella, mientras que otra dimensión como "`Productos`" podría estar normalizada en forma de copo de nieve con una subdimensión adicional.

Tabla de hechos "`Ventas`":

| ID Producto | ID Cliente | ID Tiempo | Cantidad | Monto Total |
| ----------- | ---------- | --------- | -------- | ----------- |
| 1           | 101        | 1         | 5        | $100.00     |
| 2           | 102        | 2         | 3        | $50.00      |
| 3           | 103        | 3         | 2        | $30.00      |

Tabla de dimensiones "`Productos`":

| ID Producto | Nombre     | Precio Unitario |
| ----------- | ---------- | --------------- |
| 1           | Producto A | $20.00          |
| 2           | Producto B | $10.00          |
| 3           | Producto C | $15.00          |

Tabla de dimensiones "`Clientes`":

| ID Cliente | Nombre    | Dirección   |
| ---------- | --------- | ----------- |
| 101        | Cliente A | Dirección A |
| 102        | Cliente B | Dirección B |
| 103        | Cliente C | Dirección C |

Tabla de subdimensiones "`Categorías`":

| ID Producto | Categoría   |
| ----------- | ----------- |
| 1           | Electrónica |
| 2           | Ropa        |
| 3           | Hogar       |

En cuanto a los Data Marts y los Data Warehouses, son componentes de la arquitectura de un sistema de Business Intelligence (BI) que almacenan y organizan datos para su análisis y toma de decisiones.

- **Data Warehouse:** Es una base de datos centralizada que integra datos de diversas fuentes en un solo lugar para su análisis y generación de informes. Se utiliza para almacenar grandes volúmenes de datos históricos y proporciona una vista consolidada de los datos empresariales. Un Data Warehouse se utiliza para respaldar el análisis de datos a nivel organizacional y puede contener múltiples Data Marts.

- **Data Mart:** Es una versión más específica y especializada de un Data Warehouse. Un Data Mart se enfoca en un área o función de negocio particular, como ventas, marketing o finanzas. Al contrario que un Data Warehouse, un Data Mart contiene una selección de datos preprocesados y optimizados para el análisis de un área específica. Los Data Marts son más pequeños y más ágiles que los Data Warehouses y se pueden implementar de manera independiente o como parte de un Data Warehouse más amplio.

**Ejemplo:**

Siguiendo el ejemplo anterior, podríamos tener un Data Warehouse que almacena y consolida datos de ventas de la empresa. Dentro de este Data Warehouse, podríamos tener un Data Mart de ventas que se centra únicamente en los datos de ventas y proporciona informes y análisis específicos para el equipo de ventas. Este Data Mart de ventas contendría los datos relevantes de la tabla de hechos "`Ventas`" y las dimensiones necesarias, como "`Productos`" y "`Clientes`".

En resumen, el modelo Copo de Nieve, el modelo Estrella y el modelo Constelación son enfoques utilizados en el diseño de bases de datos para estructurar y organizar los datos en un entorno de Data Warehouse. El concepto de Data Mart se utiliza para crear subconjuntos especializados de datos dentro de un Data Warehouse para un análisis más específico en áreas de negocio particulares.

[🔼](#índice)

---

| **Inicio**            | **atrás 17**                | **Siguiente 19**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./17_Consultas_SQL.md) | [⏩](./19_Consultas_SQL.md) |
