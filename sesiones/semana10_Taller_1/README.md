# Semana 10 — Integración de datos hacia SQL Server (PDI + Power Automate)

## Descripción general

En esta sesión del curso se desarrollará un taller práctico orientado a la integración de datos hacia un motor de base de datos relacional utilizando herramientas de integración y automatización revisadas previamente en clases.

Hasta este punto del curso, los procesos construidos por los estudiantes han permitido:

- consumir datos desde servicios externos
- trabajar con archivos CSV y Excel
- realizar procesos ETL básicos e intermedios
- automatizar flujos mediante Pentaho Data Integration (PDI) y Power Automate

Sin embargo, en un entorno real de Business Intelligence, los datos normalmente no se almacenan en archivos planos, sino en sistemas estructurados capaces de soportar procesos analíticos, integración de múltiples fuentes y análisis multidimensional.

Por esta razón, el foco de esta semana consiste en modificar los flujos desarrollados anteriormente para que los datos obtenidos desde APIs y servicios WSDL sean almacenados directamente en Microsoft SQL Server.

---

# Objetivo de aprendizaje

Al finalizar esta sesión, el estudiante será capaz de:

- conectar herramientas de integración de datos con SQL Server
- insertar datos obtenidos desde servicios externos en una base de datos relacional
- comprender las diferencias entre almacenamiento en archivos y almacenamiento estructurado
- reconocer problemáticas técnicas comunes asociadas a conectividad, drivers, autenticación y gateways

---

# Contenidos trabajados

Durante esta sesión se abordarán los siguientes contenidos:

- Integración de datos hacia SQL Server
- Uso de conexiones JDBC en Pentaho Data Integration
- Configuración de SQL Server para conexiones remotas
- Inserción de datos mediante `Table Output`
- Uso del conector SQL Server en Power Automate
- Inserción de registros mediante `Insert Row (V2)`
- Consideraciones sobre gateways y autenticación
- Diferencias entre almacenamiento operacional y archivos planos

---

# Actividad práctica

La sesión se estructura como un taller práctico de integración de datos.

Cada estudiante deberá modificar dos flujos desarrollados previamente:

| Herramienta | Origen de datos | Destino anterior | Nuevo destino |
|---|---|---|---|
| Pentaho Data Integration | Servicio WSDL | CSV / Excel | SQL Server |
| Power Automate | API pública | Google Sheets / Excel | SQL Server |

---

# Resultado mínimo esperado

Al finalizar la sesión, el estudiante deberá lograr:

- crear al menos una tabla en SQL Server
- establecer conexión desde alguna herramienta de integración
- insertar registros correctamente en SQL Server
- validar visualmente la carga de datos

Idealmente, el estudiante logrará integrar ambas herramientas con SQL Server.

---

# Material de apoyo

## Taller principal

- `Taller_1-Instrucciones.md`

## Anexos técnicos

### Pentaho Data Integration → SQL Server

- `Anexo_A-SQL_Server-PDI.md`

Contenidos principales:
- instalación de JDBC Driver
- configuración TCP/IP
- autenticación SQL Server
- conexión JDBC desde Spoon
- uso de `Table Output`
- solución de errores frecuentes

### Power Automate → SQL Server

- `Anexo_B-SQL_Server-Power-Automate.md`

Contenidos principales:
- uso del conector SQL Server
- autenticación
- gateway local
- acciones CRUD
- Insert Row (V2)
- limitaciones técnicas y optimización

---

# Referencias oficiales

## Pentaho Data Integration

- https://docs.pentaho.com
- https://docs.pentaho.com/pdia-data-integration

## Microsoft Power Automate

- https://learn.microsoft.com/en-us/connectors/sql/
- https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-onprem

---

# Relación con el proyecto del semestre

Este taller se conecta directamente con la segunda evaluación del curso, donde los estudiantes deben:

- construir procesos ETL reales
- integrar múltiples fuentes de datos
- crear bases de datos operacionales
- construir modelos dimensionales
- preparar los datos para análisis multidimensional

La conexión hacia SQL Server constituye una transición fundamental desde procesos de integración básicos hacia arquitecturas reales de Business Intelligence.

---

# Recomendaciones

Antes de iniciar el taller:

- verificar acceso a SQL Server
- comprobar credenciales
- validar habilitación de TCP/IP
- revisar instalación de JDBC Driver
- tener disponibles los flujos trabajados previamente en clases

---

# Archivos asociados

| Archivo | Descripción |
|---|---|
| Taller_1-Instrucciones.md | Guía principal del taller |
| Anexo_A-SQL_Server-PDI.md | Integración PDI → SQL Server |
| Anexo_B-SQL_Server-Power-Automate.md | Integración Power Automate → SQL Server |

---

# Observación final

El objetivo principal de esta sesión no es únicamente insertar datos en SQL Server, sino comprender cómo las herramientas de integración permiten construir arquitecturas reales de Business Intelligence orientadas a centralizar información, automatizar procesos y preparar datos para análisis posteriores.
