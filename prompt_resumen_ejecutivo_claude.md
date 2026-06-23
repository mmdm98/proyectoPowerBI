# Prompt para Claude: Actualización de Página "Resumen Ejecutivo"

<instrucciones>
Lee atentamente las modificaciones que acabo de realizar en el archivo `report.json` (o en el modelo) para la página **Resumen Ejecutivo**. En base a mi progreso, necesito que implementes las siguientes mejoras visuales y funcionales:

## 1. Actualización de Tarjetas del Resumen Ejecutivo (Añadir Porcentajes)
Para todas las tarjetas visuales actuales del Resumen Ejecutivo, necesito que agregues información adicional utilizando **subtítulos** (o "etiquetas de referencia" si estás usando el visual de "Nueva Tarjeta"). 
*   **Requisito**: Cada tarjeta debe mostrar, además de su valor absoluto actual, la medida correspondiente que represente su **porcentaje sobre la base del total** (ej. `% Contactados`, `% Interactuaron con Luz`, etc.).
*   Asegúrate de detallar qué campos o medidas exactas debo arrastrar a la sección de subtítulos/referencias del visual nativo.

## 2. Expansión del Lienzo y Nuevo Gráfico de Sentimiento
*   **Expansión del Lienzo**: Modifica las especificaciones de la página para expandir el tamaño del lienzo (canvas) y así tener suficiente espacio vertical/horizontal para nuevos elementos sin que se vea amontonado.
*   **Nuevo Gráfico de Sentimiento**: Crea un nuevo gráfico dedicado al `% de Sentimiento` (Positivo, Neutral, etc.). 
    *   **Estilo**: Quiero que este nuevo visual sea estructural y visualmente **igual al gráfico de barras apiladas 100%** que diseñaste previamente para el "Desglose de Fricción".
    *   **Interactividad**: Asegúrate de que los colores sean consistentes (ej. tonos verdes/azules para positivo/neutral) y que el tooltip o las etiquetas de datos muestren tanto el volumen absoluto como el porcentaje.
</instrucciones>
