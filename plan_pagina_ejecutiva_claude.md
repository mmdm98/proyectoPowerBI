# Prompt / Plan de Ejecución para Claude: Nueva Página Ejecutiva (Sin Deneb)

<context>
Este documento es un plan de acción y un prompt detallado para que construyas una nueva página en el reporte "Tablero de Control de Luz". A diferencia de otros requerimientos, **esta página NO debe utilizar el visual Deneb**. Todo debe construirse utilizando los objetos visuales nativos de Power BI.
</context>

## 1. Definiciones y Aclaraciones Generales
*   **Tarjetas del Resumen Ejecutivo**: Cada vez que se mencione este término, se refiere estrictamente al conjunto de 6 métricas fundamentales: *Base de datos, Contactados, Cortaron comunicación, Interactuaron con Luz, Solicitaron conexión* y *Avisarán al normalizar*.
*   **Filtro de Fecha**: La página debe contar con un segmentador (Slicer) nativo de fecha, configurado para mostrar **Año, Mes y Día**.

---

## 2. Requerimientos de DAX (Medidas Históricas e Inmunes al Filtro)

El usuario requiere que las **Tarjetas del Resumen Ejecutivo** aparezcan dos veces:
1.  **Versión Dinámica**: Responde al filtro de fecha (ya cuentas con las medidas creadas en la tabla `01_Medidas`).
2.  **Versión Histórica (Inmune)**: NO responde al filtro de fecha. 

**Instrucción para Claude:** 
Debes proporcionar el código DAX para crear las versiones "Históricas" de estas 6 medidas. Para ello, envuélvelas en un `CALCULATE` utilizando `REMOVEFILTERS(DimCalendario)` (o la tabla de fechas equivalente en el modelo) para que ignoren cualquier selección del segmentador temporal.

*Ejemplo de lo que debes generar:*
```dax
Base de Datos (Histórico) = CALCULATE([Base de Datos], REMOVEFILTERS(DimCalendario))
```
*(Haz lo mismo para las otras 5 métricas del resumen ejecutivo, y también crea sus respectivas medidas de porcentaje histórico).*

---

## 3. Requerimientos de Diseño Visual (Layout y Creatividad)

Como no usarás Deneb, debes ser **extremadamente creativo** usando los visuales nativos de Power BI. Aprovecha la funcionalidad de la **"Nueva Tarjeta" (New Card visual)** para agregar el porcentaje sobre la base total como "Etiqueta de Referencia" (Reference Label) dentro de la misma tarjeta.

### 3.1. Sección Superior: Filtros y Tarjetas del Resumen Ejecutivo Histórico
*   **Segmentador**: Año / Mes / Día (Estilo menú desplegable o botones horizontales elegantes).
*   **Panel Histórico (Inmune a la fecha)**: Un panel destacado (quizás con un fondo levemente diferente) que contenga las 6 *Tarjetas del Resumen Ejecutivo* en su versión "Histórica". Debe quedar muy claro visualmente que estos números representan el "Total Acumulado Histórico". Agrega subtítulos claros.

### 3.2. Sección Central: Tarjetas del Resumen Ejecutivo (Dinámicas)
*   Agrega las 6 *Tarjetas del Resumen Ejecutivo* estándar (dinámicas). 
*   Para cada tarjeta (tanto aquí como en el histórico), el valor principal debe ser el número absoluto, y debes usar el área de subtítulo o etiqueta de referencia para mostrar el **% sobre la base total**. 

### 3.3. Gráfico de Evolución
*   Debes incorporar (o indicar cómo copiar y pegar) el gráfico de **Evolución de contacto e interacción** que ya existe en la página llamada "grafico". Este gráfico **SÍ** debe filtrarse por la fecha.

### 3.4. KPIs Cualitativos y Fricción (Dinámicos)
Todo este bloque **SÍ** está atado al filtro de fecha:
*   **Indicadores CX**: Crea tarjetas atractivas o medidores (Gauge/Donut) para:
    *   `% de Sentimiento` (Positivo/Neutral)
    *   `% de Interrupciones` (Barge-in)
    *   `% de Carga al 0800`
*   **Desglose de Fricción**: Crea un **Gráfico de Barras Horizontales Apiladas** nativo o un **Gráfico de Cintas / Embudo**, que muestre cómo se desglosa la fuga de información (Segundos iniciales, Antes de completar, Buzón de voz, Otras causas). Usa colores semánticos (ej. rojo oscuro para los segundos iniciales).

---

## 4. Estilo y Entrega
1.  **Títulos y Subtítulos**: Proporciona sugerencias literales de títulos atractivos (Ej. "Rendimiento Histórico vs. Periodo Seleccionado", "Análisis de Fricción en la Llamada").
2.  **Sombras y Bordes**: Indica cómo el usuario debe configurar los bordes redondeados y sombras (UI/UX) para darle un aspecto "premium" con los visuales nativos.
3.  **Entrega**: Proporciónale al usuario las 6+ fórmulas DAX para las medidas históricas, y una guía paso a paso de qué visual nativo arrastrar, qué campos colocar en cada "bucket" (Eje X, Eje Y, Leyenda, Etiquetas de Referencia) y cómo estructurar el lienzo de la página.
