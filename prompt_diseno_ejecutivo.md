# Prompt para Claude: Rediseño Profesional y Estética (UI/UX)

<instrucciones>
Lee atentamente las modificaciones que acabo de implementar en la página **Resumen Ejecutivo** (o en el reporte en general). Ahora necesito que te enfoques exclusivamente en la **apariencia visual (UI/UX)** del tablero. Quiero que modifiques los colores, formatos, tipografías, fondos y la estructura visual para darle un aspecto de Dashboard Ejecutivo Premium.

He tomado como inspiración varias imágenes de referencia con las siguientes características clave que quiero que repliques o adaptes mediante el archivo de tema (Theme JSON) o configuraciones visuales nativas:

## 1. Estructura y Fondo del Lienzo (Canvas)
*   **Contraste de Fondo**: Configura el fondo de la página en un gris muy claro (ej. `#F3F4F6` o similar) para que las tarjetas y visuales, que deben tener fondo **blanco puro (`#FFFFFF`)**, resalten claramente.
*   **Panel de Navegación/Filtros**: Diseña un panel lateral (izquierdo) o una franja superior para alojar el menú y los filtros (como el segmentador de meses en botones). Este panel debe tener un color oscuro contrastante, preferiblemente un **Gris Oscuro/Casi Negro** (ej. `#1F2937`) o un **Morado Profundo** (basado en el estilo "EVA").

## 2. Estilo de las Tarjetas (Cards)
*   **Limpieza Visual**: Las tarjetas del "Resumen Ejecutivo" deben tener fondo blanco, bordes muy sutiles o redondeados (radio de 5px a 8px) y una **sombra ligera** paralela para dar efecto de profundidad (Glassmorphism o Material Design suave).
*   **Jerarquía Tipográfica**: 
    *   **Valor Principal**: Fuente grande, negrita (bold), en color oscuro casi negro.
    *   **Título de la Métrica**: Arriba del valor, en un gris intermedio, tamaño moderado.
    *   **Etiqueta de Referencia (% sobre el total)**: Ubicada debajo, en un tamaño menor. Si es posible, usa color **Verde** (ej. `#22C55E`) para métricas positivas o **Rojo/Naranja** para fricciones, replicando el estilo de comparación (YoY) de los dashboards profesionales.

## 3. Paleta de Colores para Gráficos
Las referencias muestran un uso predominante de **Morado/Violeta** y **Verde**. 
*   **Color Primario (Barras, Líneas, Rellenos principales)**: Usa una gama cromática basada en tonos Violeta/Morado (ej. `#8B5CF6`, `#7C3AED` o el morado de la placa "EVA").
*   **Color Secundario (Acentos, Positivos, Sentimiento Neutral/Positivo)**: Usa un Verde vibrante pero profesional (similar al de la placa "Introducción y Casuística", ej. `#10B981` o `#16A34A`).
*   **Color de Contraste (Fricción, Negativos, Cortes)**: Usa tonos rojizos, corales o grises neutros oscuros.
*   Asegúrate de configurar el arreglo de colores (`dataColors`) en el archivo del tema JSON para que los gráficos adopten esta paleta automáticamente.

## 4. Tipografía Profesional
*   Cambia la fuente predeterminada de todo el reporte a una tipografía sans-serif moderna, limpia y profesional (ej. **Segoe UI**, **DIN**, **Roboto** o la familia **Inter** si está disponible vía tema personalizado). 
*   Quita las grillas horizontales/verticales innecesarias de los gráficos de barras y líneas para maximizar la limpieza ("data-ink ratio").

Por favor, provéeme el fragmento de código JSON del **Tema de Power BI** (`theme.json`) que aplique esta paleta, fuentes y configuraciones base para tarjetas y gráficos. Adicionalmente, dame instrucciones sobre cómo acomodar físicamente los elementos en el lienzo para lograr este layout moderno.
</instrucciones>
