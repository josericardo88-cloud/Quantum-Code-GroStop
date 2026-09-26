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
