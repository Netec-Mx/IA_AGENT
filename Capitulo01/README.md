# Comparación de Modelos de IA en Poe y Análisis de Comportamientos

## 1. Metadatos

| Campo | Valor |
|-------|-------|
| **Duración** | 30 minutos |
| **Complejidad** | Fácil |
| **Nivel Bloom** | Aplicar |
| **Módulo** | 1 – Fundamentos de Agentes de IA |
| **Lección asociada** | 1.1 – Diferencia entre Chatbot, Asistente y Agente Inteligente / 1.3 – Contexto, Memoria, Herramientas, Razonamiento y Autonomía |

---

## 2. Descripción General

En este laboratorio explorarás cuatro modelos/bots de IA disponibles en la plataforma **Poe** —un modelo tipo GPT, un modelo Claude, un modelo Gemini y un bot con acceso a búsqueda web— ejecutando un conjunto estandarizado de cinco tareas de prueba en cada uno. Observarás y documentarás las diferencias de comportamiento en cuanto a contexto, memoria, herramientas, razonamiento y autonomía. Los hallazgos se registrarán en la plantilla de bitácora **`Bitacora-Lab-01-Poe.xlsx`**, generando un artefacto de referencia que utilizarás en los laboratorios del Módulo 2.

Poe no requiere licenciamiento adicional por participante: basta una cuenta gratuita para acceder a múltiples modelos de IA desde una sola interfaz.

> ⚠️ **Presupuesto de créditos:** este laboratorio usa la capa gratuita de Poe (300 puntos de cómputo por participante). Por eso las 4 tareas se ejecutan con las **variantes económicas** de cada modelo (Nano/Mini, Haiku, Flash) en lugar de las versiones insignia (Opus, Pro, Astra), que consumen muchos más puntos por mensaje. El Paso 1 incluye una verificación rápida del costo en puntos antes de empezar.

---

## 3. Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Identificar y diferenciar el comportamiento funcional de al menos tres modelos de IA distintos disponibles en Poe.
- [ ] Clasificar cada modelo/bot explorado según la taxonomía de tipos de agentes (reactivo, asistente, autónomo) con base en evidencia observada.
- [ ] Documentar en la bitácora las diferencias clave de comportamiento utilizando los cinco atributos: contexto, memoria, herramientas, razonamiento y autonomía.
- [ ] Relacionar los casos de uso observados con escenarios empresariales reales relevantes para tu contexto profesional.

---

## 4. Prerrequisitos

### Conocimientos previos

| Concepto | Descripción |
|----------|-------------|
| Diferencia Chatbot / Asistente / Agente | Lectura completada de la Lección 1.1 (temas 1.1 a 1.5 del Módulo 1) |
| Navegación básica en plataformas web | Saber crear una cuenta y navegar en un sitio web |

### Accesos requeridos

| Recurso | Detalle |
|---------|---------|
| Cuenta Poe | Cuenta gratuita en [poe.com](https://poe.com), registrada con correo electrónico o cuenta de Google |
| Navegador | Google Chrome 124+ o Microsoft Edge 124+ |
| Plantilla de bitácora | Archivo [**Bitácora Lab 01 - Poe.xlsx**](./Bitacora-Lab-01-Poe.xlsx) proporcionado por el instructor |

---

## 5. Entorno de Laboratorio

### Hardware mínimo

| Componente | Requisito |
|------------|-----------|
| Procesador | 64 bits – Intel Core i5 8ª gen. o AMD Ryzen 5 3000+ |
| RAM | 8 GB mínimo |
| Conexión a internet | 10 Mbps mínimo estable |

### Software requerido

| Aplicación | Versión | Propósito |
|------------|---------|-----------|
| Poe (Web App) | Versión actual | Acceso a múltiples modelos de IA desde una sola interfaz |
| Google Chrome / Edge | 124.x | Acceso al servicio web |
| Microsoft Excel / Google Sheets | Cualquier versión reciente | Abrir y completar la plantilla [**Bitácora Lab 01 - Poe.xlsx**](./Bitacora-Lab-01-Poe.xlsx) |

### Preparación inicial del entorno

1. Verifica que puedes acceder a [https://poe.com](https://poe.com) e iniciar sesión con tu cuenta.

![Imagen 001](../images/imagen001.png)
2. En el buscador de bots de Poe, localiza y guarda como favoritos (ícono de estrella) los siguientes cuatro bots:


   - Un modelo **GPT económico** (por ejemplo, `GPT-5.4-Nano` o la variante "Nano"/"Mini" más reciente de OpenAI disponible en Poe).

   - Un modelo **Claude económico** (por ejemplo, `Claude-Haiku-4.5` o la variante "Haiku" más reciente de Anthropic disponible en Poe).

   - Un modelo **Gemini económico** (por ejemplo, `Gemini-2.5-Flash-Lite` o la variante "Flash" más reciente de Google disponible en Poe — evita las variantes "Pro").

   - Un bot con **búsqueda web habilitada de bajo costo** (por ejemplo, `Assistant`, el bot general de Poe que enruta a modelos económicos y puede buscar información en tiempo real; evita bots de búsqueda "premium" que cobran más puntos por mensaje).

   > ⚠️ **Cuidado al elegir el modelo:** antes de guardar cada bot como favorito, toca el ícono de puntos (⚡) junto a su nombre y revisa la tabla **"Tarifas"** que se despliega. Ahí verás el costo en puntos por cada 1,000 tokens de Entrada y de Salida (texto) — elige siempre la variante con el costo más bajo en ambas columnas (Nano, Mini, Haiku y Flash suelen ser las más económicas de cada proveedor). Si el bot muestra también una tarifa de "Salida (búsqueda)", ten en cuenta que ese tipo de respuesta cuesta muchos más puntos por uso, así que solo debe activarse cuando la tarea realmente lo requiera (Tareas T2 y T4).

![Imagen 004](../images/imagen004.png)
3. Abre el archivo `Bitacora-Lab-01-Poe.xlsx` y guarda una copia personal para este laboratorio.

---

## 6. Instrucciones Paso a Paso

### Paso 1: Preparar la bitácora de documentación

**Objetivo:** Configurar tu copia de la plantilla `Bitacora-Lab-01-Poe.xlsx` donde registrarás todas las observaciones del laboratorio.

**Instrucciones:**

1. Abre tu copia personal de `Bitacora-Lab-01-Poe.xlsx`.
2. Verifica que el archivo contiene las siguientes pestañas ya preparadas:
   - **Encabezado** (datos del participante)
   - **Tabla de Tareas** (5 filas con las tareas estandarizadas)
   - **Tabla Comparativa** (4 columnas: GPT, Claude, Gemini, Bot con búsqueda web)
   - **Notas** (escenarios empresariales y observaciones libres)
3. En la pestaña **Encabezado**, completa las celdas amarillas:
   - **Nombre del participante:** [Tu nombre completo]
   - **Fecha:** [Fecha actual]
   - **Hora de inicio:** [Hora actual]
4. En la pestaña **Tabla de Tareas**, revisa las **cinco tareas de prueba estandarizadas** que ya están cargadas y que ejecutarás en cada modelo, así como la nota sobre cómo elegir el modelo económico correcto de cada bot:

| # | Tarea | Categoría |
|---|-------|-----------|
| T1 | "Redacta un correo profesional para solicitar una reunión con el equipo de ventas para discutir los resultados del Q1" | Generación de contenido |
| T2 | "¿Qué pasó en las noticias más relevantes de esta semana?" | Recuperación de información actual |
| T3 | "Dado que nuestro presupuesto se redujo un 15% y tenemos 3 proyectos pendientes, ¿cuál debería priorizar?" | Razonamiento sobre contexto |
| T4 | "Necesito ayuda con lo del proyecto" (solicitud deliberadamente ambigua) | Manejo de ambigüedad |


**Resultado esperado:** Tu copia de `Bitacora-Lab-01-Poe.xlsx` está abierta, personalizada con tus datos en la pestaña Encabezado y lista para recibir las observaciones de cada interacción.

**Verificación:** Confirma que puedes editar una celda amarilla de la pestaña **Tabla Comparativa** sin problema.

---

### Paso 2: Explorar un modelo tipo GPT en Poe

**Objetivo:** Ejecutar las cinco tareas de prueba en un bot GPT económico de Poe y registrar el comportamiento observado.

**Instrucciones:**

1. En Poe, abre el bot GPT económico que guardaste como favorito (por ejemplo, `GPT-5.4-Nano`).
2. Inicia una **conversación nueva** (ícono de "+" o "New chat").
3. Ejecuta la **Tarea T1** — escribe:
   ```
   Redacta un correo profesional para solicitar una reunión con el equipo de ventas para discutir los resultados del Q1
   ```

![Imagen 007](../images/imagen007.png)

4. Observa y registra en tu bitácora:
   - ¿Qué tan elaborada fue la respuesta?
   - ¿Ofreció opciones o variantes?
5. Ejecuta la **Tarea T2** — escribe:
   ```
   ¿Qué pasó en las noticias más relevantes de esta semana?
   ```
6. Observa: ¿El modelo indica que no tiene acceso a información actualizada o en tiempo real? Registra la respuesta textual (probablemente mencionará su fecha límite de conocimiento).

![Imagen 008](../images/imagen008.png)

7. Ejecuta la **Tarea T3** — escribe:
   ```
   Dado que nuestro presupuesto se redujo un 15% y tenemos 3 proyectos pendientes, ¿cuál debería priorizar?
   ```

![Imagen 009](../images/imagen009.png)

8. Observa: ¿Pide más contexto? ¿Razona con la información limitada? ¿Genera un análisis estructurado?

9. Ejecuta la **Tarea T4** — escribe:
   ```
   Necesito ayuda con lo del proyecto
   ```
10. Observa: ¿Cómo maneja la ambigüedad? ¿Pide clarificación o asume un contexto?

![Imagen 010](../images/imagen010.png)


11. En la pestaña **Tabla Comparativa** de tu bitácora, completa la columna **"GPT"** con tus observaciones para cada atributo.

**Resultado esperado:** Has identificado que el modelo GPT se especializa en generación de contenido y razonamiento con lenguaje natural, pero tiene contexto limitado a su fecha de entrenamiento y no accede a información en tiempo real ni ejecuta acciones externas.

**Verificación:** Tu columna "GPT" en la pestaña Tabla Comparativa tiene al menos una observación por cada uno de los 5 atributos.

---

### Paso 3: Explorar un modelo Claude en Poe

**Objetivo:** Ejecutar las cinco tareas de prueba en un bot Claude económico de Poe y registrar las diferencias de comportamiento respecto al modelo GPT.

**Instrucciones:**

1. En Poe, abre el bot Claude económico que guardaste como favorito (por ejemplo, `Claude-Haiku-4.5`).
2. Inicia una **conversación nueva**.
3. Repite las **Tareas T1 a T4** exactamente con el mismo texto usado en el Paso 2.
![Imagen 012](../images/imagen012.png)

4. Para cada tarea, observa y registra:
   - Diferencias en el tono, extensión y estructura de la respuesta frente a GPT.
   - Diferencias en cómo maneja la ambigüedad (T4) y el contexto limitado (T3).
   - Si menciona explícitamente no tener acceso a datos en tiempo real (T2).
5. En la pestaña **Tabla Comparativa** de tu bitácora, completa la columna **"Claude"**.

**Resultado esperado:** Has identificado que, aunque el modelo Claude comparte limitaciones similares a GPT en cuanto a acceso a información en tiempo real, puede diferir en estilo de razonamiento, nivel de detalle o forma de solicitar clarificación.

**Verificación:** Compara mentalmente las respuestas de Claude vs. GPT para la Tarea T4. Registra explícitamente al menos una diferencia observada en la pestaña Notas.

---

### Paso 4: Explorar un modelo Gemini en Poe

**Objetivo:** Ejecutar las cinco tareas de prueba en un bot Gemini económico de Poe y observar sus particularidades frente a los modelos anteriores.

**Instrucciones:**

1. En Poe, abre el bot Gemini económico que guardaste como favorito (por ejemplo, `Gemini-2.5-Flash-Lite`).
2. Inicia una **conversación nueva**.
3. Repite las **Tareas T1 a T4** exactamente con el mismo texto usado en los pasos anteriores.

![Imagen 013](../images/imagen013.png)

4. Para cada tarea, observa y registra:
   - Calidad y formato de la respuesta (por ejemplo, uso de listas, tablas o encabezados).
   - Cómo comunica sus limitaciones en la Tarea T2 .
   - Diferencias notables en el razonamiento de la Tarea T3.
5. En la pestaña **Tabla Comparativa** de tu bitácora, completa la columna **"Gemini"**.

**Resultado esperado:** Has identificado que los tres modelos conversacionales (GPT, Claude, Gemini) comparten un patrón: buena generación de contenido y razonamiento, pero ninguno puede acceder a información en tiempo real ni ejecutar acciones por sí mismo.

**Verificación:** Anota en la pestaña Notas si notaste alguna diferencia relevante en la Tarea T3 (razonamiento) entre los tres modelos.

---

### Paso 5: Explorar un bot con búsqueda web habilitada

**Objetivo:** Ejecutar las mismas cinco tareas en un bot de Poe con acceso a búsqueda web (herramienta externa) y comparar su comportamiento frente a los modelos puramente conversacionales.

**Instrucciones:**

1. En Poe, abre el bot con búsqueda web económico que guardaste como favorito (por ejemplo, `Assistant`).
2. Inicia una **conversación nueva**.
3. Ejecuta la **Tarea T1** y observa si el comportamiento es similar al de los modelos anteriores.
4. Ejecuta la **Tarea T2** — observa: ¿Ahora sí puede mencionar noticias recientes reales? Este es un punto clave de diferenciación.
5. Ejecuta la **Tarea T3** y observa si busca información adicional en la web para enriquecer su razonamiento.
6. Ejecuta la **Tarea T4** y observa cómo maneja la ambigüedad.
7. En la pestaña **Tabla Comparativa** de tu bitácora, completa la columna **"Bot con búsqueda web"**.

**Resultado esperado:** Has identificado que un bot con acceso a una herramienta externa (búsqueda web) puede superar la limitación de "conocimiento congelado" de los modelos puramente conversacionales, acercándose más a un comportamiento de agente al consultar información fuera de sí mismo antes de responder.

**Verificación:** La diferencia más notable debería estar en T2. Confirma que documentaste con qué fuente o forma respondió el bot (si citó un sitio web, por ejemplo).

---

### Paso 6: Completar la tabla comparativa y clasificación

**Objetivo:** Sintetizar las observaciones en la pestaña Tabla Comparativa y clasificar cada modelo/bot según la taxonomía de la Lección 1.1.

**Instrucciones:**

1. Regresa a la pestaña **Tabla Comparativa** de tu bitácora.
2. Confirma que completaste la tabla de 5 atributos × 4 modelos:

| Atributo | GPT | Claude | Gemini | Bot con búsqueda web |
|----------|-----|--------|--------|------------------------|
| **Contexto** | [Alcance del contexto disponible] | | | |
| **Memoria** | [¿Recuerda entre interacciones dentro del chat?] | | | |
| **Herramientas** | [¿Qué herramientas puede usar?] | | | |
| **Razonamiento** | [Calidad del razonamiento observado] | | | |
| **Autonomía** | [Nivel: Nula/Baja/Media/Alta] | | | |

3. En la misma pestaña, debajo de la tabla, encontrarás la sección **"Clasificación según Taxonomía"**. Clasifica cada modelo/bot:
   - **Reactivo:** Opera solo cuando se le solicita, sin memoria ni planificación.
   - **Asistente:** Comprende lenguaje natural, mantiene contexto conversacional, genera contenido pero no ejecuta acciones autónomas.
   - **Autónomo:** Planifica, usa herramientas y ejecuta acciones con mínima supervisión.

4. Para cada modelo, escribe en la celda correspondiente una justificación de 2-3 oraciones explicando por qué lo clasificaste de esa manera. Ejemplo:

   > **GPT — Clasificación: Asistente**
   > Comprende lenguaje natural y genera contenido de alta calidad. Su contexto está limitado a la conversación activa y a su fecha de entrenamiento. No ejecuta acciones externas ni accede a herramientas, por lo que su autonomía es baja.

5. En la pestaña **Notas**, redacta un párrafo de 3-5 oraciones por cada tipo (Reactivo / Asistente / Autónomo) identificando al menos un escenario empresarial real de tu contexto profesional donde ese tipo de modelo/bot sería la opción más adecuada.

6. Regresa a la pestaña **Encabezado** y registra la **hora de finalización**.

**Resultado esperado:** Tu archivo `Bitacora-Lab-01-Poe.xlsx` contiene:
- Pestaña Tabla Comparativa completa con los 5 atributos × 4 modelos (20 celdas completadas) y la clasificación taxonómica justificada para cada modelo.
- Pestaña Notas con los escenarios de aplicación empresarial.

**Verificación:** Revisa que ninguna celda amarilla del archivo esté vacía. Cada clasificación debe tener una justificación basada en evidencia observada (no en suposiciones teóricas).

---

## 7. Validación y Pruebas

Para considerar este laboratorio completado exitosamente, verifica los siguientes criterios:

| # | Criterio de validación | Cumple (✓/✗) |
|---|------------------------|:---:|
| 1 | Se ejecutaron las 4 tareas de prueba en el modelo GPT y se registraron observaciones | |
| 2 | Se ejecutaron las 4 tareas de prueba en el modelo Claude y se registraron observaciones | |
| 3 | Se ejecutaron las 4 tareas de prueba en el modelo Gemini y se registraron observaciones | |
| 4 | Se ejecutaron las 4 tareas de prueba en el bot con búsqueda web y se registraron observaciones | |
| 5 | La pestaña Tabla Comparativa tiene las 20 celdas (5 atributos × 4 modelos) completadas | |
| 6 | Cada modelo tiene una clasificación taxonómica con justificación de 2-3 oraciones | |
| 7 | La pestaña Notas identifica al menos un escenario empresarial real para cada tipo de modelo/bot | |

**Resultado esperado de clasificación típica:**

| Modelo/Bot | Clasificación esperada |
|--------|----------------------|
| GPT | Asistente (potente en generación y razonamiento, sin acceso a herramientas externas) |
| Claude | Asistente (potente en generación y razonamiento, sin acceso a herramientas externas) |
| Gemini | Asistente (potente en generación y razonamiento, sin acceso a herramientas externas) |
| Bot con búsqueda web | Asistente con rasgos de agente (usa una herramienta externa para obtener información actualizada) |

> **Nota:** Las clasificaciones pueden variar según el modelo exacto disponible en Poe al momento de ejecutar el laboratorio. Lo importante es que la justificación sea coherente con el comportamiento observado.

---

## 8. Solución de Problemas

### Problema 1: No encuentro alguno de los bots recomendados en Poe

**Síntomas:** Al buscar el nombre del bot GPT, Claude, Gemini o el bot con búsqueda web en el buscador de Poe, no aparece o el nombre exacto ha cambiado.

**Causa:** Poe actualiza periódicamente los nombres y versiones de los modelos disponibles en su catálogo.

**Solución:**
1. Usa el buscador de Poe y escribe el nombre genérico del proveedor (por ejemplo, "GPT", "Claude" o "Gemini") para ver todas las variantes disponibles.
2. Elige la versión más reciente que aparezca marcada como estable o recomendada.
3. Para el bot con búsqueda web, busca "web search" o revisa la descripción de los bots destacados: debe indicar explícitamente que tiene acceso a internet en tiempo real.
4. Si tienes dudas sobre qué bot usar, consulta con el instructor antes de continuar.

---

### Problema 2: Alcancé el límite de mensajes gratuitos en Poe

**Síntomas:** Al enviar un mensaje, Poe indica que se alcanzó el límite diario o mensual de mensajes para la cuenta gratuita en ese modelo.

**Causa:** Las cuentas gratuitas de Poe tienen un límite de puntos/mensajes que se consumen según el modelo utilizado.

**Solución:**
1. Espera al restablecimiento del límite (generalmente diario) o cambia temporalmente a otro modelo equivalente disponible.
2. Reduce el número de tareas repetidas: si ya obtuviste una respuesta clara para una tarea, no la repitas innecesariamente.
3. Si el problema persiste durante la sesión de laboratorio, consulta con el instructor sobre credenciales alternativas.

---

### Problema 3: Me quedé sin puntos a la mitad del laboratorio

**Síntomas:** Poe muestra un mensaje indicando que ya no tienes puntos suficientes para enviar otro mensaje, antes de terminar las 20 interacciones (5 tareas × 4 modelos).

**Causa:** Se eligió por error una variante más cara del modelo (revisa que el nombre del bot corresponda a Nano/Mini/Haiku/Flash y no a la versión insignia), se activó una búsqueda web en una tarea que no la necesitaba, o se repitieron tareas innecesariamente.

**Solución:**
1. Revisa en tu bitácora cuántas interacciones ya completaste y con qué modelos — no repitas tareas ya registradas.
2. Verifica que el bot que estás usando sea realmente la variante económica: toca el ícono de puntos (⚡) y compara su tabla de Tarifas con la de los demás.
3. Espera al restablecimiento diario de tus puntos gratuitos (ver Problema 2) para completar los modelos faltantes.
4. Si el laboratorio es en sesión de grupo y el tiempo apremia, completa la Tabla Comparativa con los modelos que sí alcanzaste a probar y anota en la pestaña Notas cuáles quedaron pendientes; podrás completarlos después con tus puntos del día siguiente.

---

### Problema 4: Excel muestra las celdas de la plantilla bloqueadas o el formato se rompe

**Síntomas:** Al intentar escribir en una celda de `Bitacora-Lab-01-Poe.xlsx`, no se puede editar, o al copiar/pegar texto se pierde el color de fondo amarillo de las celdas de captura.

**Causa:** Algunas celdas de la plantilla tienen combinación de celdas (merge) que puede alterarse al pegar contenido con formato desde otra fuente.

**Solución:**
1. Escribe directamente sobre la celda amarilla en lugar de copiar y pegar texto con formato desde otro documento (usa "Pegar solo valores" si necesitas copiar texto).
2. Si el formato se pierde, no te preocupes por restaurarlo: lo importante es que el contenido esté completo. El instructor puede reemplazar el formato al recopilar las bitácoras.
3. Si el archivo se abre en modo de solo lectura, verifica que estás trabajando sobre tu copia personal y no sobre el archivo original compartido por el instructor.

---

## 9. Limpieza

Este laboratorio no genera recursos que requieran eliminación significativa. Realiza las siguientes acciones de orden:

1. **Conversaciones en Poe:** Puedes renombrar cada conversación con el nombre del modelo utilizado (por ejemplo, "Lab 01 - GPT") para fácil referencia futura, o eliminarlas si no las necesitas.
2. **Bitácora:** No elimines tu archivo `Bitacora-Lab-01-Poe.xlsx` — será referencia para los laboratorios del Módulo 2.

---

## 10. Resumen

### Lo que aprendiste

En este laboratorio aplicaste los conceptos teóricos de la Lección 1.1 interactuando directamente con cuatro modelos/bots de IA en Poe. Comprobaste de primera mano que:

- **El contexto disponible** de un modelo conversacional está limitado a la conversación activa y a su fecha de entrenamiento, salvo que se le proporcione una herramienta externa.
- **La capacidad de acción** (uso de herramientas) es lo que más diferencia a un asistente de un agente: generar texto no es lo mismo que consultar información real y actualizada.
- **El manejo de ambigüedad** revela la sofisticación del sistema: los mejores piden clarificación contextualizada en lugar de asumir o fallar.
- **La autonomía** en los modelos conversacionales básicos es todavía limitada; un bot con herramientas (como búsqueda web) empieza a mostrar rasgos de agente al incorporar información externa a su respuesta.

### Conexión con los próximos laboratorios

Los hallazgos documentados en tu tabla comparativa servirán como referencia cuando, en los próximos laboratorios de Poe, construyas tus propios prompts/bots aplicando conceptos de rol, objetivos, restricciones, contexto persistente, consistencia de respuesta y manejo de ambigüedad. Podrás definir conscientemente qué nivel de contexto, memoria, herramientas y autonomía quieres otorgarle a tu propio bot, basándote en lo que observaste que funciona (y lo que no) en los modelos preconstruidos.

### Recursos adicionales

- [Poe — Sitio oficial](https://poe.com)
- [Russell & Norvig — Capítulo de Agentes Inteligentes (referencia académica)](https://aima.cs.berkeley.edu/)
