# Plan de Ejecución para Claude: Página Gerencial "PruebaGC"

<context>
Este documento es un plan de acción estructurado para construir la página **PruebaGC** en el reporte de Power BI "Tablero de Control de Luz". El objetivo de esta página es brindar visibilidad a nivel gerencial sobre la **Experiencia del Cliente (CX)** y los **Motivos de Fricción** de las llamadas automatizadas.
Nota importante de arquitectura: La tabla `input_majo_puro` es la que gestiona las relaciones del modelo. Las métricas relacionadas a los resultados de las llamadas se basan en la tabla `output`.
</context>

## 1. Nuevas Medidas DAX a Implementar

Basado en las reglas de negocio provistas, debes agregar las siguientes medidas a la tabla `01_Medidas`. Asegúrate de excluir los valores nulos, en blanco o con guiones ("-") de los divisores.

### 1.1. Indicadores CX (Experiencia Cualitativa)

**% Sentimiento Positivo/Neutral**
Mide qué porcentaje de los clientes reaccionó bien o de manera estándar frente a la IA.
```dax
% Sentimiento Positivo/Neutral = 
VAR TotalValidos = CALCULATE(
    COUNT(output[Sentimiento Cliente]),
    output[Sentimiento Cliente] <> "-"
)
VAR TotalPositivosNeutrales = CALCULATE(
    COUNT(output[Sentimiento Cliente]),
    output[Sentimiento Cliente] IN {"Positivo", "Neutral"}
)
RETURN DIVIDE(TotalPositivosNeutrales, TotalValidos, 0)
```

**% Interrupciones (Barge-in)**
Mide el porcentaje de llamadas donde el cliente interrumpió a la IA mientras hablaba.
```dax
% Interrupciones (Barge-in) = 
VAR TotalValidos = CALCULATE(
    COUNT(output[Interrupcion Al Bot]),
    output[Interrupcion Al Bot] <> "-"
)
VAR TotalInterrupciones = CALCULATE(
    COUNT(output[Interrupcion Al Bot]),
    output[Interrupcion Al Bot] = "Sí"
)
RETURN DIVIDE(TotalInterrupciones, TotalValidos, 0)
```

**% Carga al 0800**
Mide cuántas veces la IA tuvo que derivar o hacer mención al canal de atención humana.
```dax
% Carga al 0800 = 
VAR TotalValidos = CALCULATE(
    COUNT(output[Menciona 0800]),
    output[Menciona 0800] <> "-"
)
VAR TotalMenciones = CALCULATE(
    COUNT(output[Menciona 0800]),
    output[Menciona 0800] = "Sí"
)
RETURN DIVIDE(TotalMenciones, TotalValidos, 0)
```

### 1.2. Motivos de Fricción (Fuga de Información)

Para desglosar el 100% de la métrica base `[Cortaron Comunicación]`, crearemos medidas específicas analizando la columna `output[Motivo No Entrega]`.

Cada medida aplica filtros directos sobre columnas (sin llamar a `[Cortaron Comunicación]` internamente), lo que evita anidar iteradores y sigue las buenas prácticas del modelo.

```dax
Fricción - Segundos Iniciales = 
CALCULATE(
    COUNT(output[Interactores]),
    output[Interactores] = "No",
    output[Motivo No Entrega] = "corta la llamada"
)

Fricción - Antes de completar el mensaje = 
CALCULATE(
    COUNT(output[Interactores]),
    output[Interactores] = "No",
    output[Motivo No Entrega] IN {"error técnico", "interrupciones"}
)

Fricción - Buzón de Voz / Contestador = 
CALCULATE(
    COUNT(output[Interactores]),
    output[Interactores] = "No",
    output[Motivo No Entrega] = "contestador"
)

Fricción - Otras Causas = 
CALCULATE(
    COUNT(output[Interactores]),
    output[Interactores] = "No",
    NOT(output[Motivo No Entrega] IN {"corta la llamada", "error técnico", "interrupciones", "contestador"})
)
```

Formato requerido para las 4 medidas de Fricción al crearlas en TMDL: `formatString: 0` (entero, igual que las demás medidas de volumen del modelo).

*Para visualizar el Impacto (%), se utilizará el cálculo porcentual nativo del gráfico Deneb o Power BI dividiendo sobre el total de `[Cortaron Comunicación]`.*

---

## 2. Diseño de la Página "PruebaGC"

Configura la página para un tamaño de lienzo personalizado (ej. 1920x1080 o superior si es necesario para dar respiro a los componentes visuales).

### Sección Superior: Panel de KPIs Gerenciales (Resumen de CX)
Disposición sugerida: Una fila de Tarjetas (Cards) nativas o visuales de nuevo formato de Power BI en la parte superior.
1. **% Sentimiento Positivo/Neutral** (Formato %) - Color condicional (Verde si > 80%).
2. **% Interrupciones** (Formato %) - Acompañado de un tooltip o subtítulo "Barge-in".
3. **% Carga al 0800** (Formato %) - Indicador de derivación al canal humano.

### Sección Central: Gráficos de Deneb (Vega-Lite)
Utiliza la potencia de Deneb para representaciones gerenciales de alto impacto estético.

#### Visual 1: Gráfico de Cascada o Embudo (Funnel) Horizontal de Interacciones
- **Objetivo**: Mostrar el flujo desde el Total de `Base de Datos` -> `Contactados` -> `Interactuaron con Luz` -> `Solicitaron Conexión`.
- **Diseño**: Usa un diseño "Glassmorphism" o colores vibrantes sobre fondo oscuro (basado en el tema CY26SU02). Asegúrate de utilizar las medidas ya existentes en la tabla `01_Medidas`.

#### Visual 2: Desglose de Fricción (Fuga de Información)
- **Objetivo**: Desglosar visualmente el 100% de `[Cortaron Comunicación]`.
- **Tipo de Gráfico Deneb sugerido**: Un **Gráfico de Barras Apiladas 100%** horizontal o un **Gráfico de Donut interactivo**, usando las 4 medidas de Fricción creadas.
- **Detalle**: El tooltip o etiqueta de datos debe mostrar ambos valores: el volumen absoluto y el porcentaje (`Cantidad del Motivo Específico / Total Cortaron Comunicación * 100`).

## 3. Instrucciones Generales para la Implementación Visual
1. **Tipografía y Colores**: Asegurar que las especificaciones de Vega-Lite sigan las directrices del tema `CY26SU02` para mantener la estética premium.
2. **Interactividad**: Habilitar el filtrado cruzado entre el desglose de fricción y el resto de los KPIs (ej. al hacer clic en "Buzón de Voz", actualizar los KPIs de CX para ese subconjunto).
3. **Claridad Gerencial**: Usar títulos claros, subtítulos explicativos y evitar el exceso de ejes o grillas (mantener un estilo "limpio" y minimalista).
