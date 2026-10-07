# 🚀 Guía de Instalación, Configuración y Despliegue Local (Días 3-5)

> **Proyecto:** Online Store / GroStop  
> **Equipo:** Célula de Desarrollo 5  
> **Entorno de Ejecución:** Docker Compose (Flask + MySQL 8.0)  

---

## 📋 1. Requisitos Previos

Antes de iniciar con la instalación, se verificó que el equipo contara con las siguientes herramientas instaladas y ejecutándose en sus entornos locales:

1. **Docker Desktop** (con soporte para Docker Compose activo).
2. **Git Bash** o **PowerShell** (con permisos de administrador).
3. **Visual Studio Code** (con extensión de Docker y Python opcionales).

---

## ⚙️ 2. Paso a Paso: Clonación y Despliegue del Proyecto

A continuación se detallan los pasos exactos que funcionaron en nuestras máquinas para levantar la infraestructura desde cero:

### Paso 1: Obtener el Código Fuente
Abrir la terminal (PowerShell o Git Bash) y clonar el repositorio del equipo:


git clone [https://github.com/Quantum-Code-GroStop/Online-Store.git](https://github.com/Quantum-Code-GroStop/Online-Store.git)
cd Online-Store

## Paso 2: Limpieza de Entorno y Contenedores Previos
Para asegurar que no existieran conflictos de puertos (puerto 5000 para Flask y 3306 para MySQL) ni volúmenes corrompidos de pruebas pasadas, ejecutamos:

Bash
docker compose down -v
Paso 3: Construcción y Levantamiento de Contenedores
Construimos la imagen de la aplicación Flask y levantamos el contenedor de la base de datos MySQL en segundo plano (-d):

Bash
docker compose up --build -d
Verificación de estado: Ejecutar docker ps para confirmar que ambos contenedores (web y db) se encuentren en estado Up.

Paso 4: Inyección e Inicialización de la Base de Datos
El contenedor de MySQL (grostop_db) requiere la estructura inicial de tablas y datos. Importamos el archivo Dump.sql directamente dentro del contenedor en ejecución:

En PowerShell:

PowerShell
Get-Content Dump.sql | docker exec -i grostop_db mysql -u root -proot grostop_db
En Git Bash / Linux / macOS:

Bash
docker exec -i grostop_db mysql -u root -proot grostop_db < Dump.sql
## 3. Verificación de Funcionamiento
Una vez completados los pasos anteriores, verificamos el correcto despliegue realizando las siguientes pruebas:

Abrir el navegador e ingresar a: http://localhost:5000 o http://127.0.0.1:5000.

Confirmar que la pantalla principal (homePage.html) cargue sin errores de conexión a la base de datos (Error 500).

Probar la navegación hacia la tienda (/home/231), verificando que los productos se desplieguen con precios en $ MXN y las imágenes carguen correctamente desde el contenedor.

##4. Problemas Encontrados y Soluciones Aplicadas (Bitácora de Ajustes)
Durante el proceso de despliegue en nuestras máquinas locales, identificamos y resolvimos los siguientes inconvenientes técnicos:

Incapacidad de conectar Flask con MySQL dentro de Docker:

Problema: El archivo de configuración utilizaba MYSQL_HOST = 'localhost', lo que hacía que el contenedor web buscara la base de datos dentro de sí mismo en lugar del contenedor de MySQL.

Solución: Modificamos la variable a MYSQL_HOST = 'db' en market/__init__.py y database.yaml, aprovechando la red interna que genera Docker Compose.

Conflicto con la contraseña del usuario Root de MySQL:

Problema: Al modificar el archivo .env o el docker-compose.yml, los cambios de contraseña no se aplicaban porque el volumen grostop_db mantenía la configuración vieja.

Solución: Se ejecutó docker compose down -v para borrar el volumen persistente anterior y permitir que MySQL se reinicializara con las credenciales correctas definidas en la infraestructura.

## 5. Comandos Frecuentes de Uso Diario
Para trabajar en el proyecto día a día sin necesidad de reconfigurar todo el entorno:

Iniciar la aplicación:

Bash
docker compose up -d
Detener la aplicación (preservando datos):

Bash
docker compose stop
Ver logs del backend en tiempo real (para depuración de errores):

Bash
docker compose logs -f web
Reconstruir cambios tras modificar archivos HTML/CSS/Python:

Bash
docker compose up --build -d
