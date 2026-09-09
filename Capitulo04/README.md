# Integración de Herramientas en Nova Assistant: Registro y Aprobación de Solicitudes

## 1. Metadatos

| Campo | Valor |
|-------|-------|
| **Duración** | 30 minutos |
| **Complejidad** | Media-Alta |
| **Nivel Bloom** | Crear |
| **Módulo** | 4 — Uso de Herramientas y Acciones |
| **Plataforma** | Microsoft Copilot Studio + Power Automate |
| **Agente base** | Nova Assistant (creado en el Lab del Módulo 3) |
| **Requiere** | Licencia Microsoft 365 con Copilot Studio y Power Automate, permisos sobre un sitio de SharePoint |

> ⚠️ **Nota de modalidad:** igual que el laboratorio del Módulo 3, este requiere licenciamiento que por ahora solo tiene Aurora, así que **se ejecuta en modalidad demostrativa**. En cuanto un participante tenga licencia, este documento funciona como laboratorio individual sin cambios.

---

## 2. Descripción General

Hasta el Módulo 3, Nova Assistant solo podía **responder con información** (RAG sobre documentos). En este laboratorio le agregas la capacidad de **ejecutar una acción real**: registrar una solicitud de vacaciones, y — si la solicitud supera cierto número de días — pausar el proceso para pedir aprobación humana antes de confirmarla. Esto es el patrón que separa a un asistente conversacional de un agente que participa en un proceso de negocio real.

Construyes dos herramientas (flujos de Power Automate) y las conectas a Nova Assistant:

1. **RegistrarVacacionesFlow** — crea la solicitud en SharePoint y, si son más de 10 días, pausa el flujo pidiendo aprobación a un supervisor antes de confirmar.
2. **ConsultarEstadoVacacionesFlow** — permite que el agente responda "¿ya se aprobó mi solicitud?" consultando el estado real en SharePoint.

Esto comprime en una sola narrativa los tres conceptos centrales del Módulo 4: herramientas/acciones, automatización de tareas, y aprobación con intervención humana (dejamos fuera, deliberadamente, la integración con un ERP externo vía conector personalizado — es un salto de complejidad que no aporta un concepto pedagógico distinto).

---

## 3. Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Explicar la diferencia entre un agente que solo responde con información y uno que puede ejecutar acciones reales (patrón herramientas/acciones).
- [ ] Configurar un flujo de Power Automate con lógica condicional que decida automáticamente si una solicitud necesita aprobación humana.
- [ ] Conectar ese flujo a un agente de Copilot Studio como una herramienta invocable.
- [ ] Explicar qué es el patrón *human-in-the-loop* y por qué es necesario para ciertas decisiones automatizadas.
- [ ] Validar el ciclo completo: conversación → acción → (aprobación opcional) → confirmación → consulta de estado.

---

## 4. Prerrequisitos

### Conocimientos previos

| Requisito | Descripción |
|-----------|-------------|
| Lab del Módulo 3 completado | Nova Assistant existe, con instrucciones y los 3 documentos de conocimiento cargados |
| Conceptos de Power Automate | Triggers, condiciones, acciones — no requiere experiencia previa profunda |

### Acceso requerido

| Recurso | Detalle |
|---------|---------|
| Copilot Studio | Acceso al agente Nova Assistant existente |
| Power Automate | `https://make.powerautomate.com`, mismo entorno que Copilot Studio |
| SharePoint | Sitio con permisos de creación de listas (ver Paso 1) |
| Un correo de "supervisor" | Puede ser tu propio correo, para recibir las aprobaciones durante la demo |

---

## 5. Preparación Previa (hazlo antes de la sesión)

### Crear la lista de SharePoint

1. Ve a un sitio de SharePoint donde tengas permisos (puede ser el mismo que usarás para futuros laboratorios de TechNova).
2. Crea una lista nueva llamada **`SolicitudesVacacionesTechNova`**.
3. Agrega las siguientes columnas:

| Columna | Tipo | Notas |
|---|---|---|
| Title | Línea de texto (ya viene por defecto) | Úsala para el nombre del empleado |
| CorreoEmpleado | Línea de texto | Para poder enviar la confirmación |
| FechaInicio | Fecha | |
| FechaFin | Fecha | |
| DiasSolicitados | Número | |
| Estado | Opción: `Pendiente`, `Aprobada`, `Rechazada` | Valor por defecto: `Pendiente` |

4. Anota la URL completa del sitio — la necesitarás en el Paso 2 (ejemplo: `https://tuempresa.sharepoint.com/sites/TechNovaLab`).
5. Define qué correo usarás como "supervisor aprobador" durante la demo (puede ser el tuyo).

> No necesitas cargar datos de ejemplo en la lista — el flujo del Paso 2 la va a llenar durante las pruebas.

---

## 6. Instrucciones Paso a Paso

### Paso 1: Crear el flujo `RegistrarVacacionesFlow` desde Copilot Studio

**Objetivo:** Construir el flujo que recibe los datos de la solicitud, la registra, y decide si necesita aprobación — creándolo desde el lugar correcto para que quede automáticamente vinculado al agente.

> ⚠️ **Importante:** en la experiencia moderna de Copilot Studio, **no** busques el trigger "When Copilot calls a flow" directamente en Power Automate — ya no aparece de forma confiable en la lista de triggers al crear un flujo desde ahí. El flujo se crea **desde dentro de Copilot Studio**, que lo vincula automáticamente.

**Instrucciones:**

1. Abre Nova Assistant en Copilot Studio.

![Imagen 034](../images/imagen034.png)

2. Ve a la pestaña **Tools** y haz clic en **Add tool**.

![Imagen 035](../images/imagen035.png)

3. Selecciona **Add new → Workflows**.

![Imagen 036](../images/imagen036.png)

4. Ponle el nombre `RegistrarVacacionesFlow`. Copilot Studio creará y abrirá automáticamente un flujo de Power Automate ya vinculado al agente, con el trigger correcto preconfigurado — no necesitas buscarlo tú.
5. Dentro del editor de Power Automate, agrega 5 parámetros de entrada al trigger dando clic en **Add an input**: 4 de tipo texto (`NombreEmpleado`, `CorreoEmpleado`, `FechaInicio`, `FechaFin`) y 1 de tipo número (`DiasSolicitados`).

![Imagen 037](../images/imagen037.png)

6. Agrega la acción **SharePoint → Crear elemento**, apuntando a tu lista `SolicitudesVacacionesTechNova`, mapeando cada campo de entrada a su columna correspondiente y `Estado = Pendiente`.

![Imagen 038](../images/imagen038.png)

7. Agrega una **Condición**: `DiasSolicitados` **es mayor que** `10`.

![Imagen 039](../images/imagen039.png)

8. **Rama "Sí" (requiere aprobación):**
   - Agrega **Aprobaciones → Iniciar y esperar una aprobación**, tipo *Aprobar/Rechazar - Primer respondedor*, asignado al correo del supervisor que definiste en la Preparación Previa. En el detalle, incluye nombre del empleado, fechas y días solicitados.

   ![Imagen 040](../images/imagen040.png)

   - Agrega una **Condición** sobre el resultado (`Outcome` = `Approve`):

   ![Imagen 041](../images/imagen041.png)

     - Si aprobada: **Actualizar elemento** (Estado = `Aprobada`) + **Enviar correo** al empleado confirmando.

     ![Imagen 042](../images/imagen042.png)
     ![Imagen 043](../images/imagen043.png)

     - Si rechazada: **Actualizar elemento** (Estado = `Rechazada`) + **Enviar correo** al empleado explicando que fue rechazada.

     ![Imagen 044](../images/imagen044.png)
     ![Imagen 045](../images/imagen045.png)

9. **Rama "No" (10 días o menos, aprobación automática):**
   - **Actualizar elemento** (Estado = `Aprobada`) + **Enviar correo** de confirmación inmediata.
10. Guarda el flujo. Al ser creado desde Copilot Studio, la respuesta de salida hacia el agente ya viene preconfigurada — revisa que cada rama termine devolviendo un resumen de texto útil (edítalo si el valor por defecto es demasiado genérico).
11. Regresa a Copilot Studio: el tool `RegistrarVacacionesFlow` ya debería aparecer listado en la pestaña **Tools** sin pasos adicionales.

**Resultado esperado:** El flujo tiene la estructura Trigger (ya vinculado por Copilot Studio) → Crear elemento → Condición (>5 días) → dos ramas, cada una terminando en actualización + correo + respuesta al agente. El tool aparece automáticamente en la pestaña Tools de Nova Assistant.

**Verificación:** El flujo se guarda sin errores de validación, ambas ramas devuelven una salida al agente, y `RegistrarVacacionesFlow` es visible en Tools sin haber tenido que agregarlo por separado.

---

### Paso 2: Crear el flujo `ConsultarEstadoVacacionesFlow` desde Copilot Studio

**Objetivo:** Permitir que el agente consulte el estado real de una solicitud ya registrada.

**Instrucciones:**

1. En Nova Assistant, ve otra vez a **Tools → Add tool → Add new → Workflows**.
2. Nómbralo `ConsultarEstadoVacacionesFlow`. Copilot Studio vuelve a crear y vincular el flujo automáticamente.
3. Dentro de Power Automate, agrega un parámetro de entrada de texto: `NombreEmpleado`.

![Imagen 046](../images/imagen046.png)

4. Agrega **SharePoint → Obtener elementos**, con filtro `Title eq '@{parámetro NombreEmpleado}'`, máximo 1 resultado.

![Imagen 047](../images/imagen047.png)

5. Configura la respuesta de salida hacia el agente combinando `Estado`, `FechaInicio`, `FechaFin` y `DiasSolicitados` del resultado.

![Imagen 048](../images/imagen048.png)

Usa el siguiente resultado como fx y pega: 
```
concat(
'Estado: ', outputs('Get_items')?['body/value'][0]?['Estado']?['Value'],
'\nFecha Inicio: ', outputs('Get_items')?['body/value'][0]?['FechaInicio'],
'\nFecha Fin: ', outputs('Get_items')?['body/value'][0]?['FechaFin'],
'\nDías Solicitados: ', string(outputs('Get_items')?['body/value'][0]?['DiasSolicitados'])
)
```

6. Guarda el flujo. Verifica en Copilot Studio que `ConsultarEstadoVacacionesFlow` ya aparece en Tools.

**Resultado esperado:** El flujo devuelve el estado de la solicitud más reciente de un empleado dado su nombre, y el tool queda vinculado automáticamente.


**Verificación:** Ejecuta una prueba manual en Power Automate con un nombre que ya tenga un registro (puedes crear uno de prueba directamente en SharePoint) y confirma que la salida trae los datos correctos.

![Imagen 049](../images/imagen049.png)

---

### Paso 3: Revisar las descripciones de ambas herramientas

**Objetivo:** Asegurar que Nova Assistant sepa, solo con leer la descripción de cada tool, cuándo debe usarla.

**Instrucciones:**

1. En la pestaña **Tools** de Nova Assistant, abre `RegistrarVacacionesFlow` y revisa la descripción generada automáticamente. Si es genérica, edítala para que diga algo como: *"Registra una solicitud de vacaciones de un empleado. Úsala cuando el usuario quiera solicitar vacaciones y ya tengas su nombre, correo, fechas y número de días."*
2. Repite para `ConsultarEstadoVacacionesFlow`: *"Consulta el estado actual de una solicitud de vacaciones ya registrada, dado el nombre del empleado. Úsala cuando el usuario pregunte si su solicitud fue aprobada."*

![Imagen 050](../images/imagen050.png)

**Resultado esperado:** Ambos tools tienen descripciones específicas, no las genéricas que Copilot Studio propone por defecto.

**Verificación:** Los dos tools muestran sus parámetros de entrada correctamente detectados desde el flujo, con una descripción clara de cuándo usarlos.

---

### Paso 4: Actualizar las instrucciones de Nova Assistant

**Objetivo:** Que el agente sepa cuándo debe usar estas nuevas herramientas.

**Instrucciones:**

1. Ve a **Overview → Instructions**.
2. En la sección `[OBJETIVOS]`, agrega:
   ```
   4. Registrar solicitudes de vacaciones cuando el usuario lo pida, recopilando nombre,
      correo, fechas y número de días antes de usar la herramienta correspondiente.
   5. Consultar el estado de una solicitud de vacaciones ya registrada cuando el usuario
      lo pregunte.
   ```

![Imagen 051](../images/imagen051.png)

3. Guarda las instrucciones.

**Resultado esperado:** El agente ahora sabe, por sus propias instrucciones, en qué momento debe recurrir a las herramientas nuevas — no necesitas construir un flujo de conversación paso a paso: la orquestación generativa le pide al usuario los datos que falten automáticamente.

**Verificación:** Al reabrir el agente, las instrucciones muestran los dos objetivos nuevos.

---

### Paso 5: Probar los tres escenarios

**Objetivo:** Validar el ciclo completo con los dos caminos posibles (aprobación automática y aprobación humana).

**Instrucciones:**

Abre el panel **Test your agent** y ejecuta:

**Escenario A — Pocos días (aprobación automática):**
```
Quiero registrar vacaciones. Soy [tu nombre], mi correo es [correo], del 1 al 5 de diciembre, son 5 días.
```
El agente debe invocar `RegistrarVacacionesFlow`, y el registro debe quedar en **Aprobada** de inmediato (sin pausa).

**Escenario B — Muchos días (requiere aprobación humana):**
```
Quiero registrar vacaciones. Soy [otro nombre], mi correo es [correo], del 10 al 25 de diciembre, son 15 días.
```
El agente debe invocar el flujo, que esta vez **pausa** esperando la aprobación del supervisor. Ve a tu correo de supervisor, aprueba o rechaza la solicitud, y confirma que el estado en SharePoint se actualiza según tu decisión.

**Escenario C — Consultar estado:**
```
¿Ya se aprobó mi solicitud de vacaciones? Soy [nombre usado en A o B].
```
El agente debe invocar `ConsultarEstadoVacacionesFlow` y responder con el estado real.

**Resultado esperado:** Los 3 escenarios se comportan según lo descrito.

**Verificación:** Revisa la lista `SolicitudesVacacionesTechNova` en SharePoint — deben existir los registros de A y B con el `Estado` correcto.

---

## 7. Validación y Pruebas

| # | Criterio de validación | Cumple (✓/✗) |
|---|------------------------|:---:|
| 1 | La lista de SharePoint existe con las 6 columnas requeridas | |
| 2 | `RegistrarVacacionesFlow` tiene la bifurcación >10 días correctamente configurada | |
| 3 | `ConsultarEstadoVacacionesFlow` devuelve datos reales de SharePoint | |
| 4 | Ambos flujos están agregados como Tools de Nova Assistant con descripciones claras | |
| 5 | Las instrucciones del agente mencionan explícitamente ambas capacidades nuevas | |
| 6 | Escenario A (≤10 días) se aprueba automáticamente | |
| 7 | Escenario B (>10 días) pausa y espera aprobación humana | |
| 8 | Escenario C devuelve el estado correcto de una solicitud existente | |

---

## 8. Solución de Problemas

### Problema 1: El trigger "When Copilot calls a flow" no aparece al crear un flujo desde Power Automate

**Síntomas:** Al intentar crear un Automated Cloud Flow directamente desde Power Automate y buscar ese trigger, no aparece en la lista.

**Causa:** En la experiencia moderna de Copilot Studio, Microsoft ya no expone ese trigger de forma confiable para crearlo manualmente desde Power Automate.

**Solución:** No lo busques desde Power Automate. Créalo desde dentro de Copilot Studio: **Tools → Add tool → Add new → Workflows**. Esto crea y vincula automáticamente un flujo compatible con el agente, sin necesidad de configurar el trigger a mano (así están redactados los Pasos 1 y 2 de este laboratorio).

### Problema 2: El agente no invoca la herramienta y responde de forma genérica

**Solución:** La descripción del Tool probablemente es demasiado vaga. Edítala para que sea explícita sobre cuándo usarla (ver ejemplos del Paso 3), y confirma que las instrucciones del agente (Paso 4) mencionan el objetivo relacionado.

### Problema 3: La acción de aprobación falla con "No Approvals connection found"

**Solución:** Ve a **Datos → Conexiones** en Power Automate, crea una nueva conexión al conector **Approvals**, autentícate, y vuelve a seleccionarla en el paso de aprobación del flujo.

### Problema 4: La creación del elemento en SharePoint falla con error 403

**Solución:** Verifica que tu cuenta tiene al menos permisos de **Colaborar** o **Editar** sobre el sitio donde vive la lista `SolicitudesVacacionesTechNova`.

### Problema 5: El flujo de aprobación nunca llega al supervisor

**Solución:** Revisa que el correo en el campo "Asignado a" no tenga espacios ni esté mal escrito, y que esa cuenta tenga licencia de Power Automate.

---

## 9. Limpieza

- No elimines `RegistrarVacacionesFlow` ni `ConsultarEstadoVacacionesFlow` — son la base para módulos posteriores si el curso los amplía.
- Conserva los registros de prueba en SharePoint (sirven como evidencia y como datos para el Escenario C en sesiones futuras).
- Si no quieres seguir recibiendo correos de aprobación de prueba, puedes desactivar temporalmente `RegistrarVacacionesFlow` desde Power Automate.

---

## 10. Resumen

| Componente creado | Concepto del Módulo 4 que representa |
|---|---|
| `RegistrarVacacionesFlow` con condición >10 días | Herramienta/acción + automatización de tareas |
| Rama de aprobación (Approvals) | Patrón *human-in-the-loop* |
| `ConsultarEstadoVacacionesFlow` | El agente cierra el ciclo consultando el resultado de su propia acción |
| Tools en Nova Assistant | Cómo un agente conversacional se convierte en un agente que actúa |

### Arquitectura del patrón

```
Usuario → Nova Assistant (Copilot Studio) → Tool (Workflow)
        → Power Automate Flow → SharePoint / Outlook (Approvals)
        → Respuesta al agente → Usuario
```

Nota: ambos flujos se crean **desde Copilot Studio** (Tools → Add tool → Workflows), no desde Power Automate directamente — es la forma vigente de vincularlos correctamente al agente.

### Recursos adicionales

- [Aprobaciones en Power Automate](https://learn.microsoft.com/es-es/power-automate/get-started-approvals)
- [Herramientas (Tools) en Copilot Studio](https://learn.microsoft.com/es-es/microsoft-copilot-studio/authoring-tools-overview)
- [Patrón ReAct: Synergizing Reasoning and Acting (Yao et al., 2022)](https://arxiv.org/abs/2210.03629)

