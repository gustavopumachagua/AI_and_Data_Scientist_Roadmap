| **Inicio**            | **atrás 14**                | **Siguiente 16**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./14_Consultas_SQL.md) | [⏩](./16_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------ |
| [141. Introducción Backup y Restore DataBase](#141-introducción-backup-y-restore-database)                                     |
| [142. Cómo realizar un Backup desde Management Studio](#142-cómo-realizar-un-backup-desde-management-studio)                   |
| [143. Como restaurar un Backup](#143-como-restaurar-un-backup)                                                                 |
| [144. Cómo crear un Backup desde un Script](#144-cómo-crear-un-backup-desde-un-script)                                         |
| [145. ¿Qué es un SQL JOB? Opciones disponibles](#145-¿qué-es-un-sql-job-opciones-disponibles)                                  |
| [146. Preparando un JOB para realizar una tarea](#146-preparando-un-job-para-realizar-una-tarea)                               |
| [147. Tip para SQL Server Express: Emular un Scheduled JOB](#147-tip-para-sql-server-express-emular-un-scheduled-job)          |
| [148. Tip para SQL Server Express: Herramienta SQLCMD](#148-tip-para-sql-server-express-herramienta-sqlcmd)                    |
| [149. Cómo obtener nuestra IP Local](#149-cómo-obtener-nuestra-ip-local)                                                       |
| [150. Schedule Task para ejecutar un JOB por linea de comandos](#150-schedule-task-para-ejecutar-un-job-por-linea-de-comandos) |

---

# **Tutorial de SQL**

## **141. Introducción Backup y Restore DataBase**

Las operaciones de `Backup` y `Restore` en SQL Server son utilizadas para realizar copias de seguridad y restaurar bases de datos, respectivamente. Estas operaciones son fundamentales para garantizar la integridad y disponibilidad de los datos, y son vitales en la administración de bases de datos. A continuación, se explica detalladamente cada una de estas operaciones junto con un ejemplo utilizando la base de datos Northwind.

**Backup (Copia de seguridad):**

La operación de `Backup` se utiliza para crear una copia de seguridad de una base de datos en un punto determinado en el tiempo. Esta copia de seguridad incluye todos los datos y objetos de la base de datos, como tablas, vistas, procedimientos almacenados, etc. Los `backups` se utilizan para proteger los datos ante posibles pérdidas, ya sea por fallas de hardware, errores humanos o desastres naturales.

Ejemplo de `Backup` de la base de datos Northwind:

```
-- Crear una copia de seguridad completa de la base de datos Northwind
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
WITH FORMAT;
```

En este ejemplo, se realiza una copia de seguridad completa de la base de datos Northwind. La instrucción `BACKUP DATABASE` se utiliza para iniciar la operación de copia de seguridad, y se especifica el nombre y ubicación del archivo de respaldo (`'C:\Backup\Northwind.bak'`). El modificador `WITH FORMAT` indica que se desea sobrescribir cualquier copia de seguridad anterior y crear un nuevo archivo de respaldo.

**Restore (Restauración):**

La operación de `Restore` se utiliza para restaurar una base de datos a partir de una copia de seguridad previamente creada. Permite recuperar los datos y objetos de una base de datos en un estado anterior en caso de pérdida de datos o daños en la base de datos.

Ejemplo de Restauración de la base de datos Northwind:

```
-- Restaurar la base de datos Northwind desde una copia de seguridad
RESTORE DATABASE Northwind
FROM DISK = 'C:\Backup\Northwind.bak'
WITH REPLACE;
```

En este ejemplo, se restaura la base de datos Northwind a partir de una copia de seguridad previamente creada. La instrucción `RESTORE DATABASE` se utiliza para iniciar la operación de restauración, y se especifica el nombre y ubicación del archivo de respaldo (`'C:\Backup\Northwind.bak'`). El modificador `WITH REPLACE` indica que se desea reemplazar cualquier base de datos existente con el mismo nombre.

Es importante tener en cuenta que las operaciones de Backup y Restore deben realizarse con precaución y siguiendo las mejores prácticas de administración de bases de datos. Se recomienda realizar copias de seguridad regularmente y almacenarlas en ubicaciones seguras fuera del servidor de base de datos para garantizar la disponibilidad y recuperación de los datos en caso de un evento adverso.

En conclusión, las operaciones de `Backup` y `Restore` en SQL Server son fundamentales para garantizar la integridad y disponibilidad de los datos. El backup permite crear copias de seguridad de la base de datos en un punto determinado en el tiempo, mientras que el restore permite restaurar una base de datos a partir de una copia de seguridad previamente creada. Estas operaciones son esenciales en la administración de bases de datos y ayudan a proteger los datos ante posibles pérdidas o daños.

[🔼](#índice)

---

## **142. Cómo realizar un Backup desde Management Studio**

Para realizar un backup desde SQL Server Management Studio, sigue los siguientes pasos:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde se encuentra la base de datos Northwind.

2. En el Explorador de objetos, expande la carpeta "`Bases de datos`" y localiza la base de datos Northwind.

3. Haz clic derecho sobre la base de datos Northwind y selecciona "`Tareas`" -> "`Realizar copia de seguridad`".

4. Aparecerá la ventana "`Copia de seguridad de la base de datos`". En la pestaña "`General`", verifica que la base de datos Northwind esté seleccionada.

5. En la sección "`Configuración de copia de seguridad`", puedes especificar las siguientes opciones:

- **Tipo de copia de seguridad:** selecciona "`Copia de seguridad completa`" para realizar una copia completa de la base de datos.

- **Ubicación de salida:** selecciona el destino donde se almacenará el archivo de copia de seguridad. Puedes elegir entre un archivo local o una unidad de red.

- **Nombre y descripción del archivo:** puedes especificar un nombre para el archivo de copia de seguridad.

- **Expire después de:** puedes establecer una fecha de vencimiento para la copia de seguridad.

6. Haz clic en "`Aceptar`" para iniciar la copia de seguridad. Verás el progreso de la operación en la ventana "`Copia de seguridad de la base de datos`".

7. Una vez finalizada la copia de seguridad, recibirás una notificación indicando que se completó correctamente.

Ejemplo de Backup desde Management Studio de la base de datos Northwind:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde se encuentra la base de datos Northwind.

2. En el Explorador de objetos, expande la carpeta "`Bases de datos`" y haz clic derecho sobre la base de datos Northwind.

3. Selecciona "`Tareas`" -> "`Realizar copia de seguridad`".

4. En la ventana "`Copia de seguridad de la base de datos`", verifica que la base de datos Northwind esté seleccionada.

5. En la sección "`Configuración de copia de seguridad`", elige un destino para el archivo de copia de seguridad. Por ejemplo, selecciona "`Disco`" y luego haz clic en "`Agregar`".

6. En la ventana emergente, selecciona una ubicación local para el archivo de copia de seguridad, como "`C:\Backup\Northwind.bak`". Asegúrate de que el tipo de archivo sea "`.bak`".

7. Haz clic en "`Aceptar`" para volver a la ventana "`Copia de seguridad de la base de datos`". Verifica que el archivo de copia de seguridad aparezca en la lista.

8. Haz clic en "`Aceptar`" para iniciar la copia de seguridad. Observa el progreso en la ventana "`Copia de seguridad de la base de datos`".

9. Una vez finalizada la copia de seguridad, recibirás una notificación de que se ha completado correctamente.

Recuerda que es importante almacenar las copias de seguridad en un lugar seguro y seguir las mejores prácticas de respaldo para garantizar la disponibilidad y recuperación de los datos en caso de una pérdida.

[🔼](#índice)

---

## **143. Como restaurar un Backup**

Para restaurar un backup en SQL Server, puedes seguir los siguientes pasos:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde deseas restaurar el backup.

2. En el Explorador de objetos, expande la carpeta "`Bases de datos`" y haz clic derecho sobre ella. Selecciona "`Restaurar base de datos`".

3. En la ventana "`Restaurar base de datos`", selecciona la opción "`Dispositivo`" en la sección "`Origen`".

4. Haz clic en el botón "`Agregar`" y luego en "`Buscar`" para seleccionar el archivo de backup que deseas restaurar. Busca el archivo de backup en tu sistema de archivos y haz clic en "`Aceptar`".

5. En la sección "`Destino`", verifica que el nombre de la base de datos sea correcto. Si deseas cambiar el nombre de la base de datos, puedes hacerlo en el campo correspondiente.

6. En la sección "`Opciones de restauración`", selecciona las opciones adecuadas para tu escenario. Por ejemplo, puedes elegir sobrescribir la base de datos existente, dejar la base de datos en modo de recuperación completa, etc.

7. Haz clic en "`Aceptar`" para iniciar el proceso de restauración. Verás el progreso de la operación en la ventana "`Restaurar base de datos`".

8. Una vez completada la restauración, recibirás una notificación indicando que se ha realizado correctamente.

Ejemplo de restauración de un backup en SQL Server con la base de datos Northwind:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde deseas restaurar el backup.

2. En el Explorador de objetos, haz clic derecho sobre la carpeta "`Bases de datos`" y selecciona "`Restaurar base de datos`".

3. En la ventana "`Restaurar base de datos`", selecciona la opción "`Dispositivo`" en la sección "`Origen`".

4. Haz clic en el botón "`Agregar`" y busca el archivo de backup de la base de datos Northwind. Por ejemplo, busca el archivo "`Northwind.bak`" que has guardado previamente en tu sistema de archivos.

5. En la sección "`Destino`", verifica que el nombre de la base de datos sea "`Northwind`" o el nombre que desees utilizar para la base de datos restaurada.

6. En la sección "`Opciones de restauración`", puedes ajustar las opciones según tus necesidades. Por ejemplo, puedes sobrescribir la base de datos existente si ya existe una base de datos con el mismo nombre.

7. Haz clic en "`Aceptar`" para iniciar el proceso de restauración. Observa el progreso en la ventana "`Restaurar base de datos`".

8. Una vez finalizada la restauración, recibirás una notificación de que se ha completado correctamente. La base de datos Northwind estará disponible para su uso.

Es importante tener en cuenta que al restaurar una base de datos, se sobrescribirán los datos existentes en la base de datos objetivo. Por lo tanto, es recomendable realizar una copia de seguridad de la base de datos existente antes de realizar la restauración.

[🔼](#índice)

---

## **144. Cómo crear un Backup desde un Script**

Para crear un backup desde un script en SQL Server, puedes seguir los siguientes pasos:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde se encuentra la base de datos que deseas respaldar.

2. Abre una nueva consulta en la que escribirás el script para crear el backup.

3. Utiliza la instrucción `BACKUP DATABASE` seguida del nombre de la base de datos que deseas respaldar y la cláusula `TO DISK` seguida de la ruta y el nombre del archivo de respaldo. Por ejemplo:

```
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
```

4. Opcionalmente, puedes especificar otras opciones de respaldo como `WITH INIT` para crear un nuevo conjunto de respaldo o `WITH FORMAT` para formatear el medio de respaldo antes de realizar el respaldo. Por ejemplo:

```
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
WITH INIT, FORMAT
```

5. Ejecuta el script presionando F5 o haciendo clic en el botón "`Ejecutar`".

6. Verifica que el respaldo se haya creado correctamente y que no haya errores en la ventana "`Mensajes`".

Ejemplo de creación de un backup desde un script en SQL Server con la base de datos Northwind:

```
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
WITH INIT, FORMAT
```

En este ejemplo, se crea un respaldo de la base de datos Northwind y se guarda en el archivo '`C:\Backup\Northwind.bak`'. Se utiliza la opción `WITH INIT` para crear un nuevo conjunto de respaldo y `WITH FORMAT` para formatear el medio de respaldo.

Es importante asegurarse de tener los permisos necesarios para realizar el respaldo de la base de datos y que la ruta y el nombre del archivo de respaldo sean válidos y accesibles. También se recomienda almacenar los respaldos en ubicaciones seguras y realizar copias de seguridad de manera regular para proteger los datos de la base de datos contra pérdidas.

**Conclusión**

El proceso de respaldo y restauración de bases de datos en SQL Server es esencial para garantizar la integridad y disponibilidad de los datos. A través de la realización de respaldos periódicos, se crea una copia de seguridad de la base de datos, lo que permite recuperar los datos en caso de fallas, errores o pérdida de información. Por otro lado, la restauración de una base de datos implica volver a cargar los datos desde un respaldo previo, lo que permite restaurar la base de datos a un estado anterior.

En el caso de la base de datos Northwind, se puede realizar un respaldo utilizando el comando `BACKUP DATABASE`, como se mencionó anteriormente. Este comando permite especificar la base de datos a respaldar y la ubicación del archivo de respaldo. Además, se pueden especificar opciones adicionales, como la creación de un nuevo conjunto de respaldo o el formateo del medio de respaldo.

Por ejemplo, supongamos que queremos realizar un respaldo de la base de datos Northwind y guardarlo en el archivo '`C:\Backup\Northwind.bak`':

```
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
WITH INIT, FORMAT
```

Una vez que se ha creado un respaldo de la base de datos, es importante almacenarlo en una ubicación segura, como una unidad de disco externa o un servidor de respaldo remoto.

En el caso de necesitar restaurar la base de datos a partir de un respaldo previo, se utiliza el comando `RESTORE DATABASE`. Este comando permite especificar el nombre de la base de datos a restaurar y la ubicación del archivo de respaldo.

Por ejemplo, supongamos que queremos restaurar la base de datos Northwind a partir del archivo de respaldo '`C:\Backup\Northwind.bak`':

```
RESTORE DATABASE Northwind
FROM DISK = 'C:\Backup\Northwind.bak'
WITH REPLACE
```

Es importante tener en cuenta que al restaurar una base de datos, se sobrescribirá la versión actual de la base de datos con los datos del respaldo. Por lo tanto, se debe tener precaución al realizar esta operación, ya que puede resultar en la pérdida de datos.

En conclusión, el respaldo y la restauración de bases de datos son procesos fundamentales para garantizar la disponibilidad y la integridad de los datos en SQL Server. Realizar respaldos periódicos y almacenarlos en ubicaciones seguras ayuda a proteger los datos de posibles fallas o pérdidas. Además, la capacidad de restaurar una base de datos a partir de un respaldo proporciona una forma efectiva de recuperar datos en caso de incidentes. Es recomendable seguir buenas prácticas de respaldo y restauración, como realizar respaldos regulares, verificar la integridad de los respaldos y probar el proceso de restauración periódicamente para garantizar su eficacia.

[🔼](#índice)

---

## **145. ¿Qué es un SQL JOB? Opciones disponibles**

Un SQL Job en SQL Server es una tarea programada que se ejecuta de forma automática a intervalos regulares o en momentos específicos. Permite automatizar procesos repetitivos, como la ejecución de consultas, el mantenimiento de la base de datos, la generación de informes, entre otros. Los SQL Jobs se crean y administran a través del SQL Server Agent, que es un componente del motor de base de datos de SQL Server.

Existen varias opciones disponibles al configurar un SQL Job:

1. **Nombre del Job:** Se asigna un nombre descriptivo al Job para identificarlo fácilmente en el SQL Server Agent.

2. **Descripción:** Se puede proporcionar una descripción detallada del Job para documentar su propósito y funcionalidad.

3. **Paso(s) del Job:** Un Job puede tener uno o varios pasos, cada uno con instrucciones específicas a ejecutar. Estos pasos pueden ser comandos SQL, scripts Transact-SQL o incluso ejecutables externos.

4. **Programación:** Se establecen los criterios de programación para determinar cuándo y con qué frecuencia se ejecutará el Job. Esto incluye la opción de ejecutarlo en momentos específicos del día, días de la semana o a intervalos regulares.

5. **Notificación:** Se pueden configurar notificaciones por correo electrónico para recibir alertas cuando el Job se complete, falle o requiera atención.

6. **Opciones avanzadas:** Existen opciones adicionales que permiten controlar el comportamiento del Job, como la gestión de errores, la asignación de recursos, la ejecución en diferentes entornos, entre otras.

Un ejemplo con la base de datos Northwind podría ser la creación de un SQL Job que se ejecute diariamente para realizar una copia de seguridad de la base de datos. El Job tendría los siguientes pasos:

1. **Paso 1:** Ejecutar el comando `BACKUP DATABASE` para crear un respaldo de la base de datos Northwind en una ubicación específica.

```
BACKUP DATABASE Northwind
TO DISK = 'C:\Backup\Northwind.bak'
WITH INIT, FORMAT
```

2. **Paso 2:** Enviar una notificación por correo electrónico para informar sobre el éxito o el fracaso del respaldo.
   El Job se programaría para ejecutarse todos los días a una hora específica, como las 2:00 a.m. Si el respaldo se completa con éxito, se enviará un correo electrónico al administrador del sistema. En caso de que ocurra algún error durante el respaldo, se enviará un correo electrónico de notificación para tomar medidas adecuadas.

Los SQL Jobs proporcionan una forma conveniente de automatizar tareas recurrentes en SQL Server, lo que ahorra tiempo y reduce la posibilidad de errores humanos. Con la capacidad de programar y monitorear los Jobs a través del SQL Server Agent, los administradores de bases de datos pueden mantener y administrar eficientemente sus bases de datos y procesos relacionados.

---

[🔼](#índice)

## **146. Preparando un JOB para realizar una tarea**

Para preparar un SQL Job en SQL Server y realizar una tarea específica, como ejecutar un script o una consulta de forma automatizada, puedes seguir los siguientes pasos:

1. Abrir SQL Server Management Studio (SSMS) y conectarse a la instancia de SQL Server donde deseas configurar el Job.

2. En el Explorador de objetos, expande la carpeta "`SQL Server Agent`" y haz clic derecho en "`Jobs`". Luego selecciona "`Nuevo trabajo`" para crear un nuevo Job.

3. En la ventana "`Propiedades del trabajo`", proporciona un nombre descriptivo y opcionalmente una descripción para el Job.

4. En la pestaña "`Paso`", haz clic en "`Nuevo`" para agregar un paso al Job. En el campo "`Nombre del paso`", ingresa un nombre descriptivo para el paso. En el campo "`Tipo de paso`", selecciona "`Transact-SQL script (T-SQL)`". A continuación, en el campo "`Comando T-SQL`", ingresa el script o la consulta que deseas ejecutar.

5. Si es necesario, puedes agregar más pasos al Job haciendo clic en "`Nuevo`" nuevamente y siguiendo los mismos pasos descritos en el paso anterior.

6. En la pestaña "`Programación`", establece los criterios de programación para determinar cuándo y con qué frecuencia se ejecutará el Job. Puedes programar el Job para que se ejecute en momentos específicos del día, días de la semana o a intervalos regulares.

7. En la pestaña "`Notificaciones`", puedes configurar notificaciones por correo electrónico para recibir alertas cuando el Job se complete, falle o requiera atención. Puedes especificar las direcciones de correo electrónico de los destinatarios, el asunto y el cuerpo del correo electrónico.

8. Haz clic en "`Aceptar`" para guardar la configuración del Job.

Una vez que hayas creado y configurado el Job, se ejecutará automáticamente según la programación establecida. Puedes monitorear el estado y los resultados del Job en el SQL Server Agent.

Ejemplo de creación de un Job en la base de datos Northwind:

Supongamos que deseas ejecutar una consulta que obtiene la cantidad total de productos vendidos por cada categoría en la tabla "`Products`" de la base de datos Northwind. A continuación, se muestra cómo configurar un Job para ejecutar esta consulta diariamente a las 9:00 a.m. y enviar los resultados por correo electrónico:

1. Abre SQL Server Management Studio y conéctate a la instancia de SQL Server donde se encuentra la base de datos Northwind.

2. Expande la carpeta "`SQL Server Agent`" en el Explorador de objetos y haz clic derecho en "`Jobs`". Luego, selecciona "`Nuevo trabajo`" para crear un nuevo Job.

3. En la ventana "`Propiedades del trabajo`", ingresa un nombre descriptivo como "`Job_Ventas_Productos`".

4. En la pestaña "`Paso`", haz clic en "`Nuevo`" para agregar un paso al Job. Ingresa un nombre descriptivo para el paso, como "`Obtener ventas por categoría`". En el campo "`Tipo de paso`", selecciona "`Transact-SQL script (T-SQL)`". A continuación, ingresa la siguiente consulta en el campo "`Comando T-SQL`":

```
SELECT c.CategoryName, SUM(od.Quantity) AS TotalSales
FROM Categories c
JOIN Products p ON c.CategoryID = p.CategoryID
JOIN [Order Details] od ON p.ProductID = od.ProductID
GROUP BY c.CategoryName
```

5. En la pestaña "`Programación`", establece la programación del Job. Haz clic en "`Nuevo`" para crear una nueva programación y selecciona "`Diariamente`". Establece la hora de inicio en 09:00:00.

6. En la pestaña "`Notificaciones`", selecciona la opción "`Correo electrónico`" y proporciona las direcciones de correo electrónico de los destinatarios. Puedes personalizar el asunto y el cuerpo del correo electrónico según tus necesidades.

7. Haz clic en "`Aceptar`" para guardar el Job.

A partir de este momento, el Job "`Job_Ventas_Productos`" se ejecutará diariamente a las 9:00 a.m. y enviará los resultados de la consulta por correo electrónico a los destinatarios especificados. Puedes verificar el estado y los resultados del Job en el SQL Server Agent.

Recuerda que los SQL Jobs brindan una forma conveniente de automatizar tareas en SQL Server, lo que ayuda a mejorar la eficiencia y reducir errores al programar y ejecutar procesos recurrentes.

---

[🔼](#índice)

## **147. Tip para SQL Server Express: Emular un Scheduled JOB**

En SQL Server Express, que es una edición de SQL Server más ligera y con algunas limitaciones, no se incluye la funcionalidad de SQL Server Agent, que permite programar y ejecutar Jobs de forma automatizada. Sin embargo, es posible emular un Scheduled Job utilizando otras herramientas y técnicas. A continuación, se presenta un tip para emular un Scheduled Job en SQL Server Express:

1. **Crear un Script de T-SQL:** El primer paso es crear el script de T-SQL que contiene la tarea que deseas programar. Por ejemplo, supongamos que deseas ejecutar una consulta para obtener el total de ventas diarias en la tabla "`Orders`" de la base de datos Northwind. El script puede ser similar al siguiente:

```
SELECT CONVERT(date, OrderDate) AS Fecha, SUM(Total) AS TotalVentas
FROM Orders
GROUP BY CONVERT(date, OrderDate)
```

2. **Crear un archivo de Script:** Crea un archivo de texto (.sql) y guarda el script de T-SQL en él. Por ejemplo, guarda el script anterior en un archivo llamado "`TotalVentasDiarias.sql`".

3. **Programar la ejecución del Script:** Para programar la ejecución del script de T-SQL, puedes utilizar el Programador de tareas de Windows. Sigue estos pasos:

**a.** Abre el Programador de tareas de Windows. Puedes acceder a él desde el menú de inicio o mediante la ejecución del comando "`taskschd.msc`".

**b.** Haz clic en "`Crear tarea básica`" en el panel de acciones.

**c.** Proporciona un nombre y una descripción para la tarea.

**d.** Establece la frecuencia con la que deseas ejecutar la tarea (diariamente, semanalmente, mensualmente, etc.).

**e.** Selecciona "`Iniciar un programa`" como acción.

**f.** En el campo "`Programa o script`", proporciona la ruta del ejecutable "`sqlcmd.exe`", que generalmente se encuentra en la ubicación "`C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn`".

**g.** En el campo "`Agregar argumentos`", proporciona los siguientes argumentos:

`-S <nombre_servidor> -d <nombre_base_datos> -U <nombre_usuario> -P <contraseña> -i <ruta_archivo_sql>`

Reemplaza `<nombre_servidor>`, `<nombre_base_datos>`, `<nombre_usuario>`, `<contraseña>` y `<ruta_archivo_sql>` con los valores correspondientes. Por ejemplo:

`-S localhost -d Northwind -U sa -P miContraseña -i "C:\Scripts\TotalVentasDiarias.sql"`

**h.** Haz clic en "`Siguiente`" y luego en "`Finalizar`" para completar la creación de la tarea programada.

4. **Verificar y monitorear:** Una vez programada la tarea, el Programador de tareas de Windows se encargará de ejecutar el script de T-SQL según la programación establecida. Puedes verificar y monitorear la ejecución revisando los registros en la tabla "`sysjobhistory`" de la base de datos "`msdb`".

Es importante tener en cuenta que esta técnica emula un Scheduled Job en SQL Server Express, pero no proporciona todas las funcionalidades y características avanzadas que ofrece el SQL Server Agent en las ediciones completas de SQL Server. Sin embargo, puede ser una solución práctica y sencilla para programar y automatizar tareas en entornos SQL Server Express.

---

[🔼](#índice)

## **148. Tip para SQL Server Express: Herramienta SQLCMD**

La herramienta SQLCMD es una utilidad de línea de comandos que viene incluida con SQL Server Express. Proporciona una forma interactiva de ejecutar comandos y scripts de Transact-SQL (T-SQL) directamente desde la línea de comandos o mediante scripts de archivo.

Aquí tienes un tip para utilizar la herramienta SQLCMD en SQL Server Express:

1. **Abrir una ventana de comandos:** Para comenzar, abre una ventana de comandos en tu sistema operativo. Puedes hacerlo buscando "`cmd`" en el menú de inicio y seleccionando la opción "`Command Prompt`".

2. **Ejecutar SQLCMD:** En la ventana de comandos, ejecuta el comando "`sqlcmd`" para iniciar la herramienta `SQLCMD`. Puede ser necesario proporcionar la ruta completa del ejecutable dependiendo de la configuración de tu sistema. Por ejemplo, la ruta típica en un entorno de Windows sería: "`C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn\sqlcmd.exe`".

3. **Conectar a la base de datos:** Una vez que la herramienta `SQLCMD` se haya iniciado, puedes conectarte a una base de datos específica utilizando el siguiente comando:

`sqlcmd -S <nombre_servidor> -d <nombre_base_datos> -U <nombre_usuario> -P <contraseña>`

Reemplaza `<nombre_servidor>`, `<nombre_base_datos>`, `<nombre_usuario>` y `<contraseña>` con los valores correspondientes para tu entorno. Por ejemplo:

`sqlcmd -S localhost -d Northwind -U sa -P miContraseña`

4. **Ejecutar comandos y scripts:** Una vez conectado a la base de datos, puedes ejecutar comandos y scripts de T-SQL directamente desde la herramienta SQLCMD. Por ejemplo, puedes ejecutar consultas SELECT, INSERT, UPDATE, DELETE, entre otras.

Ejemplo de consulta SELECT:

`SELECT * FROM Customers;`

Ejemplo de script de archivo:

Supongamos que tienes un archivo llamado "`script.sql`" que contiene el siguiente código T-SQL:

`SELECT * FROM Orders WHERE CustomerID = 'ALFKI';`

Para ejecutar este script desde la herramienta `SQLCMD`, utiliza el siguiente comando:

`:r script.sql`

Este comando cargará y ejecutará el contenido del archivo "`script.sql`" en la base de datos actualmente conectada.

La herramienta `SQLCMD` también proporciona opciones adicionales, como guardar resultados en archivos, formatear la salida, cambiar el modo de autenticación, entre otros. Puedes explorar más detalles y opciones ejecutando el comando "`sqlcmd -?`" para obtener la lista completa de comandos y argumentos disponibles.

En resumen, la herramienta `SQLCMD` en SQL Server Express es una utilidad poderosa para ejecutar comandos y scripts de T-SQL desde la línea de comandos. Te permite interactuar con la base de datos, realizar consultas y automatizar tareas mediante scripts de archivo. Es una opción práctica para administrar y trabajar con bases de datos SQL Server Express.

---

[🔼](#índice)

## **149. Cómo obtener nuestra IP Local**

Para obtener la dirección IP local en SQL Server, puedes utilizar la función incorporada `HOST_NAME()` junto con la función `sys.dm_exec_connections`. Aquí tienes una explicación detallada con un ejemplo utilizando la base de datos Northwind:

1. **Conexión a la base de datos:** Primero, abre SQL Server Management Studio (`SSMS`) y conéctate a tu instancia de SQL Server.

2. **Ejecutar la consulta:** En la ventana de consultas de `SSMS`, ejecuta la siguiente consulta:

```
SELECT c.client_net_address AS [IP Address]
FROM sys.dm_exec_connections AS c
WHERE session_id = @@SPID;
```

Esta consulta utilizará la función `sys.dm_exec_connections` para obtener información sobre las conexiones activas en el servidor. La cláusula `WHERE session_id = @@SPID` se utiliza para filtrar las conexiones relacionadas con la sesión actual.

3.**Interpretar el resultado:** La consulta devolverá la dirección IP local en la columna "`IP Address`". La dirección IP se mostrará en formato hexadecimal. Debes interpretarla en formato decimal para obtener la dirección IP legible. Por ejemplo, si el resultado es `0x0100007F`, esto se traduce en la dirección `IP 127.0.0.1`.

Es importante tener en cuenta que esta consulta devolverá la dirección IP local de la conexión actual. Si tienes múltiples conexiones activas, puede ser necesario ajustar la consulta para obtener la dirección IP de una conexión específica.

Recuerda que esta consulta se ejecuta en el contexto de la base de datos actualmente conectada, en este caso, la base de datos Northwind. Asegúrate de haber seleccionado la base de datos correcta antes de ejecutar la consulta.

En resumen, puedes utilizar la función `HOST_NAME()` junto con `sys.dm_exec_connections` para obtener la dirección IP local en SQL Server. Esto puede ser útil para identificar la IP desde la cual se está realizando una conexión a la base de datos y realizar tareas de monitoreo o auditoría.

---

[🔼](#índice)

## **150. Schedule Task para ejecutar un JOB por linea de comandos**

Para programar la ejecución de un JOB en SQL Server mediante una tarea programada (`Scheduled Task`) utilizando la línea de comandos, puedes seguir los siguientes pasos:

1. **Crear un archivo por lotes (batch file):** Crea un archivo de texto con extensión `.bat` que contendrá los comandos necesarios para ejecutar el JOB. Puedes utilizar cualquier editor de texto para crear este archivo.

2. **Abrir el editor de texto y escribir los comandos:** Abre el archivo `.bat` con un editor de texto y escribe los comandos necesarios para ejecutar el JOB de SQL Server. Por ejemplo, el contenido del archivo podría ser el siguiente:

`sqlcmd -S <nombre_servidor> -d <nombre_base_datos> -E -Q "EXEC msdb.dbo.sp_start_job N'<nombre_job>';"`

Asegúrate de reemplazar `<nombre_servidor>`, `<nombre_base_datos>` y `<nombre_job>` con los valores correspondientes para tu entorno.

- `<nombre_servidor>`: es el nombre de tu servidor de SQL Server.
- `<nombre_base_datos>`: es el nombre de la base de datos en la que se encuentra el JOB.
- `<nombre_job>`: es el nombre del JOB que deseas ejecutar.

3. **Guardar y cerrar el archivo:** Una vez que hayas escrito los comandos, guarda y cierra el archivo.

4. **Configurar la tarea programada (Scheduled Task):** Abre el Programador de tareas en tu sistema operativo y crea una nueva tarea programada.

5. **Configurar la acción:** En la configuración de la tarea programada, especifica la acción a realizar. Selecciona la opción "`Iniciar un programa`" o similar y proporciona la ruta completa del archivo `.bat` que creaste en el paso `1`.

6. **Configurar la programación:** Establece la programación según tus necesidades. Puedes configurar la frecuencia, el día y la hora en que deseas que se ejecute el archivo `.bat`.

7. **Guardar y finalizar:** Una vez que hayas configurado todas las opciones necesarias, guarda la tarea programada.

Cuando se active la tarea programada, el archivo `.bat` se ejecutará y ejecutará el comando `sqlcmd` para iniciar el JOB especificado en SQL Server.

Recuerda que debes asegurarte de tener el comando `sqlcmd` disponible en tu sistema y que el archivo `.bat` tenga los permisos adecuados para ser ejecutado.

Este enfoque te permite programar la ejecución de un JOB en SQL Server utilizando una tarea programada y la línea de comandos. Esto puede ser útil si deseas automatizar la ejecución regular de un JOB sin tener que acceder manualmente a SQL Server Management Studio.

**Conclusión**

Los Scheduled Jobs (tareas programadas) en SQL Server son una funcionalidad clave que permite automatizar y programar la ejecución de tareas en la base de datos de manera periódica. Estas tareas pueden incluir procesos de mantenimiento, generación de informes, actualizaciones de datos, entre otros. En resumen, los Scheduled Jobs permiten ejecutar de forma automática y programada ciertas operaciones en la base de datos sin la necesidad de intervención manual.

La creación de un Scheduled Job implica los siguientes pasos:

1. **Definir la tarea:** Primero, se debe identificar y definir la tarea que se desea programar. Puede ser un procedimiento almacenado, un script SQL o cualquier otro tipo de operación que se deba realizar de forma periódica.

2. **Crear el Job:** Se crea un nuevo Job en SQL Server utilizando SQL Server Management Studio u otras herramientas administrativas. El Job incluirá información como el nombre, la descripción y las opciones de ejecución.

3. **Configurar la programación:** Se establece la programación para el Job, definiendo la frecuencia y el horario en el cual se desea que se ejecute la tarea. Esto puede ser diario, semanal, mensual u otro intervalo personalizado.

4. **Definir las acciones:** Se especifica la acción que se realizará al ejecutarse el Job. Esto puede incluir la ejecución de un script SQL, un procedimiento almacenado, la ejecución de un paquete SSIS, entre otros.

5. **Configurar notificaciones y alertas (opcional):** Si se desea recibir notificaciones o alertas por correo electrónico cuando ocurran eventos específicos durante la ejecución del Job, se pueden configurar estas opciones.

6. **Guardar y habilitar el Job:** Finalmente, se guarda el Job y se habilita para que comience a ejecutarse según la programación establecida.

Un ejemplo con la base de datos Northwind podría ser la creación de un Scheduled Job para generar un informe diario de ventas. El Job se programaría para ejecutarse todos los días a una determinada hora y ejecutaría un script SQL que recopila los datos de ventas del día anterior y genera un informe en formato PDF. Luego, se podría configurar una notificación por correo electrónico para enviar el informe a los destinatarios designados.

Los Scheduled Jobs son una herramienta poderosa para automatizar tareas recurrentes en SQL Server y garantizar la consistencia y eficiencia de las operaciones en la base de datos. Con la planificación adecuada y la configuración correcta, los Jobs pueden simplificar la administración y el mantenimiento de la base de datos, liberando tiempo y recursos para otras tareas críticas.

Es importante tener en cuenta que la configuración y administración de los Scheduled Jobs requiere permisos adecuados y un conocimiento sólido de SQL Server. Además, es fundamental monitorear y revisar regularmente los Jobs para garantizar que se estén ejecutando correctamente y ajustar la configuración según sea necesario.

En resumen, los Scheduled Jobs en SQL Server permiten automatizar y programar tareas recurrentes en la base de datos, lo que mejora la eficiencia, la productividad y la confiabilidad del sistema. Al utilizar los Jobs de manera efectiva, los administradores de bases de datos pueden optimizar las operaciones y enfocarse en tareas estratégicas para garantizar el correcto funcionamiento de la base de datos.

---

[🔼](#índice)

| **Inicio**            | **atrás 14**                | **Siguiente 16**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./14_Consultas_SQL.md) | [⏩](./16_Consultas_SQL.md) |
