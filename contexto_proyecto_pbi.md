<project_context>
<project_name>Tablero de Control de Luz</project_name>
<description>
Este documento contiene el análisis, arquitectura y documentación del proyecto "Tablero de Control de Luz" (proyectoPBI). Es un desarrollo en Power BI (.pbip) diseñado para analizar la gestión, interacción y efectividad de comunicaciones o llamadas automatizadas con clientes (presumiblemente un bot llamado "Luz").
</description>

<architecture>
El proyecto utiliza el formato de Proyecto de Power BI (.pbip), separando la lógica y la presentación:
1. Tablero de Control de Luz.SemanticModel: Contiene el modelo de datos tabular (TMDL).
2. Tablero de Control de Luz.Report: Contiene la interfaz visual y usa Deneb (visualizaciones personalizadas basadas en Vega/Vega-Lite) y un tema base ("CY26SU02").

Notas importantes sobre el modelo:
- La tabla `input_majo_puro` es la encargada de manejar las relaciones del modelo.
- Las tablas/consultas `input_majo` y `security copy of main` NO se utilizan, por lo que deben ser ignoradas en cualquier análisis.
- Los resultados y métricas de las llamadas se obtienen directamente de la tabla `output`.
</architecture>

<data_sources_and_etl>
El flujo de Power Query (M) integra fuentes locales principales que alimentan las siguientes tablas:
- <source name="input_raw">Contiene la base de suministros original (Suministro, Contrato, Razón Social, Barrio, Dirección, Costo de Instalación, Motivo, Tarifa, Fechas).</source>
- <source name="input_majo_puro">Agrega contexto sobre la responsabilidad de la gestión (ej. "Responsabilidad EPEC"), teléfonos, y detalles adicionales. Es fundamental para las relaciones del modelo.</source>
- <source name="output">Contiene los resultados directos de las interacciones (interacción, sentimiento del cliente, tiempos de habla bot/cliente, interrupciones, confirmación de solución).</source>

La tabla de hechos principal se llama `main`, la cual consolida la información uniéndola a través de claves generadas como `ID_KEY`.
</data_sources_and_etl>

<metrics_and_kpis>
El modelo centraliza sus indicadores en la tabla `01_Medidas`, definiendo el embudo de conversión de la comunicación (basándose principalmente en la tabla `output`):
- Base de Datos: Cantidad total de registros base.
- Contactados: Clientes con los que se logró contacto.
- Interactuaron con Luz: Interacciones donde el cliente participó (Interactores = "Sí").
- Cortaron Comunicación: El usuario cortó (Interactores = "No").
- Solicitaron Conexión: Interactuaron y confirmaron la solución.
- Avisarán al Normalizar: Interactuaron pero indicaron que avisarán posteriormente (no confirmaron solución inmediata).
</metrics_and_kpis>

<time_intelligence>
El modelo incorpora tablas de fechas auto-generadas y una dimensión `DimCalendario` personalizada para analizar métricas cruzando "Fecha de Carga", "Fecha de Ejecución" y la "Fecha y Hora" de la interacción.
</time_intelligence>

<instructions_for_llm>
Al analizar o sugerir código/DAX para este proyecto:
1. Ten en cuenta la estructura tabular mencionada. Utiliza nombres de columnas exactos según esta documentación.
2. Recuerda que la tabla central es `main`, la tabla de medidas es `01_Medidas`, y los indicadores de experiencia provienen de `output`.
3. Ignora por completo cualquier referencia a `input_majo` o `security copy of main`. Asume que `input_majo_puro` es la dimensión relacional correcta.
</instructions_for_llm>
</project_context>
