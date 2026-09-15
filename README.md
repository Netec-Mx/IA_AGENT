# IA para el Manejo de Agentes

Repositorio de laboratorios del curso **260813 - IA para el Manejo de Agentes**. A lo largo de cinco capítulos se exploran los fundamentos de los agentes de inteligencia artificial, la ingeniería de prompts, la creación de agentes con conocimiento empresarial, la automatización de acciones y la evaluación de su desempeño.

## Objetivo del curso

Desarrollar una comprensión práctica del ciclo de vida de un agente de IA: desde la comparación de modelos y el diseño de instrucciones hasta la conexión con herramientas, la incorporación de supervisión humana y la mejora continua basada en métricas.

Al finalizar el recorrido podrás:

- Diferenciar un chatbot, un asistente y un agente de IA.
- Comparar modelos según su contexto, memoria, razonamiento, herramientas y autonomía.
- Diseñar instrucciones estructuradas para agentes especializados.
- Crear y publicar un agente con fuentes de conocimiento empresariales.
- Integrar acciones mediante Power Automate y SharePoint.
- Aplicar controles de aprobación humana (*human-in-the-loop*).
- Evaluar métricas, detectar respuestas incorrectas e implementar mejoras.

## Ruta de laboratorios

| Capítulo | Laboratorio | Plataforma | Duración | Modalidad |
|:---:|---|---|:---:|---|
| 1 | [Comparación de modelos de IA y análisis de comportamientos](./Capitulo01/) | Poe | 30 min | Práctica individual |
| 2 | [Diseño y construcción de un agente](./Capitulo02/) | Poe | 25 min | Práctica individual |
| 3 | [Creación y publicación de Nova Assistant](./Capitulo03/) | Microsoft Copilot Studio | 45 min | Demostrativa\* |
| 4 | [Integración de herramientas y aprobación de solicitudes](./Capitulo04/) | Copilot Studio, Power Automate y SharePoint | 30 min | Demostrativa\* |
| 5 | [Medición de desempeño y mejora continua](./Capitulo05/) | Microsoft Copilot Studio | 20 min | Demostrativa\* |

> \* Los capítulos 3, 4 y 5 requieren licenciamiento y permisos en el entorno de Microsoft. Cuando el participante disponga de estos accesos, también podrá realizarlos de manera individual.

## Recorrido de aprendizaje

1. **Explorar:** compara distintos modelos de IA en un entorno común y documenta sus diferencias.
2. **Diseñar:** define el rol, los objetivos, las restricciones, el contexto y el formato de respuesta de un agente.
3. **Construir:** crea **Nova Assistant** en Copilot Studio y conéctalo con documentos de conocimiento empresarial.
4. **Actuar:** integra flujos para registrar y consultar solicitudes, incorporando aprobación humana cuando corresponda.
5. **Mejorar:** analiza métricas, identifica errores y verifica el impacto de los ajustes realizados.

## Requisitos generales

### Para los capítulos 1 y 2

- Cuenta gratuita en [Poe](https://poe.com/).
- Google Chrome 124 o posterior, o Microsoft Edge 124 o posterior.
- Microsoft Excel o Google Sheets para completar las bitácoras.
- Conexión estable a internet.

### Para los capítulos 3, 4 y 5

- Licencia y acceso a [Microsoft Copilot Studio](https://copilotstudio.microsoft.com/).
- Acceso a [Power Automate](https://make.powerautomate.com/).
- Permisos para crear y administrar una lista de SharePoint.
- Cuenta de Microsoft 365 en el mismo entorno de trabajo.

Cada capítulo contiene sus prerrequisitos, archivos de apoyo, pasos de ejecución, resultados esperados y criterios de validación específicos.

## Estructura del repositorio

```text
IA_AGENT/
├── Capitulo01/    # Comparación de modelos en Poe
├── Capitulo02/    # Diseño de un agente en Poe
├── Capitulo03/    # Agente con conocimiento en Copilot Studio
├── Capitulo04/    # Herramientas, acciones y aprobación humana
├── Capitulo05/    # Métricas y mejora continua
└── Images/        # Capturas de apoyo para los laboratorios
```

Las carpetas de los capítulos incluyen su propia guía `README.md`. Algunos laboratorios también incorporan bitácoras en Excel y documentos de ejemplo para desarrollar y registrar las actividades.

## Cómo utilizar este repositorio

1. Ingresa al capítulo correspondiente desde la [ruta de laboratorios](#ruta-de-laboratorios).
2. Revisa los prerrequisitos y prepara los accesos solicitados.
3. Descarga o clona el repositorio:

   ```bash
   git clone https://github.com/Netec-Mx/IA_AGENT.git
   ```

4. Conserva una copia personal de cada bitácora antes de comenzar.
5. Ejecuta los pasos en orden y completa las verificaciones indicadas.
6. Guarda las evidencias y los artefactos generados durante cada práctica.

## Recomendaciones

- No ingreses información confidencial, credenciales ni datos personales en los modelos o agentes utilizados durante las prácticas.
- Usa información ficticia o anonimizada en los ejercicios.
- Verifica los costos o puntos de cómputo antes de seleccionar un modelo en Poe.
- Sigue las políticas de seguridad y gobierno de datos de tu organización.
- En entornos compartidos, elimina los recursos de prueba que ya no sean necesarios.

## Recursos oficiales

- [Poe](https://poe.com/)
- [Documentación de Microsoft Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/)
- [Documentación de Microsoft Power Automate](https://learn.microsoft.com/es-es/power-automate/)
- [Documentación de Microsoft SharePoint](https://learn.microsoft.com/es-es/sharepoint/)

---

Material de uso académico desarrollado para **Netec**.
