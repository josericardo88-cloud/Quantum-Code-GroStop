
# Bitácora Individual de Trabajo

* **Nombre del Alumno:** José Ricardo Orozco Sauceda
* **Célula:** Célula 5 - Quantum Code
* **Rol Asignado:** Product Owner & Líder de Célula
* **Proyecto:** GroStop (E-Commerce Grocery Store)

---

## Registro Diario de Actividades

### 🗓️ Fecha: 23 / 09 / 2026 | Día 1: Planificación y Setup del Repositorio

* **Actividades Realizadas:**
  * Clonación local del repositorio oficial `Quantum-Code-GroStop`.
  * Análisis del perfil de los 5 integrantes del equipo para la asignación estratégica de roles (Product Owner, UML, Backend/Lógica, Backend/Datos, QA).
  * Definición del entorno de base de datos más óptimo para el equipo, seleccionando XAMPP/phpMyAdmin por rendimiento y facilidad de uso frente a SQL Server Management Studio.
  * Diseño inicial de la arquitectura de carpetas dentro de la documentación (`docs/` y `docs/bitacoras/`).

* **Pruebas y Hallazgos en el Sistema:**
  * Se identificó la necesidad de adaptar el flujo de trabajo a la nula experiencia previa del equipo con Git/GitHub.

* **Errores Encontrados y Soluciones Aplicadas:**
  * **Problema:** Riesgo de conflictos en el código si el equipo trabajaba directo sobre la rama principal.
  * **Solución:** Diseño de una estrategia estricta de ramas individuales (`rama-nombre-rol`) para aislar el trabajo de cada integrante.

* **Dudas o Aspectos por Aclarar:**
  * Definir la estructura exacta que tendrá el documento ejecutable de la descripción del sistema.

---

### 🗓️ Fecha: 26 / 09 / 2026 | Día 2: Onboarding del Equipo, Estructuración y Prompts de Apoyo

* **Actividades Realizadas:**
  * Creación y subida de mi rama individual de trabajo `rama-jose-po`.
  * Creación de la plantilla estandarizada `PLANTILLA.md` y de los 5 archivos individuales de bitácora dentro de `docs/bitacoras/`.
  * Elaboración y distribución del documento PDF *"Guía de Inicio Rápido: Creación de Ramas y Entorno"* para el equipo.
  * Definición del plan de acción paso a paso para Backend (Kevin y Yahir), Modelado UML (Javier) y QA/Docker (Josué).
  * Redacción y entrega de 3 "Prompts Maestros de IA" adaptados a cada integrante para guiarlos paso a paso sin depender de tecnicismos complejos.
  * Coordinación y comunicación por WhatsApp sobre el uso obligatorio de las bitácoras individuales.

* **Pruebas y Hallazgos en el Sistema:**
  * Se confirmó que todos los integrantes del equipo comprendieron su rol asignado, el uso de su rama individual y el proceso de llenado de bitácoras.

* **Errores Encontrados y Soluciones Aplicadas:**
  * **Problema:** Posible saturación de información técnica y limitación de recursos de hardware en algunos integrantes (laptops con pocos recursos).
  * **Solución:** Implementación de analogías didácticas (ej. la caja hermética para explicar Docker, la fotocopia para explicar Ramas) y selección de herramientas ligeras en la nube como Draw.io.

* **Dudas o Aspectos por Aclarar:**
  * Verificar en las siguientes 24 horas que todos los integrantes hayan realizado el push de sus ramas y su primer commit de bitácora en GitHub.

 ---

### 🗓️ Fecha: 26 / 09 / 2026 | Día 3: Redacción de la Descripción del Sistema e Integración de Mermaid

* **Actividades Realizadas:**
  * Redacción completa del documento ejecutable `docs/descripcion_sistema.md` definiendo objetivos, actores (Cliente y Admin), módulos y stack tecnológico.
  * Creación de un **Diagrama de Casos de Uso** y un **Diagrama Entidad-Relación (ERD)** utilizando código **Mermaid.js** directamente en Markdown.
  * Estructuración de la tabla del stack tecnológico y del listado oficial de roles de la Célula 5.

* **Pruebas y Hallazgos en el Sistema:**
  * Se verificó que GitHub renderiza de forma visual e interactiva los bloques de código Mermaid en el navegador sin necesidad de subir imágenes estáticas.

* **Errores Encontrados y Soluciones Aplicadas:**
  * **Problema 1:** Desformateo del diagrama Entidad-Relación debido a la falta de etiquetas de cierre (```) y espacio de línea en el bloque Mermaid.
  * **Problema 2:** Agrupación involuntaria de la lista numerada en un solo párrafo por omisión de renglones vacíos.
  * **Solución:** Se ajustó la sintaxis Markdown delimitando correctamente los bloques de código y agregando saltos de línea para un renderizado visual perfecto.

* **Dudas o Aspectos por Aclarar:**
  * Monitorear que los integrantes sigan avanzando en el levantamiento local del sistema.
