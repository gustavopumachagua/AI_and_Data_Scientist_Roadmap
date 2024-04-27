| **Inicio**            | **atrás 15**                | **Siguiente 17**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./15_Consultas_SQL.md) | [⏩](./17_Consultas_SQL.md) |

---

## **Índice**

| Temario                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------- |
| [151. Administración de usuarios, roles, shemas y permisos](#151-administración-de-usuarios-roles-shemas-y-permisos)          |
| [152. Usuarios y Logins](#152-usuarios-y-logins)                                                                              |
| [153. Roles de Base de Datos: tipos posibles](#153-roles-de-base-de-datos-tipos-posibles)                                     |
| [154. Crear y asignar un Rol a un Usuario desde T-SQL](#154-crear-y-asignar-un-rol-a-un-usuario-desde-t-sql)                  |
| [155. ¿Qué es un Schema? – Como asignar un esquema a un objeto](#155-¿qué-es-un-schema-–-como-asignar-un-esquema-a-un-objeto) |
| [156. Descripción de Roles de Servidor y Roles Predefinidos](#156-descripción-de-roles-de-servidor-y-roles-predefinidos)      |
| [157. SQL SERVER Profiler](#157-sql-server-profiler)                                                                          |
| [158. Conociendo la herramienta](#158-conociendo-la-herramienta)                                                              |
| [159. Como monitorear procesos por tiempo de ejecución](#159-como-monitorear-procesos-por-tiempo-de-ejecución)                |
| [160. Definiendo templates para monitoreo](#160-definiendo-templates-para-monitoreo)                                          |

---

# **Tutorial de SQL**

## **151. Administración de usuarios, roles, shemas y permisos**

La administración de usuarios, roles, esquemas y permisos en SQL Server es fundamental para garantizar la seguridad y el control de acceso a la base de datos. Estos elementos permiten gestionar quién puede acceder a la base de datos, qué acciones pueden realizar y en qué objetos pueden operar. A continuación, explicaré cada uno de estos conceptos en detalle, junto con ejemplos utilizando la base de datos Northwind.

1. **Usuarios:** Un usuario en SQL Server es una entidad que representa a una persona o aplicación que interactúa con la base de datos. Cada usuario tiene un nombre de inicio de sesión (`login`) y un nombre de usuario en la base de datos. El inicio de sesión se utiliza para autenticar al usuario en el servidor, mientras que el nombre de usuario se utiliza para asociar permisos y roles en la base de datos.

Ejemplo: Para crear un nuevo usuario llamado "`John`" en la base de datos Northwind, se puede utilizar la siguiente instrucción:

```
CREATE LOGIN John WITH PASSWORD = 'Password123';
USE Northwind;
CREATE USER John FOR LOGIN John;
```

2. **Roles:** Los roles en SQL Server son grupos lógicos que contienen usuarios y se utilizan para simplificar la asignación de permisos. Los roles pueden tener permisos asignados y los usuarios pueden ser miembros de uno o varios roles. Esto permite administrar los permisos de forma más eficiente y centralizada.

Ejemplo: Para crear un nuevo rol llamado "`Vendedor`" en la base de datos Northwind y asignarle el usuario "`John`", se puede utilizar la siguiente instrucción:

```
USE Northwind;
CREATE ROLE Vendedor;
ALTER ROLE Vendedor ADD MEMBER John;
```

3. **Esquemas:** Los esquemas en SQL Server son contenedores lógicos que agrupan objetos de la base de datos, como tablas, vistas, funciones, etc. Los esquemas se utilizan para organizar y estructurar los objetos en la base de datos. También se pueden utilizar para asignar permisos a nivel de esquema, lo que facilita la gestión de permisos.

Ejemplo: Para crear un nuevo esquema llamado "`Ventas`" en la base de datos Northwind y asignarle permisos al rol "`Vendedor`", se puede utilizar la siguiente instrucción:

```
USE Northwind;
CREATE SCHEMA Ventas;
GRANT SELECT, INSERT, UPDATE, DELETE ON SCHEMA::Ventas TO Vendedor;
```

4. **Permisos:** Los permisos en SQL Server determinan qué acciones pueden realizar los usuarios y roles en los objetos de la base de datos. Los permisos se asignan a nivel de objeto y pueden incluir permisos de lectura, escritura, modificación de esquemas, eliminación, entre otros. Se pueden asignar permisos directamente a usuarios o roles, o a través de la asignación de permisos a nivel de esquema.

Ejemplo: Para asignar permisos de lectura y escritura en la tabla "`Customers`" a un usuario específico llamado "`John`", se puede utilizar la siguiente instrucción:

```
USE Northwind;
GRANT SELECT, INSERT, UPDATE ON Customers TO John;
```

En resumen, la administración de usuarios, roles, esquemas y permisos en SQL Server es esencial para garantizar la seguridad y el control de acceso a la base de datos. Estos elementos permiten gestionar quién puede acceder a la base de datos, qué acciones pueden realizar y en qué objetos pueden operar. Al utilizar adecuadamente estos componentes, se logra una administración eficiente y segura de la base de datos, protegiendo la integridad y confidencialidad de los datos.

---

[🔼](#índice)

## **152. Usuarios y Logins**

En SQL Server, los usuarios y logins son dos conceptos relacionados pero distintos que se utilizan para gestionar el acceso a la base de datos. A continuación, explicaré cada uno de ellos en detalle, junto con ejemplos utilizando la base de datos Northwind.

1. **Logins:** Un login en SQL Server es una identidad utilizada para autenticar a un usuario en el servidor. Representa una cuenta de inicio de sesión que puede ser utilizada para acceder al servidor de base de datos. Los logins pueden ser de diferentes tipos, como logins de Windows, logins de SQL Server o logins de Active Directory.

Ejemplo: Para crear un nuevo login de SQL Server llamado "`mylogin`" con una contraseña, se puede utilizar la siguiente instrucción:

```
USE master;
CREATE LOGIN mylogin WITH PASSWORD = 'Password123';
```

2. **Usuarios:** Un usuario en SQL Server está asociado a un login y se utiliza para controlar el acceso a una base de datos específica. Un usuario se crea en el contexto de una base de datos y se asocia con un login existente en el servidor. Cada usuario en una base de datos tiene sus propios permisos y derechos de acceso.

Ejemplo: Para crear un nuevo usuario llamado "`myuser`" asociado al login "`mylogin`" en la base de datos Northwind, se puede utilizar la siguiente instrucción:

```
USE Northwind;
CREATE USER myuser FOR LOGIN mylogin;
```

Es importante tener en cuenta que el login se crea en el nivel del servidor y puede tener acceso a múltiples bases de datos, mientras que el usuario se crea en el contexto de una base de datos específica y solo tiene acceso a esa base de datos.

En resumen, los logins y usuarios en SQL Server se utilizan para gestionar el acceso y autenticación de los usuarios en el servidor y en las bases de datos respectivamente. Los logins representan las cuentas de inicio de sesión utilizadas para autenticar a los usuarios en el servidor, mientras que los usuarios están asociados a logins y tienen permisos y derechos de acceso en una base de datos específica.

---

[🔼](#índice)

## **153. Roles de Base de Datos: tipos posibles**

En SQL Server, los roles de base de datos son un mecanismo utilizado para agrupar usuarios y asignarles permisos de manera más eficiente. Los roles permiten simplificar la administración de permisos al asignarlos a un grupo de usuarios en lugar de hacerlo individualmente. A continuación, explicaré algunos de los tipos de roles de base de datos disponibles en SQL Server, junto con ejemplos utilizando la base de datos Northwind.

1. **Roles predefinidos:**

- **db_owner:** Este rol tiene todos los permisos en la base de datos y puede realizar cualquier operación.
- **db_datareader:** Este rol permite leer todos los datos en la base de datos.
- **db_datawriter:** Este rol permite escribir datos en la base de datos.

Ejemplo: Para agregar un usuario llamado "`myuser`" al rol predefinido "`db_datareader`" en la base de datos Northwind, se puede utilizar la siguiente instrucción:

```
USE Northwind;
EXEC sp_addrolemember 'db_datareader', 'myuser';
```

2. **Roles personalizados:**

Además de los roles predefinidos, es posible crear roles personalizados para adaptarse a las necesidades específicas de la aplicación. Los roles personalizados se pueden utilizar para agrupar usuarios y asignarles permisos de manera coherente.

Ejemplo: Para crear un rol personalizado llamado "`myrole`" en la base de datos Northwind, se puede utilizar la siguiente instrucción:

```
USE Northwind;
CREATE ROLE myrole;
```

3. **Roles de aplicación:**

Los roles de aplicación se utilizan para asignar permisos a aplicaciones en lugar de usuarios individuales. Esto permite controlar los permisos de manera centralizada para todas las instancias de la aplicación.

Ejemplo: Para agregar un usuario de aplicación llamado "`myappuser`" al rol de aplicación "`myapprole`" en la base de datos Northwind, se puede utilizar la siguiente instrucción:

```
USE Northwind;
EXEC sp_addapprole 'myapprole', 'password123';
```

Es importante tener en cuenta que los roles pueden ser anidados, lo que significa que un rol puede contener otros roles. Esto permite una gestión de permisos más granular y organizada.

En resumen, los roles de base de datos en SQL Server permiten agrupar usuarios y asignarles permisos de manera eficiente. Los roles predefinidos ofrecen un conjunto de permisos comunes, mientras que los roles personalizados y de aplicación se utilizan para adaptarse a las necesidades específicas de la aplicación. Al utilizar roles, se simplifica la administración de permisos al asignarlos a grupos de usuarios en lugar de hacerlo individualmente.

---

[🔼](#índice)

## **154. Crear y asignar un Rol a un Usuario desde T-SQL**

Para crear y asignar un rol a un usuario en SQL Server utilizando T-SQL, puedes seguir los siguientes pasos:

1. **Crear el rol:**

Utiliza la instrucción `CREATE ROLE` para crear un nuevo rol en la base de datos deseada. Puedes especificar los permisos que deseas asignar al rol según tus necesidades.

Ejemplo:

```
USE Northwind;
CREATE ROLE MyRole;
```

2. **Agregar el usuario al rol:**

Utiliza la instrucción `ALTER ROLE` para agregar un usuario existente al rol recién creado.

Ejemplo:

```
USE Northwind;
ALTER ROLE MyRole ADD MEMBER myuser;
```

En el ejemplo anterior, myuser es el nombre del usuario al que deseas asignar el rol `MyRole`.

3. **Asignar permisos al rol:**

Utiliza la instrucción `GRANT` para asignar los permisos deseados al rol. Puedes otorgar permisos a nivel de objeto (tablas, vistas, procedimientos almacenados, etc.) o permisos a nivel de base de datos.

Ejemplo:

```
USE Northwind;
GRANT SELECT, INSERT, UPDATE ON Customers TO MyRole;
```

En el ejemplo anterior, se otorgan permisos de `SELECT`, `INSERT` y `UPDATE` en la tabla `Customers` al rol `MyRole`.

Recuerda que debes tener los permisos adecuados para crear roles y asignarlos a usuarios. Además, asegúrate de reemplazar "`Northwind`" con el nombre de tu base de datos.

Al asignar un rol a un usuario, este heredará los permisos del rol y podrá realizar las operaciones permitidas por ese rol en la base de datos.

Es importante tener en cuenta que los roles también se pueden asignar a roles existentes, lo que permite una estructura de roles jerárquica y más compleja según sea necesario.

Ten en cuenta que este es solo un ejemplo y debes adaptarlo a tus necesidades específicas y a la estructura de tu base de datos.

---

[🔼](#índice)

## **155. ¿Qué es un Schema? – Como asignar un esquema a un objeto**

En SQL Server, un esquema (`schema`) es un contenedor lógico que se utiliza para organizar y agrupar objetos de base de datos, como tablas, vistas, funciones, procedimientos almacenados, etc. Proporciona una forma de estructurar y separar los objetos en la base de datos, lo que facilita la administración y el mantenimiento del sistema.

Cada base de datos en SQL Server puede contener múltiples esquemas, y cada esquema puede contener varios objetos. Los esquemas proporcionan una forma de organizar y separar los objetos según su propósito o función, lo que facilita su gestión y el control de acceso.

Para asignar un esquema a un objeto en SQL Server, puedes seguir los siguientes pasos:

1. **Crear un esquema:**

Utiliza la instrucción `CREATE SCHEMA` para crear un nuevo esquema en la base de datos deseada.

Ejemplo:

```
USE Northwind;
CREATE SCHEMA MySchema;
```

2. **Asignar un objeto a un esquema:**

Puedes asignar un objeto a un esquema específico durante la creación del objeto o modificar el esquema de un objeto existente utilizando la instrucción `ALTER SCHEMA`.

Ejemplo:

```
USE Northwind;
CREATE TABLE MySchema.MyTable (
    ID INT PRIMARY KEY,
    Name VARCHAR(50)
);
```

En el ejemplo anterior, se crea una nueva tabla llamada `MyTable` y se asigna al esquema `MySchema`.

También puedes modificar el esquema de un objeto existente utilizando la instrucción `ALTER SCHEMA`.

Ejemplo:

```
USE Northwind;
ALTER SCHEMA MySchema TRANSFER dbo.MyTable;
```

En el ejemplo anterior, se cambia el esquema de la tabla `MyTable` del esquema `dbo` al esquema `MySchema`.

Al asignar un objeto a un esquema, puedes especificar el nombre completo del objeto en la forma esquema.objeto. Por ejemplo, `MySchema.MyTable` se refiere a la tabla `MyTable` en el esquema `MySchema`.

Los esquemas proporcionan una forma conveniente de organizar y separar los objetos en la base de datos. También ayudan a evitar conflictos de nombres y proporcionan una mayor modularidad en la administración de la base de datos.

Es importante tener en cuenta que los permisos de acceso a los objetos en un esquema deben ser asignados correctamente a los usuarios y roles correspondientes para garantizar la seguridad y el control de acceso adecuados.

Recuerda que este es solo un ejemplo y debes adaptarlo a tus necesidades específicas y a la estructura de tu base de datos.

---

[🔼](#índice)

## **156. Descripción de Roles de Servidor y Roles Predefinidos**

En SQL Server, existen dos tipos de roles: roles de servidor y roles predefinidos. Estos roles son utilizados para administrar y asignar permisos a los usuarios en el servidor de base de datos. A continuación, explicaré cada tipo de rol y proporcionaré ejemplos utilizando la base de datos Northwind.

1. **Roles de servidor:**

Los roles de servidor son roles que se definen a nivel de servidor y están diseñados para administrar y controlar el acceso a los recursos del servidor. Estos roles se utilizan para asignar permisos y responsabilidades a nivel de servidor, y los usuarios asignados a estos roles obtienen automáticamente los permisos asociados a ellos.

Algunos ejemplos de roles de servidor en SQL Server son:

- **sysadmin:** Este rol tiene todos los permisos en el servidor y se utiliza para administradores del sistema.
- **serveradmin:** Este rol tiene permisos de administración del servidor, pero no tiene acceso a bases de datos específicas.
- **setupadmin:** Este rol tiene permisos para administrar la configuración del servidor.
- **bulkadmin:** Este rol tiene permisos para realizar operaciones de carga masiva de datos.

Ejemplo:

```
USE master;
CREATE LOGIN MyLogin WITH PASSWORD = 'MyPassword';
ALTER SERVER ROLE sysadmin ADD MEMBER MyLogin;
```

En el ejemplo anterior, se crea un nuevo inicio de sesión llamado `MyLogin` y se agrega como miembro del rol de servidor `sysadmin`, lo que le otorga todos los permisos en el servidor.

2. **Roles predefinidos:**

Los roles predefinidos son roles que se crean automáticamente al crear una base de datos en SQL Server. Estos roles se utilizan para asignar permisos y responsabilidades a nivel de base de datos, y los usuarios asignados a estos roles obtienen automáticamente los permisos asociados a ellos.

Algunos ejemplos de roles predefinidos en SQL Server son:

- **db_owner:** Este rol tiene todos los permisos en una base de datos y se utiliza para administradores de la base de datos.
- **db_datareader:** Este rol tiene permisos para leer todos los datos en una base de datos.
- **db_datawriter:** Este rol tiene permisos para insertar, actualizar y eliminar datos en una base de datos.
- **db_executor:** Este rol tiene permisos para ejecutar procedimientos almacenados y funciones en una base de datos.

Ejemplo:

```
USE Northwind;
CREATE USER MyUser FOR LOGIN MyLogin;
ALTER ROLE db_datareader ADD MEMBER MyUser;
```

En el ejemplo anterior, se crea un nuevo usuario llamado `MyUser` asociado al inicio de sesión `MyLogin` y se agrega como miembro del rol predefinido `db_datareader`, lo que le otorga permisos para leer todos los datos en la base de datos Northwind.

Los roles de servidor y roles predefinidos proporcionan una forma conveniente de asignar permisos y controlar el acceso a nivel de servidor y base de datos. Al utilizar estos roles, puedes gestionar de manera efectiva los permisos de los usuarios y mantener la seguridad de tus bases de datos.

Es importante tener en cuenta que los roles deben asignarse cuidadosamente y seguir las mejores prácticas de seguridad para garantizar un acceso adecuado y proteger la integridad de los datos.

---

[🔼](#índice)

## **157. SQL SERVER Profiler**

SQL Server Profiler es una herramienta de monitoreo y análisis de rendimiento proporcionada por Microsoft SQL Server. Permite capturar y analizar eventos y actividades que ocurren en una instancia de SQL Server. Con SQL Server Profiler, puedes realizar un seguimiento detallado de las consultas ejecutadas, los procedimientos almacenados llamados, los eventos del sistema y muchas otras actividades relacionadas con la base de datos.

SQL Server Profiler se utiliza principalmente para el análisis de rendimiento y la resolución de problemas. Puedes utilizarlo para identificar cuellos de botella, optimizar consultas, detectar consultas lentas y comprender el comportamiento del sistema en general. También es una herramienta útil para auditar actividades en la base de datos, como seguimiento de cambios, identificación de problemas de seguridad y análisis de actividad de usuarios.

A continuación, se muestra un ejemplo de cómo utilizar SQL Server Profiler con la base de datos Northwind:

1. **Abrir SQL Server Profiler:**

Abre SQL Server Profiler desde la carpeta "`Herramientas de SQL Server`" en el menú de inicio.

2. **Crear un nuevo seguimiento:**

Haz clic en "`Archivo`" y selecciona "`Nuevo seguimiento`". En la ventana emergente, selecciona la instancia de SQL Server que deseas monitorear y elige los eventos que deseas capturar. Puedes seleccionar eventos predefinidos o personalizarlos según tus necesidades.

3. **Iniciar el seguimiento:**

Haz clic en "`Iniciar`" para comenzar a capturar los eventos. A partir de este punto, SQL Server Profiler registrará todas las actividades seleccionadas en tiempo real.

4. **Realizar acciones en la base de datos:**

Realiza consultas, ejecuta procedimientos almacenados u otras acciones en la base de datos Northwind para capturar los eventos correspondientes.

5. **Analizar los resultados:**

Una vez que hayas finalizado las acciones en la base de datos, puedes detener el seguimiento haciendo clic en "`Detener`". Luego, puedes analizar los resultados en la pestaña "`Eventos capturados`" de SQL Server Profiler. Aquí encontrarás detalles sobre las consultas ejecutadas, los tiempos de respuesta, los eventos del sistema y otros datos relevantes.

SQL Server Profiler es una herramienta poderosa para el monitoreo y análisis de rendimiento en SQL Server. Te permite comprender el comportamiento de la base de datos, identificar cuellos de botella y mejorar el rendimiento de tus consultas. Además, puede ayudarte en la resolución de problemas y en la identificación de actividades sospechosas o inapropiadas en la base de datos.

Es importante tener en cuenta que SQL Server Profiler puede tener un impacto en el rendimiento del sistema debido a la sobrecarga de captura de eventos. Por lo tanto, se recomienda utilizarlo con precaución en entornos de producción y limitar la cantidad de eventos capturados según sea necesario.

---

[🔼](#índice)

## **158. Conociendo la herramienta**

SQL Server Profiler es una herramienta de monitoreo y análisis de rendimiento que permite capturar y analizar eventos y actividades que ocurren en una instancia de SQL Server. Proporciona una interfaz gráfica intuitiva que te permite definir y configurar seguimientos personalizados para capturar información detallada sobre las consultas, transacciones, eventos del sistema y otras actividades relacionadas con la base de datos.

Aquí tienes un ejemplo de cómo utilizar SQL Server Profiler con la base de datos Northwind:

1. **Abrir SQL Server Profiler:**

Inicia SQL Server Profiler desde la carpeta "`Herramientas de SQL Server`" en el menú de inicio.

2. **Crear un nuevo seguimiento:**

Haz clic en "`Archivo`" y selecciona "`Nuevo seguimiento`". En la ventana emergente, selecciona la instancia de SQL Server que deseas monitorear y elige los eventos que deseas capturar. Puedes seleccionar eventos predefinidos o personalizarlos según tus necesidades.

3. **Configurar filtros:**

Puedes aplicar filtros para capturar solo los eventos relevantes. Por ejemplo, puedes filtrar por base de datos, usuario, host o cualquier otra condición específica. Esto te ayudará a enfocarte en los eventos de interés y reducir la cantidad de datos capturados.

4. **Iniciar el seguimiento:**

Haz clic en "`Iniciar`" para comenzar a capturar los eventos. A partir de este punto, SQL Server Profiler registrará todas las actividades seleccionadas en tiempo real.

5. **Realizar acciones en la base de datos:**

Realiza consultas, ejecuta procedimientos almacenados u otras acciones en la base de datos Northwind para capturar los eventos correspondientes.

6. **Analizar los resultados:**

Una vez que hayas finalizado las acciones en la base de datos, puedes detener el seguimiento haciendo clic en "`Detener`". Luego, puedes analizar los resultados en la pestaña "`Eventos capturados`" de SQL Server Profiler. Aquí encontrarás detalles sobre las consultas ejecutadas, los tiempos de respuesta, los eventos del sistema y otros datos relevantes.

SQL Server Profiler te brinda una visión detallada del rendimiento y el comportamiento de tu base de datos. Puedes identificar consultas lentas, detectar cuellos de botella, optimizar el rendimiento y solucionar problemas de manera efectiva. También puedes utilizarlo para auditar actividades en la base de datos, monitorear el acceso de usuarios y realizar análisis de rendimiento exhaustivos.

Recuerda que SQL Server Profiler puede tener un impacto en el rendimiento del sistema debido a la sobrecarga de captura de eventos. Por lo tanto, se recomienda utilizarlo con precaución en entornos de producción y limitar la cantidad de eventos capturados según sea necesario. Además, asegúrate de tener los permisos adecuados para ejecutar SQL Server Profiler, ya que es una herramienta poderosa que puede acceder a información confidencial de la base de datos.

En resumen, SQL Server Profiler es una herramienta valiosa para el monitoreo y análisis de rendimiento en SQL Server. Te permite obtener información detallada sobre las actividades en la base de datos, lo que facilita la identificación y solución de problemas. Su interfaz gráfica intuitiva y su capacidad para personalizar los seguimientos lo convierten en una herramienta imprescindible para los administradores de bases de datos.

---

[🔼](#índice)

## **159. Como monitorear procesos por tiempo de ejecución**

Para monitorear procesos por tiempo de ejecución en SQL Server Profiler, puedes utilizar la función de filtrado y configurar los eventos adecuados. A continuación, se proporciona una explicación detallada de cómo hacerlo con un ejemplo utilizando la base de datos Northwind:

1. **Abrir SQL Server Profiler:**

Inicia SQL Server Profiler desde la carpeta "`Herramientas de SQL Server`" en el menú de inicio.

2. **Crear un nuevo seguimiento:**

Haz clic en "`Archivo`" y selecciona "`Nuevo seguimiento`". En la ventana emergente, selecciona la instancia de SQL Server que deseas monitorear y elige los eventos que deseas capturar.

3. **Configurar eventos y columnas:**

En la pestaña "`Eventos seleccionados`", selecciona los eventos que te interesan para monitorear los procesos por tiempo de ejecución. Algunos eventos relevantes pueden ser "`SQL:BatchCompleted`", "`RPC:Completed`" o "`SP:Completed`". También puedes seleccionar otros eventos adicionales según tus necesidades.

4. **Configurar columnas adicionales:**

Para monitorear el tiempo de ejecución, puedes agregar la columna "`Duration`" en la pestaña "`Columnas seleccionadas`". Esta columna muestra el tiempo transcurrido en milisegundos para cada evento capturado.

5. **Configurar filtros de duración:**

Haz clic en el botón "`Filtro`" y en la ventana emergente, selecciona la pestaña "`Columnas de duración`". Aquí puedes definir un filtro para mostrar solo los eventos con una duración mínima o máxima específica. Por ejemplo, puedes establecer un filtro para mostrar solo los eventos que tengan una duración superior a 1000 milisegundos (1 segundo).

6. **Iniciar el seguimiento:**

Haz clic en "`Iniciar`" para comenzar a capturar los eventos y monitorear los procesos por tiempo de ejecución.

7. **Realizar acciones en la base de datos:**

Realiza consultas, ejecuta procedimientos almacenados u otras acciones en la base de datos Northwind para capturar los eventos correspondientes.

8. **Analizar los resultados:**

Una vez que hayas finalizado las acciones en la base de datos, puedes detener el seguimiento haciendo clic en "`Detener`". Luego, puedes analizar los resultados en la pestaña "`Eventos capturados`" de SQL Server Profiler. Aquí encontrarás detalles sobre los eventos capturados, incluido el tiempo de ejecución de cada proceso.

Al utilizar SQL Server Profiler con la configuración mencionada, podrás monitorear los procesos por tiempo de ejecución y obtener información valiosa sobre el rendimiento de tu base de datos. Esto te permitirá identificar consultas lentas o procesos que consumen demasiado tiempo y optimizar su rendimiento.

Recuerda que SQL Server Profiler puede tener un impacto en el rendimiento del sistema debido a la sobrecarga de captura de eventos. Por lo tanto, se recomienda utilizarlo con precaución en entornos de producción y limitar la cantidad de eventos capturados según sea necesario. Además, asegúrate de tener los permisos adecuados para ejecutar SQL Server Profiler, ya que es una herramienta poderosa que puede acceder a información confidencial de la base de datos.

En resumen, utilizando SQL Server Profiler con la configuración adecuada de eventos, columnas y filtros, puedes monitorear los procesos por tiempo de ejecución y obtener información valiosa sobre el rendimiento de tu base de datos. Esto te ayudará a identificar y solucionar problemas de rendimiento de manera efectiva.

---

[🔼](#índice)

## **160. Definiendo templates para monitoreo**

En SQL Server, puedes definir templates de monitoreo para capturar y analizar eventos específicos de manera más eficiente y consistente. Un template es una configuración predefinida de eventos, columnas y filtros que se puede guardar y reutilizar en diferentes ocasiones. A continuación, se presenta una explicación detallada de cómo definir y utilizar templates de monitoreo en SQL Server utilizando la base de datos Northwind como ejemplo:

1. **Abrir SQL Server Profiler:**

Inicia SQL Server Profiler desde la carpeta "`Herramientas de SQL Server`" en el menú de inicio.

2. **Crear un nuevo seguimiento:**

Haz clic en "`Archivo`" y selecciona "`Nuevo seguimiento`". En la ventana emergente, selecciona la instancia de SQL Server que deseas monitorear.

3. **Configurar eventos y columnas:**

En la pestaña "`Eventos seleccionados`", selecciona los eventos y las columnas que deseas capturar en tu template de monitoreo. Por ejemplo, puedes seleccionar los eventos "`SQL:BatchCompleted`", "`RPC:Completed`" y las columnas "`Duration`" y "`TextData`".

4. **Configurar filtros adicionales (opcional):**

Si deseas aplicar filtros adicionales a los eventos capturados, como filtrar por una base de datos específica o por un usuario determinado, puedes hacerlo en la pestaña "`Filtro`".

5. **Guardar el template:**

Haz clic en "`Archivo`" y selecciona "`Guardar como Template`". Elige un nombre descriptivo para el template y guárdalo en una ubicación conveniente.

6. **Cerrar el seguimiento actual:**

Puedes cerrar el seguimiento actual sin guardar los datos capturados, ya que el template contendrá la configuración deseada.

7. **Utilizar el template en futuros seguimientos:**

Para utilizar el template en futuros seguimientos, abre SQL Server Profiler y haz clic en "`Archivo`" y luego en "`Abrir`". Selecciona "`Template`" en el tipo de archivo y elige el template guardado previamente.

8. **Iniciar el seguimiento:**

Haz clic en "`Iniciar`" para comenzar a capturar los eventos utilizando el template configurado. Realiza acciones en la base de datos Northwind para capturar los eventos correspondientes.

9. **Analizar los resultados:**

Una vez que hayas finalizado las acciones en la base de datos, puedes detener el seguimiento haciendo clic en "`Detener`". Luego, puedes analizar los resultados en la pestaña "`Eventos capturados`" de SQL Server Profiler. Aquí encontrarás los eventos y columnas definidos en el template, lo que te permitirá analizar la información capturada de manera más eficiente.

Al utilizar templates de monitoreo, puedes ahorrar tiempo y esfuerzo al configurar repetidamente los eventos, columnas y filtros deseados en cada seguimiento. Además, la estandarización de la configuración te permite obtener resultados consistentes y comparables en diferentes situaciones.

Recuerda que SQL Server Profiler puede tener un impacto en el rendimiento del sistema debido a la sobrecarga de captura de eventos. Por lo tanto, es importante utilizar los templates de monitoreo de manera selectiva y ajustar la configuración según sea necesario para evitar una carga excesiva en el servidor.

En resumen, los templates de monitoreo en SQL Server Profiler te permiten definir configuraciones predefinidas de eventos, columnas y filtros para capturar y analizar de manera eficiente los eventos de tu base de datos. Esto simplifica el proceso de configuración y te ayuda a obtener información relevante de manera más rápida y consistente.

**Herramientas del menú, Importación y exportación de Trazas**

En SQL Server, el menú "`Importación y exportación de trazas`" proporciona una forma conveniente de importar y exportar archivos de traza generados por SQL Server Profiler. Esto es útil cuando deseas compartir trazas con otros usuarios o importar trazas previamente generadas para su análisis. A continuación, se muestra una explicación detallada de cómo utilizar estas herramientas con la base de datos Northwind como ejemplo:

1. **Abrir SQL Server Profiler:**

Inicia SQL Server Profiler desde la carpeta "Herramientas de SQL Server" en el menú de inicio.

2. **Generar una traza:**

Antes de poder importar o exportar una traza, debes generar una utilizando SQL Server Profiler. Configura los eventos, columnas y filtros necesarios para capturar la información que deseas. Por ejemplo, puedes seleccionar los eventos "`SQL:BatchCompleted`" y "`RPC:Completed`" y las columnas "`Duration`" y "`TextData`". Inicia la captura de la traza.

3. **Detener la captura de la traza:**

Una vez que hayas realizado las acciones necesarias en la base de datos Northwind, detén la captura de la traza en SQL Server Profiler haciendo clic en "`Detener`".

4. **Acceder al menú "Importación y exportación de trazas":**

Haz clic en "`Archivo`" en la barra de menú de SQL Server Profiler y selecciona "`Importación y exportación de trazas`". Aparecerá una ventana con las opciones disponibles.

5. **Exportar una traza:**

Para exportar una traza generada previamente, selecciona la opción "`Exportar`" en la ventana "`Importación y exportación de trazas`". Se abrirá un cuadro de diálogo para seleccionar la traza que deseas exportar y la ubicación de destino. Elige un nombre para el archivo de traza y haz clic en "`Guardar`". La traza se exportará como un archivo `.trc`.

6. **Importar una traza:**

Para importar una traza previamente generada, selecciona la opción "`Importar`" en la ventana "`Importación y exportación de trazas`". Se abrirá un cuadro de diálogo para seleccionar el archivo de traza que deseas importar. Navega hasta el archivo `.trc` y haz clic en "`Abrir`". La traza se importará y estará disponible para su análisis en SQL Server Profiler.

Importar y exportar trazas te permite compartir fácilmente archivos de traza con otros usuarios o transferir trazas entre diferentes entornos de SQL Server. Esto es útil para colaboración, análisis de rendimiento y resolución de problemas.

Es importante tener en cuenta que la importación y exportación de trazas requiere permisos adecuados en el servidor SQL Server. Asegúrate de tener los permisos necesarios para realizar estas operaciones.

En resumen, la herramienta "`Importación y exportación de trazas`" en SQL Server Profiler te permite exportar trazas generadas previamente como archivos .trc y también importar trazas para su análisis. Esto facilita la colaboración y el intercambio de información entre diferentes usuarios y entornos de SQL Server.

**10 Buenas prácticas sobre diseño, programación y seguridad**

Aquí tienes 10 buenas prácticas relacionadas con el diseño, programación y seguridad al utilizar SQL Server Profiler:

1. **Limita el uso de SQL Server Profiler en entornos de producción:** La captura de trazas con SQL Server Profiler puede tener un impacto en el rendimiento del servidor, por lo que se recomienda utilizarlo principalmente en entornos de desarrollo, pruebas o en situaciones específicas de resolución de problemas en producción.

2. **Filtra adecuadamente los eventos y columnas:** Configura cuidadosamente los eventos y las columnas que deseas capturar en la traza. Limita la cantidad de eventos y selecciona solo las columnas relevantes para reducir la sobrecarga y mejorar la eficiencia de captura.

3. **Utiliza plantillas personalizadas:** SQL Server Profiler permite crear plantillas personalizadas con la configuración preferida. Utiliza estas plantillas para evitar la repetición de la configuración cada vez que inicies una nueva traza.

4. **Limita la duración de la captura de trazas:** Especifica un tiempo de duración para la captura de trazas o establece un límite de tamaño de archivo. Esto ayuda a evitar que las trazas crezcan indefinidamente y consuman recursos innecesarios.

5. **Utiliza trazas filtradas:** Aplica filtros para capturar únicamente los eventos relevantes. Puedes filtrar por aplicación, base de datos, usuario u otras condiciones que sean importantes para tu análisis.

6. **Asegura la traza:** Para proteger la información sensible, asegúrate de que las trazas se almacenen en ubicaciones seguras. Limita el acceso a los archivos de traza y considera el uso de cifrado si es necesario.

7. **Evita capturar información confidencial:** No captures información confidencial, como contraseñas o datos personales, en las trazas. Asegúrate de excluir cualquier información sensible de la configuración de eventos y columnas.

8. **Monitorea el impacto en el rendimiento:** Mantén un ojo en el impacto que SQL Server Profiler tiene en el rendimiento del servidor. Si notas una degradación significativa del rendimiento, ajusta la configuración de la traza o considera utilizar otras herramientas de monitoreo más ligeras.

9. **Mantén un registro de las trazas realizadas:** Lleva un registro de las trazas que has capturado, incluyendo la configuración utilizada, la fecha y el propósito de la traza. Esto facilita el seguimiento y la referencia futura.

10. **Actualízate con las herramientas más recientes:** SQL Server Profiler ha sido reemplazado por Extended Events como la principal herramienta de captura de eventos en versiones más recientes de SQL Server. Considera aprender y utilizar Extended Events para capturar eventos de manera más eficiente y con menos impacto en el rendimiento.

Recuerda que el uso de SQL Server Profiler y otras herramientas de monitoreo debe realizarse de manera responsable y cumpliendo con las políticas de seguridad y privacidad establecidas en tu organización.

---

[🔼](#índice)

| **Inicio**            | **atrás 15**                | **Siguiente 17**            |
| --------------------- | --------------------------- | --------------------------- |
| [🏠](../../README.md) | [⏪](./15_Consultas_SQL.md) | [⏩](./17_Consultas_SQL.md) |
