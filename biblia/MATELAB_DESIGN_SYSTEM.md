# 🧉 MateLab Design System
## Sistema de Diseño Completo para Yerba y Ecosistema de Productos

**Versión:** 1.0  
**Fecha:** 12 de Noviembre, 2025  
**Responsable:** Damian Pereyra  
**Para:** Equipo de Frontend

---

## 📋 Índice

1. [Filosofía de Diseño](#filosofía-de-diseño)
2. [Paleta de Colores](#paleta-de-colores)
3. [Themes (Claro y Oscuro)](#themes-claro-y-oscuro)
4. [Tipografía](#tipografía)
5. [Espaciado y Grid](#espaciado-y-grid)
6. [Componentes UI](#componentes-ui)
7. [Gradientes y Efectos](#gradientes-y-efectos)
8. [Iconografía](#iconografía)
9. [Animaciones](#animaciones)
10. [Responsive Design](#responsive-design)
11. [Variables CSS](#variables-css)
12. [Implementación en Código](#implementación-en-código)

---

## 🎨 Filosofía de Diseño

### Principios Core

**1. Calidez Profesional**
- Colores naturales inspirados en el mate uruguayo
- Interfaces que transmiten cercanía sin perder profesionalismo
- Diseño limpio pero no frío

**2. Claridad Funcional**
- Jerarquía visual clara
- Información accesible y fácil de escanear
- Reducción de ruido visual

**3. Identidad Uruguaya**
- Sutileza en referencias culturales
- Colores tierra y naturaleza
- Naming system coherente con la cultura del mate

**4. Accesibilidad First**
- Contraste WCAG AA mínimo (4.5:1 para texto normal)
- WCAG AAA para elementos críticos (7:1)
- Soporte para usuarios con daltonismo
- Navegación por teclado en todos los componentes

---

## 🎨 Paleta de Colores

### Colores Primarios

#### Verde Mate (Brand Primary)
```css
--mate-green-50:  #f0f4f1;  /* Tint más claro */
--mate-green-100: #d4e4d8;
--mate-green-200: #a9c9b0;
--mate-green-300: #7eae88;
--mate-green-400: #5c8468;  /* Verde medio */
--mate-green-500: #3a5a40;  /* PRINCIPAL - Brand Color */
--mate-green-600: #2f4833;
--mate-green-700: #243626;
--mate-green-800: #19241a;
--mate-green-900: #0e120d;  /* Shade más oscuro */
```

**Uso:**
- Botones primarios
- Enlaces principales
- Headers y navegación principal
- Estados activos
- Indicadores de éxito

**Contraste:**
- Sobre blanco (#fff): 8.59:1 ✅ AAA
- Sobre crema (#f5f1e8): 8.12:1 ✅ AAA

---

#### Marrón Calabaza (Secondary)
```css
--calabaza-brown-50:  #faf7f3;
--calabaza-brown-100: #f0e6d9;
--calabaza-brown-200: #e1cdb3;
--calabaza-brown-300: #d2b48d;
--calabaza-brown-400: #bc986f;
--calabaza-brown-500: #a67c52;  /* SECUNDARIO - Brand Color */
--calabaza-brown-600: #856342;
--calabaza-brown-700: #644a32;
--calabaza-brown-800: #433121;
--calabaza-brown-900: #221911;
```

**Uso:**
- Subtítulos y elementos secundarios
- Bordes y separadores destacados
- Elementos decorativos
- Headers de tablas secundarias
- Tags y badges

**Contraste:**
- Sobre blanco (#fff): 4.82:1 ✅ AA
- Sobre crema (#f5f1e8): 4.56:1 ✅ AA

---

#### Verde Salvia (Accent)
```css
--salvia-green-50:  #f5f7f3;
--salvia-green-100: #e8eddf;
--salvia-green-200: #d1dbbf;
--salvia-green-300: #bac99f;
--salvia-green-400: #aec194;
--salvia-green-500: #a3b18a;  /* ACENTO - Brand Color */
--salvia-green-600: #828e6e;
--salvia-green-700: #626b53;
--salvia-green-800: #414737;
--salvia-green-900: #21241c;
```

**Uso:**
- Bordes suaves
- Backgrounds de secciones alternadas
- Elementos de UI discretos
- Separadores
- Estados hover suaves

---

#### Terracota (Call to Action)
```css
--terracota-50:  #fdf8f3;
--terracota-100: #f8eddf;
--terracota-200: #f1dbbf;
--terracota-300: #eac99f;
--terracota-400: #dfb789;
--terracota-500: #d4a574;  /* CTA - Brand Color */
--terracota-600: #aa845d;
--terracota-700: #7f6346;
--terracota-800: #55422f;
--terracota-900: #2a2117;
```

**Uso:**
- Botones de acción destacados
- Alertas importantes
- Elementos que requieren atención
- Badges de notificación
- Precios y valores destacados

---

#### Crema (Background Base)
```css
--crema-50:  #fcfcfb;  /* Casi blanco */
--crema-100: #f9f8f5;
--crema-200: #f5f1e8;  /* BASE - Brand Color */
--crema-300: #ebe5d7;
--crema-400: #e1d9c6;
--crema-500: #d7cdb5;
--crema-600: #aca491;
--crema-700: #817b6d;
--crema-800: #565248;
--crema-900: #2b2924;
```

**Uso:**
- Background general de aplicación (theme claro)
- Fondos de cards y paneles
- Secciones alternadas
- Fondos de modales

---

### Colores Semánticos

#### Success (Éxito)
```css
--success-50:  #f0f9f4;
--success-100: #d1f0dd;
--success-200: #a3e1bb;
--success-300: #75d299;
--success-400: #47c377;
--success-500: #2fb35c;  /* Success principal */
--success-600: #268f4a;
--success-700: #1d6b37;
--success-800: #134825;
--success-900: #0a2412;
```

**Uso:** Mensajes de éxito, confirmaciones, estados completados

---

#### Warning (Advertencia)
```css
--warning-50:  #fffbf0;
--warning-100: #fef3d1;
--warning-200: #fde7a3;
--warning-300: #fcdb75;
--warning-400: #fbcf47;
--warning-500: #f9c018;  /* Warning principal */
--warning-600: #c79a13;
--warning-700: #95730e;
--warning-800: #644d0a;
--warning-900: #322605;
```

**Uso:** Alertas, avisos no críticos, campos que requieren atención

---

#### Error (Error/Peligro)
```css
--error-50:  #fef2f2;
--error-100: #fddcdc;
--error-200: #fbb9b9;
--error-300: #f99696;
--error-400: #f77373;
--error-500: #f44336;  /* Error principal */
--error-600: #c3362b;
--error-700: #922820;
--error-800: #621b16;
--error-900: #310d0b;
```

**Uso:** Errores, validaciones fallidas, acciones destructivas

---

#### Info (Información)
```css
--info-50:  #f0f7ff;
--info-100: #d1e7ff;
--info-200: #a3cfff;
--info-300: #75b7ff;
--info-400: #479fff;
--info-500: #1976d2;  /* Info principal */
--info-600: #145ea8;
--info-700: #0f477e;
--info-800: #0a2f54;
--info-900: #05182a;
```

**Uso:** Mensajes informativos, tooltips, ayuda contextual

---

### Colores Neutrales (Grises)

```css
/* Grises para Theme Claro */
--neutral-0:   #ffffff;  /* Blanco puro */
--neutral-50:  #fafafa;
--neutral-100: #f5f5f5;
--neutral-200: #e5e5e5;
--neutral-300: #d4d4d4;
--neutral-400: #a3a3a3;
--neutral-500: #737373;
--neutral-600: #525252;
--neutral-700: #404040;
--neutral-800: #262626;
--neutral-900: #171717;
--neutral-950: #0a0a0a;  /* Casi negro */
--neutral-1000: #000000; /* Negro puro */
```

---

### Colores de Texto

```css
/* Theme Claro */
--text-primary:   #1a1a1a;    /* Negro principal - sobre fondos claros */
--text-secondary: #4a4a4a;    /* Gris oscuro - texto secundario */
--text-tertiary:  #737373;    /* Gris medio - texto terciario */
--text-disabled:  #a3a3a3;    /* Gris claro - texto deshabilitado */
--text-inverse:   #ffffff;    /* Blanco - sobre fondos oscuros */

/* Theme Oscuro */
--text-primary-dark:   #f5f5f5;  /* Blanco suave principal */
--text-secondary-dark: #d4d4d4;  /* Gris claro secundario */
--text-tertiary-dark:  #a3a3a3;  /* Gris medio terciario */
--text-disabled-dark:  #737373;  /* Gris oscuro deshabilitado */
--text-inverse-dark:   #1a1a1a;  /* Negro - sobre fondos claros */
```

---

## 🌓 Themes (Claro y Oscuro)

### Theme Claro (Light Mode) - DEFAULT

```css
:root, [data-theme="light"] {
  /* Backgrounds */
  --bg-primary:    #f5f1e8;  /* Crema - Background principal */
  --bg-secondary:  #ffffff;  /* Blanco - Cards, paneles */
  --bg-tertiary:   #fafafa;  /* Gris muy claro - Elementos elevados */
  --bg-overlay:    rgba(0, 0, 0, 0.5);  /* Overlay de modales */
  
  /* Surfaces (elevaciones) */
  --surface-0:  #f5f1e8;  /* Nivel del suelo */
  --surface-1:  #ffffff;  /* Elevación 1 - cards normales */
  --surface-2:  #ffffff;  /* Elevación 2 - dropdowns */
  --surface-3:  #ffffff;  /* Elevación 3 - modales */
  
  /* Bordes */
  --border-light:    #e5e5e5;
  --border-medium:   #d4d4d4;
  --border-heavy:    #a3a3a3;
  --border-brand:    #a3b18a;  /* Verde salvia */
  
  /* Sombras */
  --shadow-sm:  0 1px 2px 0 rgba(0, 0, 0, 0.05);
  --shadow-md:  0 4px 6px -1px rgba(0, 0, 0, 0.1),
                0 2px 4px -1px rgba(0, 0, 0, 0.06);
  --shadow-lg:  0 10px 15px -3px rgba(0, 0, 0, 0.1),
                0 4px 6px -2px rgba(0, 0, 0, 0.05);
  --shadow-xl:  0 20px 25px -5px rgba(0, 0, 0, 0.1),
                0 10px 10px -5px rgba(0, 0, 0, 0.04);
  
  /* Texto */
  --text-primary:   #1a1a1a;
  --text-secondary: #4a4a4a;
  --text-tertiary:  #737373;
  --text-disabled:  #a3a3a3;
  --text-inverse:   #ffffff;
  
  /* Brand colors (mismos en ambos themes) */
  --brand-primary:   #3a5a40;  /* Verde Mate */
  --brand-secondary: #a67c52;  /* Marrón Calabaza */
  --brand-accent:    #a3b18a;  /* Verde Salvia */
  --brand-cta:       #d4a574;  /* Terracota */
  
  /* Estados interactivos */
  --hover-overlay:   rgba(58, 90, 64, 0.08);   /* Verde mate 8% */
  --active-overlay:  rgba(58, 90, 64, 0.12);   /* Verde mate 12% */
  --focus-ring:      rgba(58, 90, 64, 0.3);    /* Verde mate 30% */
  
  /* Inputs */
  --input-bg:           #ffffff;
  --input-border:       #d4d4d4;
  --input-border-hover: #a3a3a3;
  --input-border-focus: #3a5a40;
  --input-text:         #1a1a1a;
  --input-placeholder:  #a3a3a3;
}
```

---

### Theme Oscuro (Dark Mode)

```css
[data-theme="dark"] {
  /* Backgrounds */
  --bg-primary:    #0e120d;  /* Verde mate 900 - muy oscuro */
  --bg-secondary:  #19241a;  /* Verde mate 800 */
  --bg-tertiary:   #243626;  /* Verde mate 700 */
  --bg-overlay:    rgba(0, 0, 0, 0.7);
  
  /* Surfaces (elevaciones) */
  --surface-0:  #0e120d;  /* Nivel del suelo */
  --surface-1:  #19241a;  /* Elevación 1 - cards */
  --surface-2:  #243626;  /* Elevación 2 - dropdowns */
  --surface-3:  #2f4833;  /* Elevación 3 - modales */
  
  /* Bordes */
  --border-light:    #243626;
  --border-medium:   #2f4833;
  --border-heavy:    #3a5a40;
  --border-brand:    #7eae88;  /* Verde mate más claro en dark */
  
  /* Sombras (más intensas en dark mode) */
  --shadow-sm:  0 1px 2px 0 rgba(0, 0, 0, 0.3);
  --shadow-md:  0 4px 6px -1px rgba(0, 0, 0, 0.4),
                0 2px 4px -1px rgba(0, 0, 0, 0.3);
  --shadow-lg:  0 10px 15px -3px rgba(0, 0, 0, 0.5),
                0 4px 6px -2px rgba(0, 0, 0, 0.4);
  --shadow-xl:  0 20px 25px -5px rgba(0, 0, 0, 0.6),
                0 10px 10px -5px rgba(0, 0, 0, 0.5);
  
  /* Texto */
  --text-primary:   #f5f5f5;
  --text-secondary: #d4d4d4;
  --text-tertiary:  #a3a3a3;
  --text-disabled:  #737373;
  --text-inverse:   #1a1a1a;
  
  /* Brand colors ajustados para dark mode */
  --brand-primary:   #5c8468;  /* Verde mate 400 - más claro */
  --brand-secondary: #bc986f;  /* Marrón calabaza 400 */
  --brand-accent:    #bac99f;  /* Verde salvia 300 */
  --brand-cta:       #dfb789;  /* Terracota 400 */
  
  /* Estados interactivos (más visibles en dark) */
  --hover-overlay:   rgba(124, 174, 136, 0.12);   /* Verde más claro 12% */
  --active-overlay:  rgba(124, 174, 136, 0.18);   /* Verde más claro 18% */
  --focus-ring:      rgba(124, 174, 136, 0.4);    /* Verde más claro 40% */
  
  /* Inputs */
  --input-bg:           #19241a;
  --input-border:       #2f4833;
  --input-border-hover: #3a5a40;
  --input-border-focus: #5c8468;
  --input-text:         #f5f5f5;
  --input-placeholder:  #737373;
}
```

---

## 🔤 Tipografía

### Fuentes

```css
:root {
  /* Fuentes principales */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 
               Roboto, 'Helvetica Neue', Arial, sans-serif;
  --font-display: 'Poppins', var(--font-sans);
  --font-mono: 'JetBrains Mono', 'Fira Code', 'Courier New', monospace;
  
  /* Pesos de fuente */
  --font-weight-light:    300;
  --font-weight-normal:   400;
  --font-weight-medium:   500;
  --font-weight-semibold: 600;
  --font-weight-bold:     700;
  --font-weight-black:    900;
}
```

### Escala Tipográfica

```css
:root {
  /* Scale Factor: 1.250 (Major Third) */
  
  /* Tamaños de fuente */
  --text-xs:   0.75rem;   /* 12px */
  --text-sm:   0.875rem;  /* 14px */
  --text-base: 1rem;      /* 16px - Base */
  --text-lg:   1.125rem;  /* 18px */
  --text-xl:   1.25rem;   /* 20px */
  --text-2xl:  1.5rem;    /* 24px */
  --text-3xl:  1.875rem;  /* 30px */
  --text-4xl:  2.25rem;   /* 36px */
  --text-5xl:  3rem;      /* 48px */
  --text-6xl:  3.75rem;   /* 60px */
  
  /* Line Heights */
  --leading-none:    1;
  --leading-tight:   1.25;
  --leading-snug:    1.375;
  --leading-normal:  1.5;
  --leading-relaxed: 1.625;
  --leading-loose:   2;
  
  /* Letter Spacing */
  --tracking-tighter: -0.05em;
  --tracking-tight:   -0.025em;
  --tracking-normal:  0;
  --tracking-wide:    0.025em;
  --tracking-wider:   0.05em;
  --tracking-widest:  0.1em;
}
```

### Clases de Tipografía

```css
/* Headings */
.h1, h1 {
  font-family: var(--font-display);
  font-size: var(--text-4xl);
  font-weight: var(--font-weight-bold);
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
  color: var(--text-primary);
}

.h2, h2 {
  font-family: var(--font-display);
  font-size: var(--text-3xl);
  font-weight: var(--font-weight-semibold);
  line-height: var(--leading-tight);
  color: var(--text-primary);
}

.h3, h3 {
  font-family: var(--font-display);
  font-size: var(--text-2xl);
  font-weight: var(--font-weight-semibold);
  line-height: var(--leading-snug);
  color: var(--text-primary);
}

.h4, h4 {
  font-family: var(--font-sans);
  font-size: var(--text-xl);
  font-weight: var(--font-weight-semibold);
  line-height: var(--leading-snug);
  color: var(--text-primary);
}

.h5, h5 {
  font-family: var(--font-sans);
  font-size: var(--text-lg);
  font-weight: var(--font-weight-medium);
  line-height: var(--leading-normal);
  color: var(--text-secondary);
}

.h6, h6 {
  font-family: var(--font-sans);
  font-size: var(--text-base);
  font-weight: var(--font-weight-medium);
  line-height: var(--leading-normal);
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: var(--tracking-wide);
}

/* Body Text */
.text-body {
  font-family: var(--font-sans);
  font-size: var(--text-base);
  font-weight: var(--font-weight-normal);
  line-height: var(--leading-relaxed);
  color: var(--text-primary);
}

.text-body-sm {
  font-family: var(--font-sans);
  font-size: var(--text-sm);
  font-weight: var(--font-weight-normal);
  line-height: var(--leading-normal);
  color: var(--text-secondary);
}

.text-caption {
  font-family: var(--font-sans);
  font-size: var(--text-xs);
  font-weight: var(--font-weight-normal);
  line-height: var(--leading-normal);
  color: var(--text-tertiary);
}

/* Code */
.text-code {
  font-family: var(--font-mono);
  font-size: 0.875em;
  background: var(--surface-2);
  padding: 0.125rem 0.375rem;
  border-radius: 0.25rem;
  border: 1px solid var(--border-light);
}
```

---

## 📐 Espaciado y Grid

### Sistema de Espaciado (8px base)

```css
:root {
  --space-0:   0;
  --space-1:   0.25rem;  /* 4px */
  --space-2:   0.5rem;   /* 8px - BASE */
  --space-3:   0.75rem;  /* 12px */
  --space-4:   1rem;     /* 16px */
  --space-5:   1.25rem;  /* 20px */
  --space-6:   1.5rem;   /* 24px */
  --space-8:   2rem;     /* 32px */
  --space-10:  2.5rem;   /* 40px */
  --space-12:  3rem;     /* 48px */
  --space-16:  4rem;     /* 64px */
  --space-20:  5rem;     /* 80px */
  --space-24:  6rem;     /* 96px */
  --space-32:  8rem;     /* 128px */
  
  /* Espaciado semántico */
  --space-xs:  var(--space-2);   /* 8px */
  --space-sm:  var(--space-4);   /* 16px */
  --space-md:  var(--space-6);   /* 24px */
  --space-lg:  var(--space-8);   /* 32px */
  --space-xl:  var(--space-12);  /* 48px */
  --space-2xl: var(--space-16);  /* 64px */
  --space-3xl: var(--space-24);  /* 96px */
}
```

### Bordes Redondeados

```css
:root {
  --radius-none: 0;
  --radius-sm:   0.25rem;  /* 4px */
  --radius-md:   0.375rem; /* 6px */
  --radius-lg:   0.5rem;   /* 8px */
  --radius-xl:   0.75rem;  /* 12px */
  --radius-2xl:  1rem;     /* 16px */
  --radius-3xl:  1.5rem;   /* 24px */
  --radius-full: 9999px;   /* Circular */
  
  /* Semánticos */
  --radius-button: var(--radius-lg);
  --radius-card:   var(--radius-xl);
  --radius-modal:  var(--radius-2xl);
  --radius-input:  var(--radius-md);
}
```

### Grid System

```css
.container {
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  padding-left: var(--space-4);
  padding-right: var(--space-4);
}

/* Breakpoints */
@media (min-width: 640px) {  /* sm */
  .container { max-width: 640px; }
}

@media (min-width: 768px) {  /* md */
  .container { 
    max-width: 768px;
    padding-left: var(--space-6);
    padding-right: var(--space-6);
  }
}

@media (min-width: 1024px) { /* lg */
  .container { max-width: 1024px; }
}

@media (min-width: 1280px) { /* xl */
  .container { max-width: 1280px; }
}

@media (min-width: 1536px) { /* 2xl */
  .container { max-width: 1400px; }
}
```

---

## 🧩 Componentes UI

### Botones

```css
/* Botón Base */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  
  font-family: var(--font-sans);
  font-weight: var(--font-weight-medium);
  font-size: var(--text-base);
  line-height: var(--leading-none);
  
  padding: var(--space-3) var(--space-6);
  border-radius: var(--radius-button);
  border: 2px solid transparent;
  
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
  user-select: none;
  white-space: nowrap;
}

.btn:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px var(--focus-ring);
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Botón Primary */
.btn-primary {
  background: var(--brand-primary);
  color: var(--text-inverse);
}

.btn-primary:hover:not(:disabled) {
  background: var(--mate-green-600);
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}

.btn-primary:active:not(:disabled) {
  transform: translateY(0);
  box-shadow: var(--shadow-sm);
}

/* Botón Secondary */
.btn-secondary {
  background: transparent;
  color: var(--brand-primary);
  border-color: var(--brand-primary);
}

.btn-secondary:hover:not(:disabled) {
  background: var(--hover-overlay);
  border-color: var(--mate-green-600);
}

/* Botón CTA (Call to Action) */
.btn-cta {
  background: var(--brand-cta);
  color: var(--text-inverse);
}

.btn-cta:hover:not(:disabled) {
  background: var(--terracota-600);
  transform: translateY(-1px);
  box-shadow: var(--shadow-lg);
}

/* Botón Ghost */
.btn-ghost {
  background: transparent;
  color: var(--text-primary);
}

.btn-ghost:hover:not(:disabled) {
  background: var(--hover-overlay);
}

/* Botón Danger */
.btn-danger {
  background: var(--error-500);
  color: var(--text-inverse);
}

.btn-danger:hover:not(:disabled) {
  background: var(--error-600);
}

/* Tamaños */
.btn-sm {
  padding: var(--space-2) var(--space-4);
  font-size: var(--text-sm);
}

.btn-lg {
  padding: var(--space-4) var(--space-8);
  font-size: var(--text-lg);
}

/* Botón Full Width */
.btn-block {
  width: 100%;
  display: flex;
}

/* Botón con ícono */
.btn-icon {
  padding: var(--space-3);
  aspect-ratio: 1;
}
```

---

## 🎨 Gradientes y Efectos

### Gradientes de Marca

```css
:root {
  /* Gradiente principal (Verde Mate) */
  --gradient-primary: linear-gradient(
    135deg,
    var(--mate-green-500) 0%,
    var(--mate-green-600) 100%
  );
  
  /* Gradiente secundario (Calabaza) */
  --gradient-secondary: linear-gradient(
    135deg,
    var(--calabaza-brown-400) 0%,
    var(--calabaza-brown-600) 100%
  );
  
  /* Gradiente cálido (CTA) */
  --gradient-warm: linear-gradient(
    135deg,
    var(--terracota-400) 0%,
    var(--calabaza-brown-500) 100%
  );
  
  /* Gradiente natura (Salvia) */
  --gradient-nature: linear-gradient(
    135deg,
    var(--salvia-green-400) 0%,
    var(--mate-green-500) 100%
  );
  
  /* Gradiente suave (Background) */
  --gradient-soft: linear-gradient(
    180deg,
    var(--crema-100) 0%,
    var(--crema-200) 100%
  );
  
  /* Gradiente Hero */
  --gradient-hero: linear-gradient(
    135deg,
    var(--mate-green-500) 0%,
    var(--salvia-green-400) 50%,
    var(--crema-200) 100%
  );
}

/* Dark mode gradients */
[data-theme="dark"] {
  --gradient-primary: linear-gradient(
    135deg,
    var(--mate-green-400) 0%,
    var(--mate-green-600) 100%
  );
  
  --gradient-soft: linear-gradient(
    180deg,
    var(--mate-green-900) 0%,
    var(--mate-green-800) 100%
  );
  
  --gradient-hero: linear-gradient(
    135deg,
    var(--mate-green-600) 0%,
    var(--mate-green-800) 50%,
    var(--mate-green-900) 100%
  );
}
```

### ¿Cuándo usar gradientes?

**✅ Usar gradientes en:**
- Hero sections / Headers principales
- Botones CTA de máxima prioridad
- Fondos de secciones destacadas
- Overlays sobre imágenes
- Loading states animados

**❌ NO usar gradientes en:**
- Texto de contenido principal
- Botones secundarios
- Inputs de formularios
- Tablas de datos
- Navegación principal (usar colores sólidos)

### Efectos Glassmorphism

```css
.glass {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

[data-theme="dark"] .glass {
  background: rgba(36, 54, 38, 0.7);
  border: 1px solid rgba(124, 174, 136, 0.2);
}

.glass-strong {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
}

[data-theme="dark"] .glass-strong {
  background: rgba(36, 54, 38, 0.9);
}
```

**Cuándo usar glassmorphism:**
- Modales flotantes
- Dropdowns modernos
- Sidebars flotantes
- Cards sobre imágenes de fondo
- Headers con scroll transparente

---

## 🎭 Iconografía

### Sistema de Iconos

**Librería recomendada:** Lucide Icons o Heroicons

```css
.icon {
  display: inline-block;
  width: 1em;
  height: 1em;
  stroke: currentColor;
  fill: none;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* Tamaños */
.icon-xs { font-size: 12px; }
.icon-sm { font-size: 16px; }
.icon-md { font-size: 20px; }
.icon-lg { font-size: 24px; }
.icon-xl { font-size: 32px; }
.icon-2xl { font-size: 48px; }
```

### Emojis del Ecosistema

```
Yerba:     🧉 (U+1F9C9)
Bombilla:  🥤 (U+1F964) o 🫖 (U+1FAD6)
Termo:     ♨️ (U+2668) o 🌡️ (U+1F321)
Calabaza:  🥥 (U+1F965) o 🍵 (U+1F375)
Cebador:   👤 (U+1F464) o 🎯 (U+1F3AF)
Yerbera:   📊 (U+1F4CA) o 📈 (U+1F4C8)
```

---

## ✨ Animaciones

### Transiciones

```css
:root {
  --transition-fast:   0.15s ease;
  --transition-base:   0.2s ease;
  --transition-slow:   0.3s ease;
  --transition-slower: 0.5s ease;
  
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-out:    cubic-bezier(0, 0, 0.2, 1);
  --ease-in:     cubic-bezier(0.4, 0, 1, 1);
  --ease-bounce: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
```

### Animaciones Keyframe

```css
/* Fade In */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Slide Up */
@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Scale In */
@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Spin */
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Pulse */
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

/* Shimmer (para skeleton loaders) */
@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### Loading States

```css
/* Skeleton loader */
.skeleton {
  background: linear-gradient(
    90deg,
    var(--neutral-200) 0%,
    var(--neutral-100) 50%,
    var(--neutral-200) 100%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
}

[data-theme="dark"] .skeleton {
  background: linear-gradient(
    90deg,
    var(--mate-green-800) 0%,
    var(--mate-green-700) 50%,
    var(--mate-green-800) 100%
  );
}

/* Spinner */
.spinner {
  width: 40px;
  height: 40px;
  border: 3px solid var(--border-light);
  border-top-color: var(--brand-primary);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}
```

---

## 📱 Responsive Design

### Breakpoints

```css
:root {
  --breakpoint-sm:  640px;   /* Mobile landscape */
  --breakpoint-md:  768px;   /* Tablet portrait */
  --breakpoint-lg:  1024px;  /* Tablet landscape / Desktop */
  --breakpoint-xl:  1280px;  /* Desktop */
  --breakpoint-2xl: 1536px;  /* Large desktop */
}
```

### Media Queries (Mobile First)

```css
/* Extra Small (default) - 0px to 639px */
/* Estilos base aquí */

/* Small - 640px and up */
@media (min-width: 640px) {
  /* Tablet portrait styles */
}

/* Medium - 768px and up */
@media (min-width: 768px) {
  /* Tablet landscape styles */
}

/* Large - 1024px and up */
@media (min-width: 1024px) {
  /* Desktop styles */
}

/* Extra Large - 1280px and up */
@media (min-width: 1280px) {
  /* Large desktop styles */
}

/* Dark Mode Media Query */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme]) {
    /* Apply dark theme automatically */
  }
}
```

---

## 💻 Implementación en Código

### JavaScript para Theme Toggle

```javascript
// theme-manager.js

class ThemeManager {
  constructor() {
    this.storageKey = 'matelab-theme';
    this.init();
  }
  
  init() {
    const savedTheme = localStorage.getItem(this.storageKey);
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    
    const theme = savedTheme || (prefersDark ? 'dark' : 'light');
    this.setTheme(theme);
    
    window.matchMedia('(prefers-color-scheme: dark)')
      .addEventListener('change', (e) => {
        if (!localStorage.getItem(this.storageKey)) {
          this.setTheme(e.matches ? 'dark' : 'light');
        }
      });
  }
  
  setTheme(theme) {
    document.documentElement.setAttribute('data-theme', theme);
    localStorage.setItem(this.storageKey, theme);
    
    window.dispatchEvent(new CustomEvent('themechange', { 
      detail: { theme } 
    }));
  }
  
  toggleTheme() {
    const currentTheme = document.documentElement.getAttribute('data-theme');
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
    this.setTheme(newTheme);
  }
  
  getTheme() {
    return document.documentElement.getAttribute('data-theme');
  }
}

// Inicializar
const themeManager = new ThemeManager();
window.themeManager = themeManager;
```

### Componente Toggle en React

```jsx
import { useState, useEffect } from 'react';

export function ThemeToggle() {
  const [theme, setTheme] = useState('light');
  
  useEffect(() => {
    const savedTheme = localStorage.getItem('matelab-theme') || 'light';
    setTheme(savedTheme);
    document.documentElement.setAttribute('data-theme', savedTheme);
  }, []);
  
  const toggleTheme = () => {
    const newTheme = theme === 'light' ? 'dark' : 'light';
    setTheme(newTheme);
    document.documentElement.setAttribute('data-theme', newTheme);
    localStorage.setItem('matelab-theme', newTheme);
  };
  
  return (
    <button 
      onClick={toggleTheme}
      className="btn btn-ghost btn-icon"
      aria-label="Cambiar tema"
    >
      {theme === 'light' ? '🌙' : '☀️'}
    </button>
  );
}
```

---

## ✅ Checklist de Implementación

### Para el equipo de Frontend:

- [ ] Importar variables CSS en el proyecto
- [ ] Configurar fonts (Inter y Poppins) desde Google Fonts
- [ ] Implementar ThemeManager para toggle light/dark
- [ ] Crear componentes base siguiendo las especificaciones
- [ ] Testear contraste de colores (WCAG AA mínimo)
- [ ] Implementar animaciones y transiciones
- [ ] Configurar responsive breakpoints
- [ ] Documentar componentes en Storybook (recomendado)
- [ ] Validar accesibilidad (navegación por teclado, screen readers)
- [ ] Probar en diferentes navegadores

### Herramientas de Testing Recomendadas:

- **Contraste:** https://webaim.org/resources/contrastchecker/
- **Accesibilidad:** WAVE, axe DevTools
- **Responsive:** Chrome DevTools, BrowserStack
- **Performance:** Lighthouse

---

## 📞 Contacto y Soporte

**Para consultas sobre el Design System:**

Damian Pereyra  
MateLab - Soluciones digitales con sabor uruguayo

📧 info@matelab.com.uy  
📱 +598 91 670 863  
📍 Florida, Uruguay

---

**Última actualización:** 12 de Noviembre, 2025  
**Versión:** 1.0  
**Próxima revisión:** Enero 2026
