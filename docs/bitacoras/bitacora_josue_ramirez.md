# Bitácora de Trabajo - QA / Git Manager
**Nombre:** Josué Emmanuel Ramírez Cruz
**Rol:** QA / Control de Versiones

---

## Fecha: 26/09/2026

### Actividades realizadas
- Verificación de la estructura de ramas del repositorio oficial en GitHub.
- Cambio de entorno a la rama asignada (`rama-josue-qa`).
- Inspección de la raíz del proyecto para verificar la presencia de Docker.

### Hallazgos
- **Control de Versiones:** La rama `rama-yahir-datos` aún no está presente en el servidor remoto (integrante reporta falta de acceso a internet).
- **Docker:** No se localizan los archivos `Dockerfile` ni `docker-compose.yml` en la raíz del proyecto.

### Pendientes
- Apoyar a Yahir cuando restablezca su conexión para verificar su rama.
- Trabajar en la preparación de los archivos de contenerización (Dockerfile y docker-compose.yml) junto con el equipo.

### Pruebas QA
- **Módulo probado:** Registro de usuarios.
- **Resultado:** Fallido (Error 500 Internal Server Error).
- **Acción tomada:** Se tomó evidencia mediante captura de pantalla y se reportó al área de Backend.




# Bitácora de QA y Despliegue Local - Proyecto GroStop

**Integrante / Tester QA:** Josué Emmanuel Ramírez Cruz

**Rama de Git:** `rama-josue-qa`

**Entorno de Desarrollo:** Windows (PowerShell / VS Code), Docker Desktop, WSL2

---

## 🛠️ Resumen de Trabajos Realizados

1. **Configuración y Levantamiento del Entorno Local:**
* Despliegue de los contenedores web (Flask) y base de datos (MySQL) mediante Docker Compose.
* Ajuste de variables de conexión en `database.yaml` para alinearlas con los valores definidos en `docker-compose.yml`.


2. **Depuración y Resolución de Errores de Base de Datos:**
* Diagnóstico del error HTTP 500 al intentar registrar clientes en `/customerRegister`.


* Corrección de fallos de autenticación de MySQL limpiando volúmenes persistentes de Docker (`docker compose down -v`).
* Importación exitosa del esquema y datos iniciales mediante `Dump.sql` hacia el contenedor `grostop_db`.


3. **Pruebas de Funcionalidad (QA Testing):**
* Validación end-to-end del módulo de registro de usuarios (`/customerRegister`).
* Confirmación de inserción de registros en la base de datos relacional y retroalimentación en la interfaz gráfica.


4. **Control de Versiones y Sincronización:**
* Resolución manual de conflictos de *merge* en Git sobre archivos modificados (`Dump.sql`, `run.py`, `market/__init__.py`).
* Cierre de commit de fusión y *push* exitoso a la rama remota `rama-josue-qa`.



---

## 📝 Registro Detallado de Sesiones (Bitácora de Pruebas)
## 📝 Registro Detallado de Sesiones (Bitácora de Pruebas)

<details>
<summary><b>🔴 Sesión 1: Registro (/customerRegister)</b> — <i>Estado: ❌ Fallido</i></summary>
<br>

* **Acción realizada:** Envío de formulario de registro de clientes.
* **Resultado obtenido:** **Error 500 (Internal Server Error)** en el navegador por fallo de autenticación de MySQL (`Access denied for user 'root'`).
* **Solución aplicada:** Se identificó un descalce entre la contraseña guardada en el volumen persistente de Docker y `database.yaml`.

---
</details>

<details>
<summary><b>🟢 Sesión 2: Infraestructura / Docker</b> — <i>Estado: ✔️ Resuelto</i></summary>
<br>

* **Acción realizada:** Limpieza de volúmenes antiguos y reinicio de contenedores.
* **Resultado obtenido:** Los contenedores se recrearon con la contraseña `root` correctamente enlazada.
* **Solución aplicada:** Se ejecutó `docker compose down -v` seguido de `docker compose up --build -d`.

---
</details>

<details>
<summary><b>🟢 Sesión 3: Base de Datos (MySQL)</b> — <i>Estado: ✔️ Resuelto</i></summary>
<br>

* **Acción realizada:** Importación del script de volcado de datos `Dump.sql`.
* **Resultado obtenido:** **ERROR 2002 (HY000)** en PowerShell al no estar MySQL completamente listo durante la inicialización.
* **Solución aplicada:** Se esperaron 15 segundos para la inicialización del socket y se reejecutó:  
  `Get-Content Dump.sql | docker exec -i grostop_db mysql -u root -proot grostop_db`

---
</details>

<details>
<summary><b>🟢 Sesión 4: Registro (/customerRegister)</b> — <i>Estado: ✔️ Exitoso</i></summary>
<br>

* **Acción realizada:** Registro de un nuevo cliente de prueba en la plataforma.
* **Resultado obtenido:** Muestra el banner *"You have registered successfully!"* en la interfaz.
* **Solución aplicada:** Se verificó la persistencia del usuario registrado directamente en la base de datos `grostop_db`.

---
</details>

<details>
<summary><b>🟢 Sesión 5: Git / Control de Cambios</b> — <i>Estado: ✔️ Resuelto</i></summary>
<br>

* **Acción realizada:** Intento de push tras resolver divergencias de ramas.
* **Resultado obtenido:** Git notificó un estado inconcluso (`All conflicts fixed but you are still merging`).
* **Solución aplicada:** Se agregaron los archivos de configuración (`run.py`), se cerró el commit con `git commit -m "..."` y se subió con `git push origin rama-josue-qa`.

---
</details>
---

## 📌 Observaciones Técnicas y Notas para el Equipo

Para que cualquier integrante del equipo pueda levantar el proyecto en su máquina sin encontrarse con los errores resueltos en esta rama, debe seguir estas recomendaciones:

1. **Secuencia limpia de arranque:**
```powershell
# 1. Limpiar volúmenes para evitar descalces de contraseña
docker compose down -v

# 2. Reconstruir e iniciar contenedores
docker compose up --build -d

# 3. Esperar 15 segundos a que la BD responda y luego importar Dump.sql
Get-Content Dump.sql | docker exec -i grostop_db mysql -u root -proot grostop_db

```


2. **Manejo de `database.yaml`:**
No sobreescribir las credenciales locales de prueba si difieren de las configuraciones compartidas.
3. **Deuda Técnica Detectada:**
Actualmente el sistema utiliza consultas SQL puras con `Flask-MySQLdb` y cargas manuales de `Dump.sql`. Como propuesta de mejora para el entregable final del proyecto, se sugiere refactorizar la persistencia hacia un ORM (**Flask-SQLAlchemy**) con migraciones automáticas (**Flask-Migrate**).



---

### 🚀 Pasos para agregar esta bitácora a tu repositorio desde PowerShell:

1. Crea el archivo en la raíz del proyecto:
```powershell
New-Item -Path . -Name "BITACORA_QA_JOSUE.md" -ItemType "File"

```


2. Abre el archivo en VS Code, pega el texto de arriba y guárdalo (`Ctrl + S`).
3. Sube el nuevo archivo a tu rama en GitHub:
```powershell
git add BITACORA_QA_JOSUE.md
git commit -m "docs: agrega bitacora de pruebas de QA y guia de resolucion de errores"
git push origin rama-josue-qa

```
