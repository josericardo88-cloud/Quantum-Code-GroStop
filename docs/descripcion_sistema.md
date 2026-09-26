# Descripción del Sistema: GroStop (E-Commerce)

* **Célula de Desarrollo:** Célula 5 - Quantum Code
* **Product Owner / Líder de Proyecto:** José Ricardo Orozco Sauceda
* **Proyecto:** GroStop - Tienda de Abarrotes en Línea
* **Fecha de Documentación:** Septiembre 2026

---

##  1. Introducción y Propósito del Sistema

**GroStop** es una plataforma web de comercio electrónico (e-commerce) diseñada para la gestión, venta y distribución de productos de abarrotes y canasta básica en línea. El sistema busca optimizar la experiencia de compra del cliente final al permitirle explorar catálogos digitalizados, gestionar su carrito de compras en tiempo real y realizar pedidos de forma rápida y segura.

Asimismo, la plataforma provee una interfaz administrativa centralizada para el control de inventarios, gestión de usuarios, registro de categorías y monitoreo de las ventas realizadas por la tienda.

---

##  2. Objetivos del Proyecto

### Objetivo General
Desarrollar e implementar una plataforma web e-commerce funcional, escalable y segura utilizando la arquitectura **Python/Flask** e integración con bases de datos **MySQL**, facilitando la compra-venta de productos de abarrotes en un entorno digital.

### Objetivos Específicos
1. **Digitalización del Catálogo:** Clasificar y desplegar productos de la canasta básica con precios, stock actualizado e imágenes representativas.
2. **Gestión de Carrito y Compras:** Permitir al usuario seleccionar múltiples productos, calcular montos totales en tiempo real y simular la confirmación de la orden.
3. **Módulo de Administración (Backoffice):** Brindar a los administradores herramientas para altas, bajas, cambios y consultas (CRUD) sobre el inventario y categorías.
4. **Despliegue y Contenerización:** Estructurar el entorno mediante contenedores aislados (Docker) para garantizar la portabilidad y ejecución uniforme del software.

---

##  3. Módulos y Roles del Sistema

El sistema divide sus funcionalidades en dos perfiles o actores principales:

### 3.1. Módulo del Cliente (Front-Office)
* **Autenticación:** Registro de nuevos clientes e inicio de sesión seguro.
* **Exploración de Productos:** Catálogo dinámico organizado por categorías (lácteos, frutas/verduras, enlatados, limpieza, etc.).
* **Carrito de Compras:** Opción para agregar, incrementar, reducir o eliminar artículos antes de finalizar la transacción.
* **Procesamiento de Pedido:** Confirmación de la orden con resumen detallado del costo total y datos de entrega.

### 3.2. Módulo de Administración (Back-Office)
* **Gestión de Inventario (CRUD):** Módulo para agregar nuevos productos, actualizar precios/fotografías o dar de baja ítems agotados.
* **Gestión de Categorías:** Control de la estructura del catálogo general.
* **Visualización de Ventas:** Panel centralizado para revisar los pedidos recibidos y su estatus.

---

## 📐 4. Diagrama de Casos de Uso (UML)

El siguiente diagrama ilustra las interacciones de cada actor con los módulos clave del sistema GroStop:

```mermaid
graph LR
    subgraph Actores
        C[👤 Cliente]
        A[👨‍💼 Administrador]
    end

    subgraph Sistema GroStop
        UC1((Registrarse / Login))
        UC2((Ver Catálogo de Abarrotes))
        UC3((Buscar y Filtrar Productos))
        UC4((Gestionar Carrito de Compras))
        UC5((Procesar y Confirmar Pedido))
        
        UC6((Gestionar Productos - CRUD))
        UC7((Gestionar Categorías - CRUD))
        UC8((Ver Reporte de Ventas))
    end

    C --> UC1
    C --> UC2
    C --> UC3
    C --> UC4
    C --> UC5

    A --> UC1
    A --> UC6
    A --> UC7
    A --> UC8
