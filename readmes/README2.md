# 📐 GUÍA COMPLETA DE CSS GRID
## De Cero a Experto - Todo lo que necesitas saber

---

## 📚 TABLA DE CONTENIDOS

1. [¿Qué es CSS Grid?](#qué-es-css-grid)
2. [Conceptos Fundamentales](#conceptos-fundamentales)
3. [Propiedades del Contenedor](#propiedades-del-contenedor)
4. [Propiedades de los Items](#propiedades-de-los-items)
5. [Unidades en Grid](#unidades-en-grid)
6. [Casos de Uso Reales](#casos-de-uso-reales)
7. [Grid vs Flexbox](#grid-vs-flexbox)
8. [Ejemplos Prácticos](#ejemplos-prácticos)
9. [Patrones Comunes](#patrones-comunes)
10. [Tips y Mejores Prácticas](#tips-y-mejores-prácticas)

---

## 🎯 ¿QUÉ ES CSS GRID?

CSS Grid Layout es un **sistema de diseño bidimensional** que te permite crear layouts complejos de manera simple y eficiente.

### Diferencia clave:
- **Flexbox**: Una dimensión (fila O columna)
- **Grid**: Dos dimensiones (filas Y columnas simultáneamente)

### ¿Cuándo usar Grid?
✅ Layouts de página completos  
✅ Galerías de imágenes  
✅ Dashboards y paneles  
✅ Cards complejas  
✅ Diseños de revistas/periódicos  
✅ Cualquier layout que necesite control en 2 dimensiones  

---

## 🧱 CONCEPTOS FUNDAMENTALES

### 1. Contenedor Grid (Grid Container)
El elemento padre que tiene `display: grid`

```css
.contenedor {
    display: grid;
}
```

### 2. Items Grid (Grid Items)
Los hijos directos del contenedor grid

```html
<div class="contenedor"> <!-- Grid Container -->
    <div>Item 1</div>     <!-- Grid Item -->
    <div>Item 2</div>     <!-- Grid Item -->
    <div>Item 3</div>     <!-- Grid Item -->
</div>
```

### 3. Líneas de Grid (Grid Lines)
Las líneas divisorias que forman la estructura del grid

```
      1        2        3        4
   ┌────────┬────────┬────────┐
 1 │        │        │        │
   ├────────┼────────┼────────┤
 2 │        │        │        │
   ├────────┼────────┼────────┤
 3 │        │        │        │
   └────────┴────────┴────────┘
```

### 4. Tracks (Filas y Columnas)
El espacio entre dos líneas consecutivas

- **Column Track**: Espacio vertical entre dos líneas de columna
- **Row Track**: Espacio horizontal entre dos líneas de fila

### 5. Celdas (Grid Cells)
La intersección de una fila y una columna

### 6. Áreas (Grid Areas)
Una o más celdas juntas que forman un área rectangular

---

## 🎛️ PROPIEDADES DEL CONTENEDOR

### 1. `display: grid`
Activa el sistema Grid

```css
.contenedor {
    display: grid;        /* Grid en bloque */
    display: inline-grid; /* Grid en línea */
}
```

---

### 2. `grid-template-columns`
Define el número y tamaño de las columnas

```css
/* Tres columnas de 200px cada una */
.grid {
    grid-template-columns: 200px 200px 200px;
}

/* Tres columnas: primera 200px, las otras iguales */
.grid {
    grid-template-columns: 200px 1fr 1fr;
}

/* Con repeat() - más limpio */
.grid {
    grid-template-columns: repeat(3, 200px);
}

/* Columnas de diferentes tamaños */
.grid {
    grid-template-columns: 100px 200px 300px;
}

/* Mix de unidades */
.grid {
    grid-template-columns: 200px 1fr 2fr;
    /* 200px fijos, el resto se divide en 3 partes (1+2) */
    /* Segunda columna: 33.33% del espacio restante */
    /* Tercera columna: 66.66% del espacio restante */
}
```

**📊 Ejemplo Visual:**
```css
grid-template-columns: 1fr 2fr 1fr;

┌─────────┬──────────────────┬─────────┐
│   25%   │       50%        │   25%   │
│  (1fr)  │      (2fr)       │  (1fr)  │
└─────────┴──────────────────┴─────────┘
```

---

### 3. `grid-template-rows`
Define el número y tamaño de las filas

```css
/* Tres filas de 100px cada una */
.grid {
    grid-template-rows: 100px 100px 100px;
}

/* Primera fija, las demás se ajustan */
.grid {
    grid-template-rows: 100px auto auto;
}

/* Con fracciones */
.grid {
    grid-template-rows: 1fr 2fr 1fr;
}
```

---

### 4. `gap` (antes grid-gap)
Espacio entre celdas

```css
/* Mismo espacio en filas y columnas */
.grid {
    gap: 20px;
}

/* Diferente espacio */
.grid {
    gap: 20px 40px; /* fila columna */
}

/* Propiedades individuales */
.grid {
    row-gap: 20px;
    column-gap: 40px;
}
```

---

### 5. `grid-template-areas`
Nombra áreas del grid para ubicar elementos

```css
.grid {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header  header  header"
        "sidebar content aside"
        "footer  footer  footer";
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**📊 Representación Visual:**
```
┌─────────────────────────────────────┐
│              HEADER                 │
├──────────┬─────────────────┬────────┤
│ SIDEBAR  │    CONTENT      │  ASIDE │
│          │                 │        │
├──────────┴─────────────────┴────────┤
│              FOOTER                 │
└─────────────────────────────────────┘
```

---

### 6. `justify-items`
Alinea items horizontalmente DENTRO de su celda

```css
.grid {
    justify-items: start;    /* ←  Izquierda */
    justify-items: center;   /* •  Centro */
    justify-items: end;      /* →  Derecha */
    justify-items: stretch;  /* ↔  Estira (default) */
}
```

---

### 7. `align-items`
Alinea items verticalmente DENTRO de su celda

```css
.grid {
    align-items: start;    /* ↑  Arriba */
    align-items: center;   /* •  Centro */
    align-items: end;      /* ↓  Abajo */
    align-items: stretch;  /* ↕  Estira (default) */
}
```

---

### 8. `justify-content`
Alinea TODO el grid horizontalmente dentro del contenedor

```css
.grid {
    justify-content: start;         /* ←  Izquierda */
    justify-content: center;        /* •  Centro */
    justify-content: end;           /* →  Derecha */
    justify-content: space-between; /* |•••| */
    justify-content: space-around;  /* •|•|•|• */
    justify-content: space-evenly;  /* |•|•|•| */
}
```

---

### 9. `align-content`
Alinea TODO el grid verticalmente dentro del contenedor

```css
.grid {
    align-content: start;
    align-content: center;
    align-content: end;
    align-content: space-between;
    align-content: space-around;
    align-content: space-evenly;
}
```

---

### 10. `grid-auto-rows` y `grid-auto-columns`
Define el tamaño de filas/columnas creadas automáticamente

```css
.grid {
    grid-template-columns: repeat(3, 200px);
    grid-auto-rows: 150px; /* Las filas adicionales serán de 150px */
}
```

---

### 11. `grid-auto-flow`
Controla cómo se colocan los items automáticamente

```css
.grid {
    grid-auto-flow: row;    /* Llena por filas (default) */
    grid-auto-flow: column; /* Llena por columnas */
    grid-auto-flow: dense;  /* Intenta llenar huecos */
}
```

---

## 🎨 PROPIEDADES DE LOS ITEMS

### 1. `grid-column` (shorthand)
Posiciona un item en columnas específicas

```css
.item {
    /* Desde línea 1 hasta línea 3 */
    grid-column: 1 / 3;
    
    /* Ocupa 2 columnas desde donde esté */
    grid-column: span 2;
    
    /* Desde línea 2 hasta el final */
    grid-column: 2 / -1;
}
```

**Propiedades individuales:**
```css
.item {
    grid-column-start: 1;
    grid-column-end: 3;
}
```

---

### 2. `grid-row` (shorthand)
Posiciona un item en filas específicas

```css
.item {
    /* Desde fila 1 hasta fila 3 */
    grid-row: 1 / 3;
    
    /* Ocupa 2 filas */
    grid-row: span 2;
}
```

**Propiedades individuales:**
```css
.item {
    grid-row-start: 1;
    grid-row-end: 3;
}
```

---

### 3. `grid-area`
Coloca un item en un área nombrada O define su posición completa

```css
/* Usando área nombrada */
.item {
    grid-area: header;
}

/* Shorthand para posición completa */
.item {
    /* grid-row-start / grid-column-start / grid-row-end / grid-column-end */
    grid-area: 1 / 1 / 3 / 3;
}
```

---

### 4. `justify-self`
Alinea UN item horizontalmente dentro de su celda

```css
.item {
    justify-self: start;   /* ←  Izquierda */
    justify-self: center;  /* •  Centro */
    justify-self: end;     /* →  Derecha */
    justify-self: stretch; /* ↔  Estira */
}
```

---

### 5. `align-self`
Alinea UN item verticalmente dentro de su celda

```css
.item {
    align-self: start;   /* ↑  Arriba */
    align-self: center;  /* •  Centro */
    align-self: end;     /* ↓  Abajo */
    align-self: stretch; /* ↕  Estira */
}
```

---

## 📏 UNIDADES EN GRID

### 1. **fr (Fracción)**
La unidad más importante de Grid. Representa una fracción del espacio disponible.

```css
.grid {
    grid-template-columns: 1fr 1fr 1fr;
    /* Tres columnas iguales, cada una toma 1/3 del espacio */
}

.grid {
    grid-template-columns: 2fr 1fr 1fr;
    /* Primera columna: 50% (2/4) */
    /* Segunda columna: 25% (1/4) */
    /* Tercera columna: 25% (1/4) */
}
```

**⚠️ Importante:** `fr` solo divide el **espacio disponible**, no el espacio total.

```css
.grid {
    grid-template-columns: 200px 1fr 2fr;
    /* 200px se toman primero */
    /* El resto se divide: 33.33% (1fr) y 66.66% (2fr) */
}
```

---

### 2. **px (Píxeles)**
Tamaño fijo

```css
.grid {
    grid-template-columns: 200px 300px 400px;
}
```

---

### 3. **% (Porcentaje)**
Relativo al contenedor

```css
.grid {
    grid-template-columns: 25% 50% 25%;
}
```

---

### 4. **auto**
Se ajusta al contenido

```css
.grid {
    grid-template-columns: auto 1fr auto;
    /* Primera y tercera columna: tamaño del contenido */
    /* Segunda columna: toma el resto del espacio */
}
```

---

### 5. **minmax(min, max)**
Define un rango de tamaño

```css
.grid {
    grid-template-columns: minmax(200px, 1fr) minmax(300px, 2fr);
    /* Primera columna: mínimo 200px, máximo 1 fracción */
    /* Segunda columna: mínimo 300px, máximo 2 fracciones */
}
```

**📌 Caso de Uso:** Responsive sin media queries

```css
.grid {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    /* Crea columnas automáticamente según el espacio */
    /* Cada columna: mínimo 250px, máximo 1fr */
}
```

---

### 6. **min-content**
Tamaño mínimo del contenido

```css
.grid {
    grid-template-columns: min-content 1fr;
    /* Primera columna: ancho mínimo necesario */
}
```

---

### 7. **max-content**
Tamaño máximo del contenido

```css
.grid {
    grid-template-columns: max-content 1fr;
    /* Primera columna: ancho máximo del contenido */
}
```

---

### 8. **fit-content()**
Limita el tamaño al contenido con un máximo

```css
.grid {
    grid-template-columns: fit-content(300px) 1fr;
    /* Primera columna: tamaño del contenido, máximo 300px */
}
```

---

## 🎯 CASOS DE USO REALES

### 📱 CASO 1: Layout de Página Completa

```css
.page {
    display: grid;
    grid-template-columns: 250px 1fr 200px;
    grid-template-rows: 80px 1fr 60px;
    grid-template-areas:
        "header  header  header"
        "sidebar content aside"
        "footer  footer  footer";
    min-height: 100vh;
    gap: 20px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**✅ Por qué Grid:**
- Control total del layout en 2D
- Áreas nombradas para claridad
- Fácil modificar en responsive

---

### 🖼️ CASO 2: Galería de Imágenes Responsive

```css
.galeria {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
```

**✅ Por qué Grid:**
- `auto-fit`: Crea columnas automáticamente
- `minmax(250px, 1fr)`: Mínimo 250px, se estira para llenar
- Sin media queries necesarios

---

### 📰 CASO 3: Layout Tipo Revista

```css
.revista {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: repeat(4, 200px);
    gap: 15px;
    grid-template-areas:
        "destacado destacado destacado destacado destacado destacado art1 art1 art1 art2 art2 art2"
        "destacado destacado destacado destacado destacado destacado art3 art3 art3 art4 art4 art4"
        "art5 art5 art5 art6 art6 art6 art7 art7 art7 art8 art8 art8"
        "art9 art9 art9 art9 art10 art10 art10 art10 art11 art11 art11 art11";
}

.destacado { grid-area: destacado; }
.articulo-1 { grid-area: art1; }
/* etc... */
```

**✅ Por qué Grid:**
- Sistema de 12 columnas flexible
- Control preciso de posicionamiento
- Fácil crear layouts complejos

---

### 🎴 CASO 4: Cards con Diferentes Alturas (Masonry-Style)

```css
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    grid-auto-rows: 50px;
    gap: 20px;
}

.card:nth-child(1) { grid-row: span 4; } /* 200px */
.card:nth-child(2) { grid-row: span 6; } /* 300px */
.card:nth-child(3) { grid-row: span 5; } /* 250px */
.card:nth-child(4) { grid-row: span 7; } /* 350px */
```

**✅ Por qué Grid:**
- `grid-auto-rows` para unidades pequeñas
- `span` para controlar altura de cada card
- Efecto "masonry" sin JavaScript

---

### 📊 CASO 5: Dashboard

```css
.dashboard {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: auto;
    gap: 20px;
    grid-template-areas:
        "stats stats stats stats"
        "chart1 chart1 chart2 chart2"
        "table table table sidebar";
}

.stats { 
    grid-area: stats;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
}
```

**✅ Por qué Grid:**
- Layouts anidados (grid dentro de grid)
- Fácil reorganizar widgets
- Control de proporciones

---

### 🛒 CASO 6: Producto con Info Lateral

```css
.producto {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto 1fr;
    gap: 30px;
    grid-template-areas:
        "imagen titulo"
        "imagen precio"
        "imagen descripcion";
}

.imagen      { grid-area: imagen; }
.titulo      { grid-area: titulo; }
.precio      { grid-area: precio; }
.descripcion { grid-area: descripcion; }
```

**✅ Por qué Grid:**
- Imagen abarca múltiples filas
- Info organizada verticalmente
- Fácil cambiar a mobile

---

### 📧 CASO 7: Email Layout

```css
.email-app {
    display: grid;
    grid-template-columns: 200px 300px 1fr;
    grid-template-rows: 60px 1fr;
    height: 100vh;
    grid-template-areas:
        "nav toolbar toolbar"
        "nav inbox   message";
}
```

**✅ Por qué Grid:**
- Layout de aplicación compleja
- Proporciones fijas y flexibles
- Altura completa de viewport

---

## ⚔️ GRID VS FLEXBOX

| Aspecto | Grid | Flexbox |
|---------|------|---------|
| **Dimensiones** | 2D (filas Y columnas) | 1D (fila O columna) |
| **Uso Principal** | Layouts de página | Componentes, navegación |
| **Control** | Desde el contenedor | Items controlan su tamaño |
| **Alineación** | Precisa en ambos ejes | Flexible en un eje |
| **Mejor para** | Layouts estructurados | Distribución flexible |

### Cuándo usar Grid:
✅ Layout completo de página  
✅ Galerías complejas  
✅ Dashboards  
✅ Diseños bidimensionales  
✅ Necesitas control preciso de filas Y columnas  

### Cuándo usar Flexbox:
✅ Navegación horizontal  
✅ Centrar elementos  
✅ Cards internas  
✅ Listas verticales  
✅ Distribución simple en una dirección  

### ¡Puedes combinarlos!
```css
.page {
    display: grid; /* Layout general */
    grid-template-columns: 200px 1fr;
}

.nav {
    display: flex; /* Navegación */
    flex-direction: column;
}

.header {
    display: flex; /* Header horizontal */
    justify-content: space-between;
}
```

---

## 💡 EJEMPLOS PRÁCTICOS COMPLETOS

### Ejemplo 1: Card Product Grid

```css
.productos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
    padding: 30px;
}

.producto-card {
    display: grid;
    grid-template-rows: 250px auto auto auto;
    background: white;
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 4px 16px rgba(0,0,0,0.1);
}

.producto-imagen {
    background: linear-gradient(135deg, #667eea, #764ba2);
}

.producto-info {
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.producto-acciones {
    padding: 20px;
    display: flex;
    gap: 10px;
}
```

---

### Ejemplo 2: Blog Layout Complejo

```css
.blog {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    gap: 20px;
}

.post-destacado {
    grid-column: span 12;
    grid-row: span 2;
}

.post-mediano {
    grid-column: span 6;
}

.post-pequeño {
    grid-column: span 4;
}

@media (max-width: 768px) {
    .post-destacado,
    .post-mediano,
    .post-pequeño {
        grid-column: span 12;
    }
}
```

---

### Ejemplo 3: Form Layout

```css
.formulario {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
}

.campo-completo {
    grid-column: span 2;
}

.campo-mitad {
    grid-column: span 1;
}

@media (max-width: 600px) {
    .formulario {
        grid-template-columns: 1fr;
    }
    
    .campo-completo,
    .campo-mitad {
        grid-column: span 1;
    }
}
```

---

## 🎨 PATRONES COMUNES

### 1. Holy Grail Layout
```css
.holy-grail {
    display: grid;
    grid-template: auto 1fr auto / 200px 1fr 200px;
    grid-template-areas:
        "header header header"
        "nav    main   aside"
        "footer footer footer";
    min-height: 100vh;
}
```

### 2. 12-Column System
```css
.container {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    gap: 20px;
}

.col-4 { grid-column: span 4; }
.col-6 { grid-column: span 6; }
.col-12 { grid-column: span 12; }
```

### 3. Centering
```css
.center {
    display: grid;
    place-items: center;
    min-height: 100vh;
}
```

### 4. RAM Pattern (Repeat, Auto, Minmax)
```css
.responsive {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
```

### 5. Sidebar que Colapsa
```css
.layout {
    display: grid;
    grid-template-columns: minmax(200px, 25%) 1fr;
}

@media (max-width: 768px) {
    .layout {
        grid-template-columns: 1fr;
    }
}
```

---

## 🚀 TIPS Y MEJORES PRÁCTICAS

### ✅ DO (Hacer)

1. **Usa `fr` en lugar de porcentajes**
```css
/* ✅ BIEN */
grid-template-columns: 1fr 2fr 1fr;

/* ❌ MAL */
grid-template-columns: 25% 50% 25%;
```

2. **Nombra áreas para claridad**
```css
/* ✅ BIEN */
grid-template-areas: "header header" "sidebar main";

/* ❌ MENOS CLARO */
.item1 { grid-column: 1 / 3; grid-row: 1; }
```

3. **Usa `gap` en lugar de márgenes**
```css
/* ✅ BIEN */
.grid {
    display: grid;
    gap: 20px;
}

/* ❌ MAL */
.item {
    margin: 10px;
}
```

4. **Usa `repeat()` para columnas repetidas**
```css
/* ✅ BIEN */
grid-template-columns: repeat(4, 1fr);

/* ❌ VERBOSO */
grid-template-columns: 1fr 1fr 1fr 1fr;
```

5. **Combina Grid y Flexbox**
```css
.grid-container {
    display: grid;
}

.flex-item {
    display: flex;
    justify-content: space-between;
}
```

---

### ❌ DON'T (Evitar)

1. **No uses Grid para todo**
```css
/* ❌ MAL - Usa Flexbox */
.nav {
    display: grid;
    grid-template-columns: repeat(5, auto);
}

/* ✅ BIEN */
.nav {
    display: flex;
    gap: 20px;
}
```

2. **No olvides el responsive**
```css
/* ✅ BIEN */
@media (max-width: 768px) {
    .grid {
        grid-template-columns: 1fr;
    }
}
```

3. **No uses Grid Lines negativas sin entender**
```css
/* -1 es la última línea */
grid-column: 1 / -1; /* Abarca todo el ancho */
```

---

## 🎓 RECURSOS PARA PRACTICAR

### Herramientas Visuales:
- **Grid Garden**: https://cssgridgarden.com/ (Juego interactivo)
- **Firefox DevTools**: Mejor inspector de Grid
- **Chrome DevTools**: También excelente

### Cheat Sheets:
- CSS Tricks Complete Guide to Grid
- MDN Grid Layout

### Ejercicios:
1. Recrea tu sitio web favorito usando solo Grid
2. Crea un dashboard con widgets movibles
3. Diseña una galería de fotos tipo Masonry
4. Construye un layout de email client

---

## 📝 RESUMEN RÁPIDO

### Contenedor Grid:
```css
display: grid;
grid-template-columns: 1fr 2fr 1fr;
grid-template-rows: auto 1fr auto;
gap: 20px;
grid-template-areas: "header header header";
```

### Items Grid:
```css
grid-column: 1 / 3;
grid-row: span 2;
grid-area: header;
```

### Responsive Automático:
```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

---

## 🎯 CONCLUSIÓN

CSS Grid es **la herramienta más poderosa** para layouts en CSS. Te permite:

✅ Crear layouts complejos fácilmente  
✅ Menos código más legible  
✅ Responsive sin muchos media queries  
✅ Control total en 2 dimensiones  
✅ Combinar con Flexbox para resultados perfectos  

**La clave es practicar**. Empieza con layouts simples y ve aumentando la complejidad. ¡Grid cambiará tu forma de hacer CSS!

---

## 📚 PRÓXIMOS PASOS

1. ✅ Practica cada propiedad individualmente
2. ✅ Recrea layouts reales
3. ✅ Combina Grid + Flexbox
4. ✅ Experimenta con áreas nombradas
5. ✅ Domina el responsive con `auto-fit` y `minmax()`

**¡Ahora ve y crea layouts increíbles! 🚀**