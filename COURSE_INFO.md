# Curso: Inteligencia de Negocios

Este repositorio contiene el material del curso **Inteligencia de Negocios**, centrado en el desarrollo de soluciones analíticas para apoyar procesos de toma de decisiones organizacionales.

El curso se organiza en torno a un proyecto aplicado, en el cual los estudiantes desarrollan un sistema de Business Intelligence utilizando datos abiertos del sistema educativo chileno.

---

# Objetivo del curso

Comprender cómo las organizaciones utilizan datos para apoyar la toma de decisiones mediante procesos de:

- integración de datos
- modelamiento dimensional
- construcción de indicadores
- visualización de información mediante dashboards

---

# Proyecto del curso

Durante el semestre los estudiantes desarrollarán una solución de Inteligencia de Negocios utilizando datos abiertos del **Ministerio de Educación de Chile**.

Producto final del curso:

**Dashboard analítico de matrícula escolar en Chile**

---

# Arquitectura del proyecto

El proyecto del curso sigue una arquitectura básica de Business Intelligence:

Datos abiertos MINEDUC  
↓  
Exploración de datos  
↓  
Procesos ETL  
↓  
Modelo dimensional  
↓  
Dashboard BI  
↓  
Análisis para la toma de decisiones

---

# Modelo analítico

El modelo analítico del proyecto se basa en un **esquema estrella**.

## Tabla de hechos

**Hecho_Matricula**

Medida principal:

- matrícula_total

## Dimensiones

- Dim_Tiempo
- Dim_Establecimiento
- Dim_Territorio
- Dim_Dependencia
- Dim_Nivel_Educativo

---

# Organización del curso

El curso se desarrolla en **15 sesiones presenciales** organizadas en cuatro unidades:

| Unidad | Tema |
|------|------|
| U1 | Introducción a Business Intelligence |
| U2 | Analítica de negocios |
| U3 | Gobierno de datos |
| U4 | Gestión de proyectos BI |

---

# Entregables del proyecto

| Entregable | Contenido |
|---|---|
| 1 | Exploración y comprensión de los datos |
| 2 | Diseño del modelo dimensional |
| 3 | Implementación del modelo analítico |
| 4 | Dashboard final y análisis BI |

---

# Autor

Julio López Núñez  
Ingeniero en Computación e Informática  
Doctor en Política y Gestión Educativa
