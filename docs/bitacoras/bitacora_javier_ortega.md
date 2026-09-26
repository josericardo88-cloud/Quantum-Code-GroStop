# Bitácora de Actividades

**Fecha:** 21 de septiembre de 2026

**Nombre del Alumno:** Ortega Cortez Javier Aram

**Célula:** Célula 5 - Quantum Code

**Rol Asignado:** Backend

**Proyecto:** GroStop (E-Commerce Grocery Store)

---

## Actividades Realizadas

Se trabajó en la puesta en marcha del proyecto GroStop en un entorno local con Windows. Las actividades del día fueron:

- Descarga y revisión del repositorio `ECommerce-Grocery-Store`.
- Instalación y configuración de MySQL Server, ya que inicialmente se confundió con los conectores de Python (`mysqlclient`, `Flask-MySQLdb`) que aparecen en el `requirements.txt`.
- Configuración de la variable de entorno `PATH` para poder usar el comando `mysql` desde cualquier ubicación en CMD.
- Creación del entorno virtual con `py -m venv online_store` y activación mediante `.\online_store\Scripts\activate.bat`.
- Instalación de las dependencias del proyecto desde `requirements.txt`.
- Corrección del archivo `market\__init__.py` para adaptarlo a la versión actual de PyYAML.
- Intento de ejecución del proyecto con `python run.py`.

---

## Pruebas y Hallazgos en el Sistema

- Se verificó la instalación de MySQL con `mysql --version`, confirmando que el servidor y el cliente quedaron correctamente instalados.
- Se revisó el contenido del `requirements.txt` y se detectó que varias versiones de librerías eran incompatibles con Python 3.13.
- Se comprobó que la base de datos `online_store` y el dump `Dump.sql` son necesarios para que el sitio funcione, ya que el proyecto depende de un servidor MySQL activo (no basta con los conectores de Python).
- Se exploró la estructura del proyecto y se identificó que la configuración de la base de datos se carga desde un archivo `database.yaml` mediante PyYAML.
- Al ejecutar `python run.py`, el sistema cargó el módulo `market` pero falló en la lectura del archivo YAML.

---

## Errores Encontrados y Soluciones Aplicadas

**Problema 1:** Al ejecutar `pip install -r requirements.txt`, falló la compilación de `PyYAML` con el error `AttributeError: 'build_ext' object has no attribute 'cython_sources'`.

**Solución:** Se detectó que era un problema de incompatibilidad entre versiones antiguas de PyYAML y Cython 3.x. Se actualizó la línea del `requirements.txt` a `pyyaml>=6.0.2`, que ya incluye soporte para Cython 3.

---

**Problema 2:** Al instalar las dependencias, falló la compilación de `greenlet==1.1.2` y `mysqlclient==2.1.0` con el error `Microsoft Visual C++ 14.0 or greater is required`.

**Solución:** Se identificó que esas versiones antiguas no tienen wheels binarios para Python 3.13 y forzaban una compilación desde código fuente. Se actualizaron ambas versiones en el `requirements.txt`:
- `greenlet>=3.1`
- `mysqlclient==2.2.5`

Con esas versiones, `pip` descargó wheels precompilados y la instalación se completó sin necesidad del compilador de C++.

---

**Problema 3:** El comando `mysql` no era reconocido en CMD (`"mysql" no se reconoce como un comando interno o externo`), a pesar de que MySQL Server estaba instalado.

**Solución:** Se revisó el `PATH` con `echo %PATH%` y se detectó que solo estaba la ruta de `MySQL Shell 8.0\bin`, pero no la de `MySQL Server 8.0\bin`. Se agregó manualmente la ruta `C:\Program Files\MySQL\MySQL Server 8.0\bin` a las variables de entorno del sistema y se reinició CMD.

---

**Problema 4:** Al ejecutar `python run.py`, apareció `TypeError: load() missing 1 required positional argument: 'Loader'` en la línea 9 de `market\__init__.py`.

**Solución:** Se identificó que PyYAML 6.x ya no permite usar `yaml.load()` sin especificar un `Loader`. Se reemplazó la línea:
```python
db = yaml.load(open('database.yaml'))
```
por:
```python
db = yaml.safe_load(open('database.yaml'))
```

# Comparación de `requirements.txt`

## Versión Original (con errores)

```txt
bidict==0.22.0
click==8.1.2
colorama==0.4.4
Flask==2.1.1
Flask-MySQLdb==1.0.1
Flask-SocketIO==5.1.1
Flask-SQLAlchemy==2.5.1
Flask-WTF==1.0.1
greenlet==1.1.2
importlib-metadata==4.11.3
itsdangerous==2.1.2
Jinja2==3.1.1
MarkupSafe==2.1.1
mysqlclient==2.1.0
PyMySQL==1.0.2
pyparsing==3.0.8
python-dateutil==2.8.2
python-engineio==4.3.1
python-socketio==5.5.2
pytz==2022.1
pyyaml>=6.0.2
six==1.16.0
SQLAlchemy==1.4.35
Werkzeug==2.1.1
WTForms==3.0.1
zipp==3.8.0
```
## Versión Modificada (funcional con Python 3.13)
```txt
bidict==0.22.0
click==8.1.2
colorama==0.4.4
Flask==2.1.1
Flask-MySQLdb==1.0.1
Flask-SocketIO==5.1.1
Flask-SQLAlchemy==2.5.1
Flask-WTF==1.0.1
greenlet>=3.1
importlib-metadata==4.11.3
itsdangerous==2.1.2
Jinja2==3.1.1
MarkupSafe==2.1.1
mysqlclient==2.2.5
PyMySQL==1.0.2
pyparsing==3.0.8
python-dateutil==2.8.2
python-engineio==4.3.1
python-socketio==5.5.2
pytz==2022.1
pyyaml>=6.0.2
six==1.16.0
SQLAlchemy==1.4.35
Werkzeug==2.1.1
WTForms==3.0.1
zipp==3.8.0
```
