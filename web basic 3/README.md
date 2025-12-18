

## 📚 **ESTRUCTURA DEL PROYECTO**

```
basketball-shop/
├── index.html (Todo está aquí para simplificar)
├── README.md (Explicación general)
└── GRID-GUIDE.md (Guía de Grid)
```

---

## 🎨 **COLORES PASTELES UTILIZADOS**

```css
--color-primary: #FFB4D6    (Rosa pastel)
--color-secondary: #B4E4FF  (Azul pastel)
--color-accent: #FFC5A1     (Naranja/durazno pastel)
--color-highlight: #D4B5FF  (Morado pastel)
--color-soft-green: #C5E1A5 (Verde pastel)
```

---

## 🏗️ **GRID vs FLEXBOX - ¿Cuándo usar cada uno?**

### **FLEXBOX** ✅
**Usa Flexbox cuando:**
- Organizas elementos en **UNA dimensión** (fila O columna)
- Necesitas **alinear elementos** (centro, extremos)
- Tienes **navegación horizontal**
- Quieres **distribuir espacio** entre elementos
- Necesitas **orden flexible** de elementos

**Ejemplos en el proyecto:**
```css
/* Header - navegación horizontal */
.header-container {
    display: flex;
    justify-content: space-between;  /* Logo a la izquierda, nav a la derecha */
    align-items: center;             /* Centrado vertical */
}

/* Botones - centrar contenido */
.btn {
    display: inline-flex;
    align-items: center;             /* Centra icono y texto */
    gap: 0.5rem;                     /* Espacio entre elementos */
}
```

### **GRID** ✅
**Usa Grid cuando:**
- Organizas elementos en **DOS dimensiones** (filas Y columnas)
- Necesitas **layout complejo** con diferentes tamaños
- Quieres **control preciso** de posicionamiento
- Tienes **áreas específicas** para contenido
- Necesitas **diseño responsivo** automático

**Ejemplos en el proyecto:**
```css
/* Hero - 2 columnas (texto + imagen) */
.hero {
    display: grid;
    grid-template-columns: 1fr 1fr;  /* 2 columnas iguales */
    gap: 3rem;
}

/* Productos - cuadrícula responsiva */
.products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    /* Crea columnas automáticamente según el espacio */
}
```

---

## 📱 **RESPONSIVIDAD DETALLADA**

### **Desktop (>1024px)**
- Header: Logo izquierda, nav derecha
- Hero: 2 columnas lado a lado
- Productos: 3-4 columnas
- Ofertas: Layout especial con áreas nombradas

### **Tablet (768px - 1024px)**
```css
@media (max-width: 1024px) {
    .hero {
        grid-template-columns: 1fr;  /* 1 columna */
    }
    
    .offers-grid {
        grid-template-columns: 1fr 1fr;  /* 2 columnas */
    }
}
```

### **Mobile (<768px)**
```css
@media (max-width: 768px) {
    .header-container {
        flex-direction: column;  /* Apila verticalmente */
    }
    
    .products-grid {
        grid-template-columns: 1fr;  /* 1 producto por fila */
    }
}
```

---

## 🎯 **SECCIONES EXPLICADAS**

### **1. HEADER (Flexbox)**
```css
.header-container {
    display: flex;                /* Activamos Flexbox */
    justify-content: space-between; /* Logo y nav en extremos */
    align-items: center;          /* Centrado vertical */
    flex-wrap: wrap;              /* Permite saltos de línea */
}
```
**Por qué Flexbox:** Solo una fila horizontal, necesitamos alinear 2 elementos.

### **2. HERO (Grid)**
```css
.hero {
    display: grid;
    grid-template-columns: 1fr 1fr;  /* 2 columnas iguales */
    gap: 3rem;                       /* Espacio entre columnas */
    align-items: center;             /* Centra contenido verticalmente */
}
```
**Por qué Grid:** Necesitamos 2 columnas con control preciso del espacio.

### **3. CATEGORÍAS (Grid Auto-fit)**
```css
.categories-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
}
```
**Explicación:**
- `repeat()`: Repite el patrón
- `auto-fit`: Crea columnas según espacio disponible
- `minmax(250px, 1fr)`: Mínimo 250px, máximo 1 fracción del espacio
- **Resultado:** Se adapta automáticamente sin media queries

### **4. PRODUCTOS (Grid + Flexbox)**
```css
/* Grid externo */
.products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
}

/* Grid interno de cada card */
.product-card {
    display: grid;
    grid-template-rows: 250px auto auto;  /* Imagen fija, contenido flexible */
}

/* Flexbox para botones */
.product-actions {
    display: flex;
    gap: 0.5rem;
}
```
**Combinación perfecta:** Grid para layout general, Flexbox para detalles.

### **5. OFERTAS (Grid con Áreas Nombradas)**
```css
.offers-grid {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    grid-template-areas:
        "main-offer side-offer-1 side-offer-2"
        "main-offer side-offer-3 side-offer-4";
}

.offer-main { grid-area: main-offer; }
```
**Por qué esto es poderoso:**
- La oferta principal ocupa 2 filas
- Ofertas secundarias ocupan 1 celda cada una
- Super legible y mantenible

### **6. TESTIMONIOS (Grid + Grid interno)**
```css
.testimonials-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

/* Grid interno para avatar + texto */
.testimonial-card {
    display: grid;
    grid-template-columns: 80px 1fr;
    grid-template-rows: auto 1fr;
    grid-template-areas:
        "avatar name"
        "avatar text";
}
```

### **7. FOOTER (Grid + Flexbox)**
```css
/* Grid para columnas */
.footer-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

/* Flexbox para listas */
.footer-links {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}
```

---

## 🎓 **CONCEPTOS CLAVE DE GRID**

### **1. fr (Fracción)**
```css
grid-template-columns: 1fr 2fr 1fr;
/* Primera columna: 25% del espacio
   Segunda columna: 50% del espacio
   Tercera columna: 25% del espacio */
```

### **2. auto-fit vs auto-fill**
```css
/* auto-fit: Colapsa columnas vacías */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));

/* auto-fill: Mantiene columnas vacías */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
```

### **3. minmax()**
```css
minmax(250px, 1fr)
/* Mínimo 250px, máximo 1 fracción
   Perfecto para responsividad sin media queries */
```

### **4. gap**
```css
gap: 2rem;              /* Mismo espacio en filas y columnas */
column-gap: 2rem;       /* Solo columnas */
row-gap: 1rem;          /* Solo filas */
```

---

## 🚀 **CARACTERÍSTICAS RESPONSIVAS**

1. **Grid Auto-responsivo:** Las columnas se ajustan solas
2. **Flexbox Wrap:** Los elementos bajan automáticamente
3. **Media Queries:** Ajustes finos para móvil/tablet
4. **Viewport Units:** Tipografía escalable
5. **Min-width en Grid:** Previene elementos muy pequeños

---

## 💡 **TRUCOS Y MEJORES PRÁCTICAS**

### **Centrar con Flexbox:**
```css
display: flex;
align-items: center;      /* Vertical */
justify-content: center;  /* Horizontal */
```

### **Centrar con Grid:**
```css
display: grid;
place-items: center;  /* Ambas direcciones */
```

### **Grid Responsivo Sin Media Queries:**
```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

### **Espaciado Consistente:**
```css
:root {
    --spacing-sm: 1rem;
    --spacing-md: 2rem;
    --spacing-lg: 3rem;
}
```
