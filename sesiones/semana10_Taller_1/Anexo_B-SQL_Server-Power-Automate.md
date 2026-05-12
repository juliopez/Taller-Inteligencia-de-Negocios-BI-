# Anexo B: Integración de datos desde Power Automate hacia SQL Server
Conectar Power Automate con **Microsoft SQL Server** requiere el uso de un conector clasificado como **Premium**, lo que implica un licenciamiento específico. Este conector permite realizar operaciones de creación, lectura, actualización y eliminación (CRUD), además de ejecutar procedimientos almacenados y consultas nativas tanto en la nube como en entornos locales.

A continuación, se presenta una guía detallada basada en las fuentes para establecer y optimizar esta conexión:
### 1. Configuración de la Infraestructura
El método de conexión varía según dónde se encuentre alojada la base de datos:
*   **Azure SQL:** Se conecta directamente a través de la nube utilizando las credenciales correspondientes.
*   **SQL Server local (On-premises):** Es obligatorio instalar y configurar una **Puerta de enlace de datos local (On-premises data gateway)** en el servidor o PC donde reside la base de datos para que Power Automate pueda "ver" el servidor local.
### 2. Métodos de Autenticación
Al crear la conexión, puedes elegir entre varios tipos de seguridad:
*   **SQL Server Authentication:** Requiere el nombre del servidor, base de datos, usuario y contraseña.
*   **Windows Authentication:** Utiliza una cuenta de Windows local; requiere la puerta de enlace (gateway).
*   **Microsoft Entra ID (antes Azure AD):** Permite autenticación integrada, por entidad de servicio (Service Principal) o mediante identidad administrada (esta última principalmente para Logic Apps).
*   **Secure Implicit Connections:** Una mejora de seguridad (enero 2024) que evita que los usuarios finales reutilicen las credenciales compartidas para crear nuevas aplicaciones no autorizadas.
### 3. Uso de Acciones y Desencadenadores (Triggers)
Se recomienda utilizar siempre las versiones **V2** de las operaciones, ya que las V1 están en proceso de depreciación.
*   **Triggers:** Permiten iniciar flujos automáticamente. "Cuando se crea un elemento" requiere una columna `IDENTITY`, y "Cuando se modifica un elemento" requiere una columna `ROWVERSION` en la tabla.
*   **Acciones CRUD:** Para obtener, actualizar o eliminar filas específicas, es indispensable que la tabla tenga definida una **Clave Primaria (Primary Key)**.
*   **Procedimientos Almacenados:** Si el procedimiento no requiere parámetros de entrada, Power Automate puede fallar; se recomienda añadir un parámetro "ficticio" o ingresar `{}` para satisfacer el requerimiento del conector.
### 4. Mejores Prácticas y Optimización
*   **Evitar bucles seriales:** Procesar filas una por una dentro de un bucle "Apply to each" es ineficiente y puede tomar minutos para pocos registros.
*   **Procesamiento por lotes (Batch):** Es mucho más rápido convertir los datos a formato **JSON** y enviarlos a un **procedimiento almacenado** que los procese todos de una vez, reduciendo tiempos de carga de 10 minutos a pocos segundos.
*   **Limpieza de datos (Sanitización):** Para evitar errores en las consultas SQL, se deben limpiar caracteres especiales. Una práctica común es reemplazar comillas simples (`'`) por comillas dobles (`"`) y eliminar saltos de línea en las variables antes de insertarlas.
*   **Filtros OData:** Al obtener filas, utiliza filtros de servidor (parámetro `$filter`) como `precio eq 1.5` para que SQL Server solo devuelva los datos necesarios, mejorando el rendimiento del flujo.
### 5. Limitaciones Técnicas Importantes
*   **Tamaño de solicitud:** Para servidores locales vía gateway, el límite es de **2 MB** por solicitud y **8 MB** por respuesta.
*   **Tiempos de espera (Timeout):** Las consultas o procedimientos que excedan los **110 segundos** de ejecución fallarán automáticamente.
*   **Caracteres especiales:** El signo de porcentaje (`%`) debe escaparse (usando `%%`) si no se está utilizando como indicador de variable en Power Automate para escritorio.

---
## Gateway
El uso de una **puerta de enlace de datos local (On-premises data gateway)** es obligatorio únicamente si tu servidor de SQL Server se encuentra en un entorno **local (on-premises)** o en una red privada. Si te conectas a una base de datos en la nube, como **Azure SQL**, no es necesario utilizarla.

A continuación, se detalla el proceso para configurar la conexión utilizando una puerta de enlace:
### 1. Instalación de la Puerta de Enlace
Para que Power Automate (en la nube) pueda "ver" tu servidor local, debes instalar un software mediador:
*   **Descarga e instalación:** Debes descargar el instalador oficial de Microsoft y ejecutarlo en el servidor o PC donde reside la base de datos o en un equipo que tenga acceso constante a ella.
*   **Configuración:** Sigue los pasos del asistente para registrar la puerta de enlace con tu cuenta de Microsoft 365. Una vez configurada, aparecerá automáticamente como una opción disponible en Power Automate.
### 2. Configuración de la Conexión en Power Automate
Al crear un nuevo paso con el conector de **SQL Server** (que es un conector **Premium**), deberás completar los siguientes campos:
*   **Tipo de Autenticación:** Generalmente se utiliza **SQL Server Authentication** o **Windows Authentication** para entornos locales.
*   **Credenciales:** Introduce el nombre del servidor (server[:port]), el nombre de la base de datos, el usuario y la contraseña.
*   **Selección del Gateway:** En el campo desplegable "Gateway" o "Puerta de enlace", selecciona el nombre de la puerta de enlace que instalaste en el paso anterior.
### 3. Limitaciones Técnicas al usar Gateway
Es importante considerar que el uso de una puerta de enlace impone ciertas restricciones de rendimiento y funcionalidad:
*   **Límites de tamaño:** Existe un límite de **2 MB** para el tamaño de la solicitud (datos enviados) y de **8 MB** para la respuesta (datos recibidos) a través de la puerta de enlace.
*   **Procedimientos Almacenados:** Cuando se invocan mediante una puerta de enlace, no se devuelven los valores de los parámetros de salida (`OUTPUT`), no está disponible el valor de retorno y solo se devuelve el primer conjunto de resultados.
*   **Consultas Nativas:** Algunas fuentes indican que la operación "Ejecutar consulta SQL nativa" puede presentar problemas de compatibilidad o no estar soportada en ciertas configuraciones de puerta de enlace local.
*   **Versión de SQL:** El servidor local debe ser, como mínimo, **SQL Server 2005**.
### 4. Seguridad
Si utilizas **Windows Authentication**, ten en cuenta que esta conexión puede configurarse como **"No compartida"** (Windows Authentication Non Shared), lo que obligará a otros usuarios de la aplicación o flujo a introducir sus propias credenciales en lugar de usar las del creador.

