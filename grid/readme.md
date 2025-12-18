# Teoría de CSS Grid Layout

CSS Grid Layout es un sistema de diseño bidimensional nativo de CSS que transforma la manera en que diseñamos interfaces de usuario para la web. A diferencia de Flexbox, que está diseñado principalmente para diseños unidimensionales (una fila o una columna), Grid permite controlar el diseño en ambas dimensiones (filas y columnas) simultáneamente.

---

## 1. Conceptos Fundamentales

Para comprender Grid, es útil visualizar una cuadrícula virtual sobre el lienzo de la página web.

### Grid Container (Contenedor)
Es el elemento padre sobre el cual se aplica `display: grid` o `display: inline-grid`. Al hacer esto, se establece un nuevo contexto de formato de cuadrícula para sus hijos directos.

```css
.contenedor {
  display: grid;
}
```

### Grid Items (Items)
Son los hijos directos del contenedor grid. Estos elementos se colocan automáticamente dentro de las celdas de la cuadrícula definida, aunque su posición puede ser manipulada explícitamente.

### Grid Lines (Líneas)
Son las líneas divisorias horizontales y verticales que forman la estructura de la cuadrícula. Estas líneas son numeradas comenzando desde el 1.
- Las líneas verticales delimitan las columnas.
- Las líneas horizontales delimitan las filas.
Es posible referenciar estas líneas por su número o asignarles nombres.

### Grid Tracks (Pistas)
Es el espacio genérico entre dos líneas adyacentes de la cuadrícula. En otras palabras, es lo que conocemos comúnmente como una **columna** o una **fila**.

### Grid Cell (Celda)
Es la unidad más pequeña de la cuadrícula, delimitada por cuatro líneas de grid (dos adyacentes de fila y dos adyacentes de columna). Conceptualmente similar a una celda en una hoja de cálculo.

### Grid Area (Área)
Es un espacio rectangular compuesto por una o más celdas adyacentes. Las áreas son fundamentales para el diseño de layouts semánticos.

---

## 2. Propiedades del Contenedor (Padre)

Estas propiedades definen la estructura general de la cuadrícula.

### Definición de Pistas: `grid-template-columns` y `grid-template-rows`
Estas propiedades definen el tamaño de las columnas y filas. Se puede utilizar una variedad de unidades: píxeles (`px`), porcentajes (`%`), la unidad flexible (`fr`), o la palabra clave `auto`.

```css
.contenedor {
  display: grid;
  /* Define 3 columnas: 
     1. 100px fijos
     2. 20% del ancho del contenedor
     3. El espacio restante (1fr) */
  grid-template-columns: 100px 20% 1fr;
  
  /* Define 2 filas: una automática según contenido y otra de 200px */
  grid-template-rows: auto 200px;
}
```

### La unidad `fr` (fracción)
La unidad `fr` es específica de Grid y representa una fracción del espacio libre disponible en el contenedor. Es extremadamente útil para diseños fluidos.

```css
.contenedor {
  /* Tres columnas de igual ancho */
  grid-template-columns: 1fr 1fr 1fr;
  
  /* La segunda columna es el doble de ancha que la primera y la tercera */
  grid-template-columns: 1fr 2fr 1fr;
}
```

### Función `repeat()`
Permite definir patrones repetitivos de columnas o filas de manera concisa.

```css
.contenedor {
  /* Equivalente a: 1fr 1fr 1fr 1fr */
  grid-template-columns: repeat(4, 1fr);
}
```

### Función `minmax()`
Define un rango de tamaño para una pista, estableciendo un mínimo y un máximo.

```css
.contenedor {
  /* La columna será al menos de 200px, pero puede crecer hasta 1fr */
  grid-template-columns: minmax(200px, 1fr);
}
```

### Espaciado: `gap`, `row-gap`, `column-gap`
Define el espacio vacío entre las pistas (filas y columnas). No añade espacio en los bordes exteriores del contenedor.

```css
.contenedor {
  gap: 20px; /* Aplica 20px tanto a filas como a columnas */
  /* row-gap: 20px; */
  /* column-gap: 10px; */
}
```

### Grid Template Areas
Permite nombrar secciones de la cuadrícula para referenciarlas luego en los items. Esto hace que el código CSS sea muy descriptivo y fácil de leer.

```css
.contenedor {
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "footer footer footer";
}
```

### Alineación del Contenido (Grid completa)
Si la cuadrícula total es más pequeña que el contenedor, podemos alinearla.
- `justify-content`: Alineación horizontal (start, end, center, stretch, space-around, space-between, space-evenly).
- `align-content`: Alineación vertical (start, end, center, stretch, space-around, space-between, space-evenly).

### Alineación de Items (Por defecto)
Define cómo se comportan todos los items dentro de sus celdas.
- `justify-items`: Alineación horizontal dentro de la celda (start, end, center, stretch).
- `align-items`: Alineación vertical dentro de la celda (start, end, center, stretch).

---

## 3. Propiedades de los Items (Hijos)

Estas propiedades controlan la posición y comportamiento de cada elemento individual dentro de la cuadrícula.

### Posicionamiento por Líneas
Se puede especificar explícitamente dónde comienza y termina un item.

```css
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3; /* Abarca desde la línea 1 hasta la 3 */
  
  /* Sintaxis abreviada: inicio / fin */
  grid-row: 1 / 2; 
}
```

### Palabra clave `span`
Permite especificar cuántas pistas debe ocupar el item, en lugar de definir la línea final.

```css
.item-1 {
  grid-column: 1 / span 2; /* Comienza en la línea 1 y abarca 2 columnas */
}
```

### Posicionamiento por Áreas
Si se definieron áreas en el contenedor, se asignan a los items mediante `grid-area`.

```css
.header {
  grid-area: header;
}
.sidebar {
  grid-area: sidebar;
}
```

### Alineación Individual
Un item puede sobrescribir la alineación por defecto definida en el contenedor.
- `justify-self`: Alineación horizontal del item individual (start, end, center, stretch).
- `align-self`: Alineación vertical del item individual (start, end, center, stretch).

---

## 4. Grid Implícita vs Explícita

- **Grid Explícita**: Es la que definimos manualmente con `grid-template-columns` y `grid-template-rows`.
- **Grid Implícita**: Si colocamos contenido fuera de la grid explícita, el navegador crea pistas adicionales automáticamente. Podemos controlar el tamaño de estas pistas automáticas con `grid-auto-rows` y `grid-auto-columns`.

---

## 5. Diseño Responsive Avanzado

Grid permite crear diseños adaptables potentes sin necesidad de múltiples media queries, combinando `repeat`, `auto-fit` (o `auto-fill`) y `minmax`.

```css
.contenedor {
  /* Crea tantas columnas como quepan en el contenedor.
     Cada columna tendrá un ancho mínimo de 200px y máximo de 1fr. */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

---

Para ver estos conceptos en acción, por favor revise los archivos en la carpeta `examples/`.
