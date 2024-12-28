# Documentación del Proyecto GitHub Actions

## Introducción
Este proyecto integra un conjunto de mejoras automatizadas mediante GitHub Actions para garantizar la calidad del código, ejecutar pruebas, generar métricas de rendimiento y realizar despliegues automáticos. La configuración permite mantener altos estándares de desarrollo y una entrega continua eficiente.

## Conceptos Clave

### GitHub Actions
GitHub Actions es una herramienta que automatiza flujos de trabajo dentro de repositorios. Permite ejecutar procesos definidos en archivos YAML llamados workflows.

**Elementos principales:**
- **Workflow:** Conjunto de procesos que se activan por eventos.
- **Job:** Unidad de trabajo que realiza pasos específicos.
- **Step:** Instrucción dentro de un job.
- **Action:** Tarea preconfigurada reutilizable.

### Cypress
Cypress es un framework para pruebas end-to-end que asegura la funcionalidad correcta de las aplicaciones web.

### Vercel
Vercel es una plataforma de despliegue que soporta frameworks como Next.js. Proporciona una integración fácil con GitHub para despliegues automáticos.

---

## Workflows Configurados

### Linter Job
**Descripción:** Verifica que el código cumpla con las reglas de estilo y calidad.

**Pasos:**
1. Realiza el checkout del código.
2. Instala las dependencias con `npm install`.
3. Ejecuta el linter con `npm run lint`.

**Resultados:** Asegura un código limpio y uniforme.

---

### Cypress Job
**Descripción:** Ejecuta pruebas end-to-end para verificar funcionalidades.

**Pasos:**
1. Realiza el checkout del código.
2. Instala dependencias.
3. Levanta un servidor de desarrollo con Next.js.
4. Ejecuta las pruebas configuradas.
5. Guarda resultados en un archivo `result.txt`.

**Resultados:** Valida que las funcionalidades operen como se espera.

---

### Add Badge Job
**Descripción:** Actualiza el README.md con un badge que refleja los resultados de las pruebas de Cypress.

**Pasos:**
1. Realiza el checkout del código.
2. Descarga los resultados generados por Cypress.
3. Determina el estado de los tests (success o failure).
4. Actualiza el README.md con el badge correspondiente.

**Resultados:** Proporciona una referencia visual del estado de las pruebas.

---

### Deploy Job
**Descripción:** Realiza el despliegue de la aplicación en Vercel.

**Pasos:**
1. Realiza el checkout del código.
2. Utiliza la action `amondnet/vercel-action` para desplegar el proyecto.

**Resultados:** Despliega automáticamente la aplicación en producción.

---

### Notification Job
**Descripción:** Envía una notificación con el estado de los jobs al bot de Telegram configurado.

**Pasos:**
1. Construye un mensaje con los resultados.
2. Envía el mensaje utilizando la API de Telegram.

**Resultados:** Informa en tiempo real sobre el estado del workflow.

---

### Metrics Job
**Descripción:** Genera gráficos de métricas basados en los lenguajes utilizados en el perfil de GitHub del desarrollador.

**Pasos:**
1. Utiliza la acción `lowlighter/metrics` para generar las métricas.
2. Actualiza el README.md con el gráfico generado.

**Resultados:** Ofrece una visión profesional del perfil del desarrollador.

---

## Configuración de Secrets

Los secrets utilizados son:
- `METRICS_TOKEN`: Para generar métricas.
- `PAT_TOKEN`: Token de acceso para operaciones de `push`.
- `VERCEL_TOKEN`, `ORG_ID`, `PROJECT_ID`: Credenciales para despliegue en Vercel.
- `TELEGRAM_TOKEN`, `TELEGRAM_CHAT_ID`: Credenciales para enviar notificaciones.

---

## Resultados de Métricas
![Metrics](github-metrics.svg)

## Resultados de los Últimos Tests
![Test Badge](https://img.shields.io/badge/tested%20with-Cypress-04C38E.svg)



