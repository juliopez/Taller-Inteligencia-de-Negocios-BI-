# Taller Práctico — Integración de datos hacia SQL Server (PDI + Power Automate)

**Duración total: 90 minutos**

---
## Objetivo del taller
Modificar los flujos de integración de datos desarrollados en clases (Pentaho Data Integration y Power Automate), con el propósito de almacenar la información obtenida en una base de datos SQL Server alojada en una instancia en la nube (AWS), en lugar de archivos planos (Excel o CSV).

---
## Contexto
Hasta este punto del curso, los procesos desarrollados han permitido:
- extraer datos desde servicios externos (WSDL y APIs)
- transformarlos
- almacenarlos en archivos (Excel, CSV, Google Sheets)

Este enfoque es útil para validación inicial, pero no representa el funcionamiento de una solución real de *Business Intelligence*.

En entornos productivos, los datos deben ser almacenados en sistemas estructurados (bases de datos), permitiendo su integración, modelamiento y posterior análisis.

Este taller introduce ese cambio:  **pasar de almacenamiento en archivos a almacenamiento en base de datos relacional.**

---
## Descripción general de la actividad

El estudiante deberá:
1. Utilizar el flujo desarrollado en **Pentaho Data Integration (WSDL)**
2. Utilizar el flujo desarrollado en **Power Automate (API)**
3. Modificar ambos procesos para que:
    - los datos no se almacenen en archivos
    - sino que se inserten en **SQL Server**
---
## Condiciones del entorno
Cada estudiante trabajará con su propia configuración:
- SQL Server en instancia AWS
- IP distinta
- Base de datos distinta
- Usuario distinto (autenticación Windows o SQL Server)

---
## Resultado mínimo esperado
Al finalizar el taller, el estudiante deberá lograr:
- insertar datos en SQL Server desde al menos **una herramienta**  
- idealmente, lograr inserción desde **ambas herramientas**
- evidenciar:
	- tablas creadas
	- datos cargados correctamente
---
## Estructura de datos requerida
Durante el taller, el estudiante deberá:
- crear **al menos una tabla** en SQL Server
- idealmente trabajar con **dos tablas**:

| Tabla   | Origen                           |
| ------- | -------------------------------- |
| Tabla 1 | Datos desde PDI (WSDL)           |
| Tabla 2 | Datos desde Power Automate (API) |

---
## Sugerencia de trabajo
Se recomienda abordar el taller en el siguiente orden:
1. Crear la tabla en SQL Server
2. Modificar el flujo en PDI y validar la carga de datos
3. Una vez validada la conexión a la base de datos, modificar el flujo en Power Automate
---
## Actividad 1 — Integración desde PDI (WSDL → SQL Server)
Modificar el flujo existente en Pentaho para:
- reemplazar salida a archivo
- insertar datos en SQL Server
### Consideraciones
- Crear una conexión a base de datos (JDBC)
- Utilizar componente: **Table Output**
- Validar correspondencia entre:
    - columnas del flujo
    - columnas de la tabla
---
## Actividad 2 — Integración desde Power Automate (API → SQL Server)
Modificar el flujo existente en Power Automate para:
- reemplazar almacenamiento en Excel/Sheets
- insertar datos en SQL Server
### Consideraciones
- Utilizar conector: **SQL Server**
- Acción clave: **Insert row (V2)**
---
## Pregunta evaluativa
Durante el taller, se trabajó en la modificación de flujos de integración de datos para reemplazar el almacenamiento en archivos por la carga en una base de datos SQL Server.

**Pregunta:**
> Explique dos diferencias relevantes entre almacenar datos en archivos (CSV/Excel) y almacenarlos en una base de datos SQL Server dentro de un proceso de integración de datos.
> 
> Además, describa una dificultad técnica concreta que haya enfrentado (o que podría enfrentar) al realizar la conexión desde Pentaho Data Integration o Power Automate hacia SQL Server, indicando cómo podría resolverse.

---
## Referencias
- **Anexo A:** SQL_Server-PDI
- [https://docs.pentaho.com](https://docs.pentaho.com/)  
- **Anexo B:**  SQL_Server-Power-Automate
- [https://learn.microsoft.com/en-us/connectors/sql/](https://learn.microsoft.com/en-us/connectors/sql/)
- [https://learn.microsoft.com/en-us/connectors/sql/#actions](https://learn.microsoft.com/en-us/connectors/sql/#actions)
- [https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-onprem](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-onprem)
