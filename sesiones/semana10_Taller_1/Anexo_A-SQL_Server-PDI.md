# Anexo A: Integración de datos desde PDI hacia SQL Server

Para conectar **Pentaho Data Integration (PDI)** con **Microsoft SQL Server**, es necesario realizar una serie de configuraciones tanto en el entorno de Pentaho como en la base de datos para permitir la comunicación a través del protocolo TCP/IP.

> Se asume que la instancia de SQL Server ya se encuentra correctamente configurada para permitir conexiones remotas.

A continuación, se detallan los pasos basados en las fuentes proporcionadas:
### 1. Preparación de los Controladores (JDBC Drivers)
Pentaho requiere un controlador específico para comunicarse con SQL Server.
*   **Descarga del Driver:** Debe descargar el **Microsoft JDBC Driver para SQL Server** (archivo .zip) desde el sitio oficial de Microsoft. 
*   **Selección del archivo JAR:** Al descomprimirlo, encontrará varios archivos JAR. Elija el que corresponda a su versión de Java: por ejemplo, `mssql-jdbc-xxx.jre8.jar` para Java 8 o `jre11` para Java 11 o superiores.
*   **Instalación en PDI:** Copie el archivo JAR seleccionado y péguelo en la carpeta de instalación de PDI, específicamente en la ruta: `data-integration/lib`.
*   **Importante:** Asegúrese de que **solo haya una versión** del controlador en esta carpeta para evitar conflictos de versiones. Si PDI está abierto, debe **reiniciarlo** para que reconozca el nuevo controlador.
### 2. Configuración de SQL Server
Debe habilitar los permisos y protocolos necesarios en su instancia de SQL Server:
*   **Habilitar TCP/IP:** Abra el **SQL Server Configuration Manager**, vaya a "Protocolos de [Nombre de instancia]" y asegúrese de que **TCP/IP** y **Named Pipes** estén en estado "Habilitado".
*   **Configurar el Puerto:** En las propiedades de TCP/IP, vaya a la pestaña "Direcciones IP", busque la sección **IPAll** y verifique que el puerto TCP esté configurado en **1433**.
*   **Autenticación:** En SQL Server Management Studio (SSMS), haga clic derecho en el servidor, vaya a "Propiedades" > "Seguridad" y seleccione **"Modo de autenticación de SQL Server y Windows"**.
*   **Usuario SQL:** Se recomienda habilitar el usuario `sa`, asignarle una contraseña y verificar que tenga permisos para conectarse.
*   **Reiniciar Servicios:** Es fundamental **reiniciar el servicio de SQL Server** desde el Administrador de Configuración o la consola de Servicios de Windows para aplicar estos cambios.
### 3. Configuración de la Conexión en PDI (Spoon)
Una vez configurado el entorno, cree la conexión dentro de la interfaz de Spoon:
1.  En su transformación o trabajo, cree una nueva conexión de base de datos (por ejemplo, desde un paso de "Table Output").
2.  **Tipo de base de datos:** Seleccione **MS SQL Server**.
3.  **Tipo de acceso:** Elija **Native (JDBC)**.
4.  **Configuración de Host:** Ingrese la dirección IP o el nombre del servidor.
5.  **Nombre de la base de datos:** Escriba el nombre exacto de la base de datos a la que desea conectar.
6.  **Instancia:** Si utiliza una versión Express, especifique el nombre de la instancia (comúnmente `SQLEXPRESS`).
7.  **Puerto:** Use el **1433**.
8.  **Credenciales:** Ingrese el nombre de usuario (ej. `sa`) y la contraseña configurada previamente.
9.  Haga clic en el botón **"Test"** para verificar que la conexión sea exitosa.
### 4. Solución de Problemas Comunes
*   **Firewall:** Si la conexión falla, verifique que el **Firewall de Windows** no esté bloqueando el puerto 1433. Es posible que deba crear una regla de entrada para permitir el tráfico en este puerto.
*   **Autenticación Integrada:** Si desea usar la autenticación de Windows en lugar de un usuario SQL, debe copiar el archivo `sqljdbc_auth.dll` (incluido en la descarga del driver) en el directorio de PDI y asegurarse de que coincida con la arquitectura de su procesador (x64 o x86).
*   **Error de conexión remota:** Asegúrese de que en las propiedades del servidor en SSMS esté marcada la opción **"Permitir conexiones remotas a este servidor"**.
