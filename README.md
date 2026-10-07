# Calculadora de Relubricación con grasa

Herramienta web de una sola página (HTML, CSS y JavaScript, sin dependencias) que estima **cada cuántas semanas reengrasar** un rodamiento y **cuántos gramos aplicar**. Está pensada para usarse desde el celular, en terreno, como asistente por pantallas:

1. Tipo de rodamiento (rodillos esféricos, cilíndricos, cónicos, de agujas y rígido de bolas).
2. Cotas d, D y B sobre la figura.
3. Operación: velocidad (rpm), horas por semana y gramos por embolada (opcional).
4. Condiciones del lugar: temperatura, suciedad, humedad, vibración y posición del eje. El programa asigna cada factor a partir de lo observado.
5. Resultado: frecuencia (semanas), dosificación (g), consumo medio y cálculo paso a paso.

## Uso

**En línea:** https://vasco1-flores.github.io/relubricacion-grasa/ (GitHub Pages, rama `main`, carpeta raíz).

**Sin conexión:** descargar `index.html` y abrirlo en cualquier navegador. No requiere instalación ni servidor.

## Fórmulas

Unidades del Sistema Internacional (mm, rpm, h, g).

```
G_p     = 0,005 · D · B                              [g]   dosificación por reengrase
t_f     = K_r · [ 14·10⁶ / (n · √d) − 4·d ]          [h]   intervalo base
K_total = F_t · F_c · F_m · F_v · F_p                      factor de ajuste
t_aj    = t_f · K_total                              [h]
t       = mín( t_aj ; 30 000 h )                     [h]   tope
semanas = t / (horas de operación por semana)
```

K_r: 1 (rodillos esféricos y cónicos), 5 (cilíndricos y de agujas), 10 (bolas radiales).
F_t: 1 hasta 70 °C; sobre 70 °C se reduce a la mitad por cada 15 °C (regla SKF). Existe una opción por escalones (criterio aportado por el autor).
F_c, F_m, F_v, F_p: valores editables en «Opciones avanzadas».

## Origen y confiabilidad de los valores

| Valor | Origen | Confiabilidad (1–10) |
|---|---|---|
| G_p = 0,005·D·B | Mobil (ExxonMobil); extracto de Tribology Handbook | 7 / 6 |
| t_f y K_r | Extracto de Tribology Handbook. La forma exacta de la fórmula es una reconstrucción; verificar en el catálogo SKF | 6 |
| F_t (regla SKF) | Nota técnica de SKF | 9 |
| Tope de 30 000 h | SKF, Lube-Tech N° 44 | 8 |
| F_c, F_m, F_v, F_p y escalones de F_t | Criterio aportado por el autor, de fuentes de baja confiabilidad. **No pertenece a DIN 51825**, que clasifica grasas K. Las preguntas de terreno son una traducción propia | 2–4 |
| ν₁ requerida (referencia) | Fórmula SKF / ISO 281 citada de memoria, no verificada | — |

## Limitaciones

- La fórmula clásica de t_f solo es válida bajo cierta velocidad que depende de d (n < 14·10⁶ / (4·d·√d)). Fuera de ese rango la herramienta lo advierte y entrega solo la dosificación.
- A velocidades muy bajas el intervalo lo fijan la contaminación, el sellado y el estado de la grasa, no la velocidad. Rige el tope de 30 000 h.
- No usa el factor b_f del método de diagrama SKF (no verificado para todas las series).
- En rodamientos cónicos no está verificado si la fórmula de dosificación usa B o T.
- Herramienta de apoyo. Confirmar con la ficha del fabricante (SKF, Schaeffler/FAG) y con análisis de la grasa en servicio.

Normas de referencia: ISO 15, ISO 281, ISO 20816, DIN 51825.

## Nota sobre las figuras

Todas las figuras son esquemas propios dibujados en SVG, sin escala. La versión pública no incluye figuras de catálogos de fabricantes.
