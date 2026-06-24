# Prompt para Claude: Refinamiento de Resumen Ejecutivo y Nuevos Análisis

<instrucciones>
Por favor, lee la configuración actual de la página **Resumen Ejecutivo** (revisa los últimos cambios en `report.json` o en el modelo), ya que he actualizado las tarjetas y modificado algunos elementos visuales. En base a esto, necesito que implementes las siguientes modificaciones y agregues nuevos visuales:

## 1. Ajustes a Visuales y Filtros Existentes
*   **Filtro de Fechas (Meses en Botones)**: Modifica el comportamiento de los segmentadores de fecha actuales. **Elimina por completo el selector de día**. Necesito que dejes un segmentador exclusivo para el **Mes**, pero configurado visualmente con estilo de **Botones** (Orientación horizontal o Cuadrícula/Mosaico), para que la experiencia de elegir el mes sea directa y táctil.
*   **Gráfico de Fricción**: Transforma el gráfico de barras actual de "Desglose de Fricción". En lugar de mostrar los números absolutos, configúralo para que muestre el **porcentaje (100% apilado)** de cada motivo de fricción sobre el total de cortes.

## 2. Nuevos Gráficos de Evolución y Top
*   **Evolución Mensual (Contactados vs. Interactuaron)**: Crea un nuevo gráfico de barras (columnas agrupadas o apiladas) idéntico en estilo al gráfico de evolución diario/histórico que ya tenemos, pero el eje X debe usar una jerarquía estrictamente **Mensual**. Debe comparar las métricas de `Contactados` e `Interactuaron con Luz`.
*   **Top 5 Impedimentos**: Agrega un gráfico (sugiero barras horizontales) que muestre el Top 5 basado en la columna `Impedimento` de la tabla `output`. Este gráfico debe mostrar la proporción de cada impedimento en **porcentajes** respecto al total.

## 3. Nuevas Tarjetas Históricas (Promedio de Tiempos de Llamada)
Necesito dos nuevas **tarjetas visuales históricas** que ignoren el filtro de fecha de la página (usa `REMOVEFILTERS(DimCalendario)` o equivalente). Deben mostrar el promedio del tiempo de llamada convertido a minutos:
1.  **Promedio Histórico Tiempo Cliente (Minutos)**: Calcula el promedio de la columna `output[Tiempo Habla Cliente Seg]` y divídelo por 60.
2.  **Promedio Histórico Tiempo Luz (Minutos)**: Calcula el promedio de la columna `output[Tiempo Habla Bot Seg]` y divídelo por 60.
*(Por favor, facilítame el código DAX exacto para crear estas dos medidas).*

## 4. Matrices / Tablas de Comparación Temporal
Agrega dos objetos visuales de tipo **Matriz** o **Tabla** diseñados con un estilo limpio y gerencial para hacer seguimiento del desempeño a lo largo del tiempo:
*   **Tabla 1 - Comparación entre Semanas (Week-over-Week)**: 
    *   **Filas**: Semana (o Inicio de Semana, según la dimensión calendario).
    *   **Valores (Métricas)**: `Base de Datos`, `Contactados`, `Solicitaron Conexión` y `% Sentimiento Positivo/Neutral`.
*   **Tabla 2 - Comparación entre Meses (Month-over-Month)**:
    *   **Filas**: Mes (Mes-Año).
    *   **Valores (Métricas)**: `Base de Datos`, `Contactados`, `Solicitaron Conexión` y `% Sentimiento Positivo/Neutral`.

Si necesito crear alguna columna calculada adicional en mi tabla de Calendario para agrupar correctamente por semana, indícamelo en las instrucciones junto con el DAX correspondiente.
</instrucciones>
