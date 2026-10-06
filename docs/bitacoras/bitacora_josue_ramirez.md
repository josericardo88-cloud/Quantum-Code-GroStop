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
Aquí tienes el bloque completo con los **cambios exactos de código (archivo y línea)** y los **comandos de PowerShell** necesarios. Este formato también utiliza el estilo desplegable para que se integre perfectamente con tu bitácora en GitHub.

Puedes copiar este bloque y pegarlo al final de tu archivo `BITACORA_QA_JOSUE.md`:

---

```markdown
## 🛠️ Cambios de Código Aplicados y Configuración de PowerShell

<details>
<summary><b>📂 1. Modificaciones en el Código Fuente (Archivos y Líneas)</b></summary>
<br>

* **Archivo:** `market/__init__.py`
  * **Línea modificada / agregada:** Configuración del cliente MySQL.
  * **Cambio realizado:** Se aseguraron los parámetros de conexión para el contenedor de la base de datos reemplazando el valor por defecto de `localhost` por el host del servicio de Docker Compose (`db`):
    ```python
    app.config['MYSQL_HOST'] = 'db'
    app.config['MYSQL_USER'] = 'root'
    app.config['MYSQL_PASSWORD'] = 'root'
    app.config['MYSQL_DB'] = 'grostop_db'
    ```

* **Archivo:** `run.py`
  * **Líneas 1-6:** Ajuste en el punto de entrada de la aplicación Flask.
  * **Cambio realizado:** Se verificó que el servidor dev modifique el host a `0.0.0.0` para permitir la comunicación bidireccional desde los contenedores de Docker hacia el navegador local:
    ```python
    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=5000, debug=True)
    ```

* **Archivo:** `database.yaml`
  * **Líneas 1-4:** Sincronización de credenciales locales.
  * **Cambio realizado:** Ajuste de variables para mantener paridad con `docker-compose.yml`:
    ```yaml
    mysql_host: 'db'
    mysql_user: 'root'
    mysql_password: 'root'
    mysql_db: 'grostop_db'
    ```

---
</details>

<details>
<summary><b>💻 2. Comandos de PowerShell para la Conexión y Carga de la BD</b></summary>
<br>

Para conectar e importar correctamente la base de datos sin errores de socket ni conflictos de volumen, se deben ejecutar los siguientes comandos en orden desde PowerShell dentro de la raíz del proyecto (`Quantum-Code-GroStop`):

1. **Ubicarse en el directorio del proyecto:**
   ```powershell
   cd "C:\Users\Quantum-Code-GroStop"

```

2. **Limpiar volúmenes corruptos y levantar los contenedores de Docker:**
```powershell
docker compose down -v
docker compose up --build -d

```


3. **Importar el esquema y volcados de datos (`Dump.sql`) a MySQL:**
*(Es importante esperar 10-15 segundos tras el `up` para que el servicio de MySQL acepte conexiones).*
```powershell
Get-Content Dump.sql | docker exec -i grostop_db mysql -u root -proot grostop_db

```


4. **Verificar que la base de datos recibió las tablas correctamente (Opcional):**
```powershell
docker exec -it grostop_db mysql -u root -proot -e "SHOW TABLES FROM grostop_db;"

```



---
git commit -m "docs: agrega bitacora de pruebas de QA y guia de resolucion de errores"
git push origin rama-josue-qa

```
