# Next.js Project Improvements
Este proyecto incluye diversas mejoras utilizando GitHub Actions para automatizar tareas clave en el desarrollo y mantenimiento del código.

## Introducción: ¿Qué son las GitHub Actions?

GitHub Actions es una plataforma que permite automatizar flujos de trabajo directamente desde los repositorios de GitHub. Permite a los desarrolladores definir procesos automatizados (llamados workflows) que se ejecutan en respuesta a eventos como `push`, `pull_request`, o mediante un cron job. Estos workflows se configuran utilizando archivos YAML y se componen de jobs que incluyen pasos para realizar tareas específicas.

### Conceptos principales

- **Workflow**: Conjunto de procesos automatizados definidos en un archivo YAML que se activan ante ciertos eventos.
- **Job**: Unidad de trabajo dentro de un workflow, compuesta por pasos que ejecutan comandos o acciones específicas.
- **Action**: Acciones preconfiguradas que permiten realizar tareas como checkout del código, ejecución de tests, o despliegues.
- **Runner**: Máquina donde se ejecutan los jobs. GitHub proporciona runners alojados o puedes configurar runners auto-hospedados.

GitHub Actions proporciona una manera eficiente de automatizar tareas repetitivas, reducir errores humanos, y mantener la calidad del código en los proyectos.

---

## Workflows Configurados

En este proyecto se han configurado varios workflows para mejorar y automatizar el desarrollo, las pruebas, y el despliegue de la aplicación Next.js. A continuación, se detalla cada uno de ellos:

### `linter_job`

- **Descripción**: Este job verifica que el código cumple con las reglas de estilo y calidad establecidas.
- **Pasos**:
  1. Descarga el código del repositorio utilizando `actions/checkout`.
  2. Instala las dependencias del proyecto con `npm install`.
  3. Ejecuta el linter utilizando el script `npm run lint`.
- **Beneficios**: Garantiza un código limpio y uniforme, detectando errores de sintaxis o estilo.

---

### `cypress_job`

- **Descripción**: Ejecuta pruebas `end-to-end` con Cypress para verificar el comportamiento de la aplicación.
- **Pasos**:
  1. Descarga el código del repositorio.
  2. Instala las dependencias del proyecto.
  3. Levanta un servidor de desarrollo de Next.js.
  4. Espera a que el servidor esté listo y ejecuta las pruebas configuradas en Cypress.
  5. Guarda los resultados de las pruebas en un archivo de artefacto.
- **Beneficios**: Asegura que las funcionalidades de la aplicación funcionan según lo esperado.

---

### `metrics_job`

- **Descripción**: Genera y actualiza dinámicamente métricas de los lenguajes más utilizados en el perfil de GitHub del desarrollador.
- **Pasos**:
  1. Descarga el código del repositorio.
  2. Utiliza la acción `lowlighter/metrics` para generar un gráfico de métricas basado en el perfil de GitHub.
  3. Actualiza el archivo `README.md` para incluir estas métricas.
- **Beneficios**: Proporciona una visión profesional y visual del perfil del desarrollador.

---

### `add_badge_job`

- **Descripción**: Actualiza el archivo `README.md` con un badge que refleja los resultados de las pruebas Cypress.
- **Pasos**:
  1. Descarga el código del repositorio.
  2. Lee los resultados de las pruebas Cypress desde el archivo de artefacto.
  3. Actualiza el archivo `README.md` para incluir un badge (verde si los tests pasaron, rojo si fallaron).
- **Beneficios**: Ofrece una referencia visual rápida sobre el estado de los tests en el proyecto.

---

### `deploy_job`

- **Descripción**: Despliega automáticamente la aplicación en la plataforma Vercel tras un push exitoso en la rama `main`.
- **Pasos**:
  1. Descarga el código del repositorio.
  2. Utiliza la acción `amondnet/vercel-action` para realizar el despliegue.
- **Beneficios**: Automatiza el proceso de despliegue, asegurando que los cambios estén disponibles en producción de manera eficiente.

---

### `notification_job`

- **Descripción**: Envía notificaciones a Telegram con el estado de cada job ejecutado en el workflow.
- **Pasos**:
  1. Construye un mensaje con el resultado de cada job.
  2. Utiliza la API de Telegram para enviar el mensaje al chat configurado.
- **Beneficios**: Proporciona retroalimentación en tiempo real sobre el estado de los workflows.

---

## Pasos Realizados

### Configuración de GitHub Actions

- Se configuró el archivo `workflow.yml` para definir los workflows mencionados.
- Se crearon secretos en el repositorio para manejar de forma segura tokens de acceso como:
  - `METRICS_TOKEN`: Permite acceder a la API de GitHub para generar métricas.
  - `PAT_TOKEN`: Token de acceso personal para realizar operaciones `push` en el repositorio.
  - `VERCEL_TOKEN`, `ORG_ID`, `PROJECT_ID`: Credenciales necesarias para el despliegue en Vercel.
  - `TELEGRAM_TOKEN`, `TELEGRAM_CHAT_ID`: Credenciales para enviar notificaciones a Telegram.

---

### Configuración de Métricas

- La acción `lowlighter/metrics` se utilizó para generar un gráfico de métricas. Se configuró para ignorar lenguajes irrelevantes como `html`, `css`, y `shell`, y limitar la cantidad de lenguajes mostrados a los cuatro más utilizados.

---

### Actualización Dinámica del README

- Tanto el job `metrics_job` como `add_badge_job` se diseñaron para actualizar dinámicamente el archivo `README.md`:
  - `metrics_job`: Añade un gráfico con métricas de lenguajes utilizados.
  - `add_badge_job`: Añade un badge con los resultados de Cypress.

---

### GitHub Actions: Ventajas y Conclusión

Las GitHub Actions son una herramienta poderosa para automatizar flujos de trabajo en proyectos de software. Este proyecto demuestra cómo utilizar estas acciones para mejorar la calidad del código, realizar pruebas automatizadas, generar métricas profesionales, y desplegar aplicaciones automáticamente.

Con la implementación de estos workflows, se logra:
- Incrementar la productividad del desarrollador.
- Reducir errores manuales.
- Mantener un estándar profesional en el desarrollo del proyecto.

---

### Notas finales

Este proyecto sirve como base para la implementación de buenas prácticas en el desarrollo de software utilizando herramientas modernas como GitHub Actions, Cypress, y Vercel.

## Resultados de Métricas

![Metrics](github-metrics.svg)

## Resultados de los Últimos Tests
![Test Badge](https://img.shields.io/badge/tested%20with-Cypress-04C38E.svg)


