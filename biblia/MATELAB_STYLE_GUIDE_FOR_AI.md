# 🧉 MateLab Style Guide for AI Assistants
## Guía de Estilos para Implementación Automatizada

**Audiencia:** Claude Code, Cursor, GitHub Copilot y otros asistentes de código  
**Versión:** 1.0  
**Fecha:** 12 de Noviembre, 2025

---

## 🎯 Objetivo de este Documento

Esta guía proporciona instrucciones **CLARAS, CONCISAS y SIN AMBIGÜEDAD** sobre qué estilos usar en cada situación al desarrollar para el ecosistema Yerba de MateLab.

---

## 📋 Reglas de Oro (SIEMPRE aplicar)

### 1. Variables CSS Obligatorias
```css
/* NUNCA uses valores hardcodeados. SIEMPRE usa variables CSS */

❌ INCORRECTO:
color: #3a5a40;
padding: 16px;
font-size: 14px;

✅ CORRECTO:
color: var(--brand-primary);
padding: var(--space-4);
font-size: var(--text-sm);
```

### 2. Theme Awareness
```css
/* SIEMPRE considera que existen 2 themes: light y dark */
/* Las variables se adaptan automáticamente, NO uses colores directos */

✅ CORRECTO:
background: var(--bg-primary);
color: var(--text-primary);
border: 1px solid var(--border-light);
```

### 3. Clases Semánticas
```html
<!-- USA clases de componentes existentes ANTES de crear CSS custom -->

❌ INCORRECTO:
<button style="background: #3a5a40; padding: 12px 24px; border-radius: 8px;">

✅ CORRECTO:
<button class="btn btn-primary">
```

---

## 🎨 Decisiones de Color

### Cuándo Usar Cada Color

| Situación | Variable a Usar | Ejemplo |
|-----------|----------------|---------|
| **Botón de acción principal** | `--brand-primary` | Guardar, Enviar, Crear |
| **Botón secundario/outline** | `--brand-primary` (borde) | Cancelar, Volver |
| **Botón de máxima prioridad** | `--brand-cta` | ¡Comprar Ahora!, Suscribirse |
| **Botón destructivo** | `--error-500` | Eliminar, Borrar |
| **Botón neutro/ghost** | `transparent` con `--text-primary` | Ver más, Detalles |
| **Texto principal** | `--text-primary` | Párrafos, contenido |
| **Texto secundario** | `--text-secondary` | Descripciones, labels |
| **Texto terciario** | `--text-tertiary` | Timestamps, metadata |
| **Texto deshabilitado** | `--text-disabled` | Inputs disabled, botones disabled |
| **Fondo de página** | `--bg-primary` | Body, main container |
| **Fondo de card/panel** | `--bg-secondary` | Cards, modales |
| **Fondo elevado** | `--bg-tertiary` | Dropdowns, tooltips |
| **Bordes sutiles** | `--border-light` | Separadores, divisiones |
| **Bordes medios** | `--border-medium` | Inputs, cards |
| **Bordes destacados** | `--border-heavy` | Focus states |
| **Éxito/Confirmación** | `--success-500` | Mensajes de éxito |
| **Advertencia** | `--warning-500` | Alertas no críticas |
| **Error** | `--error-500` | Errores, validaciones fallidas |
| **Información** | `--info-500` | Mensajes informativos |

---

## 🔤 Decisiones Tipográficas

### Qué Fuente Usar

```css
/* REGLA: Display headings = Poppins, Todo lo demás = Inter */

✅ Para h1, h2, h3:
font-family: var(--font-display); /* Poppins */

✅ Para h4, h5, h6, body, UI elements:
font-family: var(--font-sans); /* Inter */

✅ Para código:
font-family: var(--font-mono); /* JetBrains Mono */
```

### Qué Tamaño Usar

| Elemento | Variable | Uso |
|----------|----------|-----|
| **Hero title** | `--text-5xl` o `--text-6xl` | Landing pages, hero sections |
| **Page title** | `--text-4xl` | Título de página principal |
| **Section title** | `--text-3xl` | Títulos de secciones mayores |
| **Card/Panel title** | `--text-2xl` | Títulos de cards, paneles |
| **Subsection title** | `--text-xl` | Subtítulos dentro de secciones |
| **Large body** | `--text-lg` | Introducción, lead text |
| **Normal body** | `--text-base` | Texto principal (default) |
| **Small body** | `--text-sm` | Descripciones, labels |
| **Caption/metadata** | `--text-xs` | Timestamps, footnotes |

### Qué Peso Usar

```css
/* REGLA: Títulos = semibold/bold, Body = normal/medium */

✅ Para h1-h3:
font-weight: var(--font-weight-bold); /* 700 */

✅ Para h4-h6:
font-weight: var(--font-weight-semibold); /* 600 */

✅ Para body text:
font-weight: var(--font-weight-normal); /* 400 */

✅ Para labels, botones:
font-weight: var(--font-weight-medium); /* 500 */
```

---

## 📐 Decisiones de Espaciado

### Padding/Margin de Componentes

```css
/* REGLA: Usa el sistema de 8px (space-2 base) */

✅ Espaciado mínimo entre elementos relacionados:
gap: var(--space-2); /* 8px */

✅ Espaciado interno de botones:
padding: var(--space-3) var(--space-6); /* 12px 24px */

✅ Espaciado interno de cards/panels:
padding: var(--space-6); /* 24px */

✅ Espaciado entre secciones:
margin-bottom: var(--space-8); /* 32px */

✅ Espaciado entre sections grandes:
margin-bottom: var(--space-16); /* 64px */
```

### Tabla de Referencia Rápida

| Escenario | Variable |
|-----------|----------|
| Gap entre íconos y texto en botón | `--space-2` |
| Padding de input | `--space-3 --space-4` |
| Padding de botón normal | `--space-3 --space-6` |
| Padding de botón small | `--space-2 --space-4` |
| Padding de botón large | `--space-4 --space-8` |
| Padding de card | `--space-6` |
| Padding de modal | `--space-6` |
| Margin entre form fields | `--space-6` |
| Margin entre secciones | `--space-8` a `--space-12` |
| Margin entre major sections | `--space-16` a `--space-24` |

---

## 🧩 Árbol de Decisión para Componentes

### ¿Qué Componente Usar?

```
¿Necesitas un BOTÓN?
├─ ¿Es la acción principal? → .btn .btn-primary
├─ ¿Es una acción secundaria? → .btn .btn-secondary
├─ ¿Es una acción destructiva? → .btn .btn-danger
├─ ¿Es una acción de máxima prioridad? → .btn .btn-cta
├─ ¿Es una acción sutil? → .btn .btn-ghost
└─ ¿Solo tiene ícono? → .btn .btn-icon

¿Necesitas un INPUT?
├─ ¿Es texto simple? → <input class="input">
├─ ¿Es texto largo? → <textarea class="textarea">
├─ ¿Es selección? → <select class="select">
├─ ¿Es checkbox? → <input type="checkbox" class="checkbox">
├─ ¿Es radio? → <input type="radio" class="radio">
└─ ¿Tiene error? → Agrega class="input-error"

¿Necesitas una CARD?
├─ ¿Es contenedor simple? → .card
├─ ¿Tiene header? → .card > .card-header + .card-body
├─ ¿Tiene footer con acciones? → .card > .card-body + .card-footer
├─ ¿Necesita destacarse? → .card.card-accent
└─ ¿Necesita más elevación? → .card.card-elevated

¿Necesitas mostrar un MENSAJE?
├─ ¿Es éxito? → .alert.alert-success
├─ ¿Es advertencia? → .alert.alert-warning
├─ ¿Es error? → .alert.alert-error
└─ ¿Es información? → .alert.alert-info

¿Necesitas un BADGE/TAG?
├─ ¿Es estado activo/primario? → .badge.badge-primary
├─ ¿Es estado exitoso? → .badge.badge-success
├─ ¿Es advertencia? → .badge.badge-warning
└─ ¿Es solo outline? → .badge.badge-outline
```

---

## 🎨 Reglas para Usar Gradientes

### ✅ USA gradientes en:

```css
/* Hero sections */
.hero {
  background: var(--gradient-hero);
}

/* Botones CTA de máxima prioridad */
.btn-cta-special {
  background: var(--gradient-warm);
}

/* Overlays sobre imágenes */
.image-overlay {
  background: var(--gradient-primary);
  opacity: 0.8;
}
```

### ❌ NO uses gradientes en:

- Texto de body/contenido
- Botones secundarios normales
- Inputs de formularios
- Navegación principal
- Tablas de datos
- Fondos de cards normales

---

## 🔘 Reglas para Bordes Redondeados

```css
/* REGLA: Componentes más pequeños = radius más pequeño */

✅ Inputs, pequeños elementos:
border-radius: var(--radius-input); /* 6px */

✅ Botones:
border-radius: var(--radius-button); /* 8px */

✅ Cards, paneles:
border-radius: var(--radius-card); /* 12px */

✅ Modales:
border-radius: var(--radius-modal); /* 16px */

✅ Avatares, badges circulares:
border-radius: var(--radius-full); /* 9999px */
```

---

## ⚡ Reglas para Animaciones

### Cuándo Animar

```css
/* SIEMPRE anima: hover, focus, active states */

✅ Botones:
.btn {
  transition: all var(--transition-base); /* 0.2s */
}

✅ Inputs en focus:
.input:focus {
  transition: border-color var(--transition-fast); /* 0.15s */
}

✅ Cards en hover:
.card:hover {
  transition: transform var(--transition-base),
              box-shadow var(--transition-base);
}
```

### NO animes:

- Cambios de texto
- Cambios de layout mayores
- Scrolling (déjalo nativo)
- Renders iniciales de listas grandes

---

## 📱 Reglas Responsive

### Breakpoints a Usar

```css
/* MÓVIL FIRST: Estilos base = mobile, luego crece */

/* Base styles (móvil, < 640px) */
.container {
  padding: var(--space-4);
}

/* Tablet portrait (≥ 640px) */
@media (min-width: 640px) {
  .container {
    padding: var(--space-6);
  }
}

/* Tablet landscape / Desktop (≥ 1024px) */
@media (min-width: 1024px) {
  .container {
    padding: var(--space-8);
  }
}
```

### Patrones Comunes

```css
/* Stack en móvil, row en desktop */
.flex-container {
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

@media (min-width: 768px) {
  .flex-container {
    flex-direction: row;
  }
}

/* Texto centrado en móvil, left en desktop */
.text-responsive {
  text-align: center;
}

@media (min-width: 768px) {
  .text-responsive {
    text-align: left;
  }
}
```

---

## 🎯 Patrones de Código Frecuentes

### Botón con Ícono

```html
<button class="btn btn-primary">
  <svg class="icon icon-sm"><!-- ícono aquí --></svg>
  <span>Guardar</span>
</button>
```

### Form Group

```html
<div class="form-group">
  <label class="label label-required">Nombre</label>
  <input type="text" class="input" placeholder="Ingresa tu nombre">
  <span class="helper-text">Mínimo 3 caracteres</span>
</div>
```

### Card con Header y Footer

```html
<div class="card">
  <div class="card-header">
    <h3 class="card-title">Título de Card</h3>
    <p class="card-subtitle">Subtítulo opcional</p>
  </div>
  <div class="card-body">
    Contenido principal aquí
  </div>
  <div class="card-footer">
    <button class="btn btn-secondary">Cancelar</button>
    <button class="btn btn-primary">Confirmar</button>
  </div>
</div>
```

### Alert con Ícono

```html
<div class="alert alert-success">
  <svg class="alert-icon"><!-- check icon --></svg>
  <div class="alert-content">
    <strong class="alert-title">¡Éxito!</strong>
    <p class="alert-message">La operación se completó correctamente.</p>
  </div>
</div>
```

### Modal Completo

```html
<div class="modal-overlay">
  <div class="modal modal-md">
    <div class="modal-header">
      <h2 class="modal-title">Título del Modal</h2>
      <button class="modal-close" aria-label="Cerrar">×</button>
    </div>
    <div class="modal-body">
      Contenido del modal
    </div>
    <div class="modal-footer">
      <button class="btn btn-secondary">Cancelar</button>
      <button class="btn btn-primary">Confirmar</button>
    </div>
  </div>
</div>
```

### Tabla con Datos

```html
<div class="table-container">
  <table class="table table-striped">
    <thead>
      <tr>
        <th>Columna 1</th>
        <th>Columna 2</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Dato 1</td>
        <td>Dato 2</td>
        <td>
          <button class="btn btn-sm btn-ghost">Editar</button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## 🚫 Anti-Patrones (NUNCA hagas esto)

### ❌ NUNCA: Colores Hardcodeados

```css
/* MAL */
.button {
  background: #3a5a40;
  color: white;
}

/* BIEN */
.button {
  background: var(--brand-primary);
  color: var(--text-inverse);
}
```

### ❌ NUNCA: Valores de Espaciado Arbitrarios

```css
/* MAL */
.card {
  padding: 17px;
  margin-bottom: 23px;
}

/* BIEN */
.card {
  padding: var(--space-4);
  margin-bottom: var(--space-6);
}
```

### ❌ NUNCA: Fuentes Hardcodeadas

```css
/* MAL */
h1 {
  font-family: 'Poppins', sans-serif;
}

/* BIEN */
h1 {
  font-family: var(--font-display);
}
```

### ❌ NUNCA: Border Radius Aleatorio

```css
/* MAL */
.button {
  border-radius: 7px;
}

/* BIEN */
.button {
  border-radius: var(--radius-button);
}
```

### ❌ NUNCA: Estilos Inline

```html
<!-- MAL -->
<div style="padding: 20px; background: #3a5a40; color: white;">

<!-- BIEN -->
<div class="card">
```

### ❌ NUNCA: Z-index Aleatorio

```css
/* MAL */
.modal {
  z-index: 99999;
}

/* BIEN */
.modal {
  z-index: var(--z-modal);
}
```

---

## ✅ Checklist Pre-Commit

Antes de hacer commit de código CSS/HTML, verifica:

- [ ] ¿Usaste SOLO variables CSS (no valores hardcodeados)?
- [ ] ¿Usaste clases existentes antes de crear nuevas?
- [ ] ¿El contraste de texto cumple WCAG AA (4.5:1)?
- [ ] ¿Funciona en AMBOS themes (light y dark)?
- [ ] ¿Usaste el sistema de espaciado de 8px?
- [ ] ¿Los botones tienen estados hover/focus/active?
- [ ] ¿Los inputs tienen estados hover/focus/error?
- [ ] ¿Funciona en mobile (< 640px)?
- [ ] ¿Tiene navegación por teclado (si es interactivo)?
- [ ] ¿Los nombres de clases son semánticos y claros?

---

## 🔍 Cómo Debuggear Problemas de Estilo

### Problema: "El color no se ve bien en dark mode"

```
Solución: Revisa que estés usando variables semánticas, no colores directos
✅ var(--text-primary) se adapta automáticamente
❌ #1a1a1a NO se adapta
```

### Problema: "El espaciado se ve inconsistente"

```
Solución: Usa SOLO variables de espaciado del sistema
✅ var(--space-4), var(--space-6)
❌ 20px, 1.5rem arbitrarios
```

### Problema: "El botón no se ve como los demás"

```
Solución: Usa las clases existentes de botón
✅ class="btn btn-primary"
❌ Crear estilos custom
```

### Problema: "El contraste es bajo"

```
Solución: Usa variables de texto correctas
✅ var(--text-primary) = #1a1a1a (contraste alto)
❌ var(--text-tertiary) = #737373 (contraste medio, solo para metadata)
```

---

## 📖 Glosario de Variables Más Usadas

```css
/* Colores de Marca */
--brand-primary      /* Verde Mate #3a5a40 */
--brand-secondary    /* Marrón Calabaza #a67c52 */
--brand-accent       /* Verde Salvia #a3b18a */
--brand-cta         /* Terracota #d4a574 */

/* Backgrounds */
--bg-primary        /* Fondo general de app */
--bg-secondary      /* Cards, paneles */
--bg-tertiary       /* Elementos elevados */

/* Texto */
--text-primary      /* Texto principal */
--text-secondary    /* Texto secundario */
--text-tertiary     /* Metadata, timestamps */
--text-disabled     /* Texto deshabilitado */
--text-inverse      /* Texto sobre fondos oscuros */

/* Bordes */
--border-light      /* Separadores sutiles */
--border-medium     /* Bordes normales */
--border-heavy      /* Bordes destacados */

/* Espaciado Común */
--space-2          /* 8px - gap mínimo */
--space-4          /* 16px - padding de inputs */
--space-6          /* 24px - padding de cards */
--space-8          /* 32px - margin entre secciones */

/* Tipografía */
--text-xs          /* 12px */
--text-sm          /* 14px */
--text-base        /* 16px - default */
--text-lg          /* 18px */
--text-xl          /* 20px */
--text-2xl         /* 24px */

/* Fuentes */
--font-display     /* Poppins - para h1, h2, h3 */
--font-sans        /* Inter - para todo lo demás */
--font-mono        /* JetBrains Mono - para código */

/* Radios */
--radius-button    /* 8px - botones */
--radius-card      /* 12px - cards */
--radius-modal     /* 16px - modales */
--radius-input     /* 6px - inputs */

/* Sombras */
--shadow-sm        /* Sutil */
--shadow-md        /* Normal */
--shadow-lg        /* Elevada */
--shadow-xl        /* Muy elevada */

/* Semánticos */
--success-500      /* Verde éxito */
--warning-500      /* Amarillo advertencia */
--error-500        /* Rojo error */
--info-500         /* Azul información */
```

---

## 🎓 Ejemplos de Uso Correcto

### Ejemplo 1: Dashboard Card

```html
<div class="card">
  <div class="card-header">
    <h3 class="card-title">Ventas del Mes</h3>
    <span class="badge badge-success">+12%</span>
  </div>
  <div class="card-body">
    <p class="text-body">Total: $45,230</p>
    <p class="text-body-sm text-secondary">Comparado con mes anterior</p>
  </div>
</div>
```

**Por qué es correcto:**
- Usa clases de componentes existentes
- Jerarquía clara con card-header y card-body
- Badge para destacar métrica
- Texto secundario con clase específica

### Ejemplo 2: Formulario de Login

```html
<form class="form">
  <div class="form-group">
    <label class="label label-required">Email</label>
    <input 
      type="email" 
      class="input" 
      placeholder="tu@email.com"
      required
    >
  </div>
  
  <div class="form-group">
    <label class="label label-required">Contraseña</label>
    <input 
      type="password" 
      class="input" 
      placeholder="••••••••"
      required
    >
    <span class="helper-text">Mínimo 8 caracteres</span>
  </div>
  
  <button type="submit" class="btn btn-primary btn-block">
    Iniciar Sesión
  </button>
</form>
```

**Por qué es correcto:**
- form-group para organizar cada campo
- label con clase apropiada
- helper-text para instrucciones
- btn-block para botón full-width
- Uso de clases semánticas

### Ejemplo 3: Lista de Productos

```html
<div class="container">
  <h2 class="h2">Productos Disponibles</h2>
  
  <div class="grid" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: var(--space-6);">
    
    <div class="card card-accent">
      <img src="..." alt="..." style="width: 100%; border-radius: var(--radius-lg) var(--radius-lg) 0 0;">
      <div class="card-body">
        <h3 class="card-title">Producto 1</h3>
        <p class="text-body-sm text-secondary">Descripción breve</p>
        <p class="text-lg" style="color: var(--brand-primary); font-weight: var(--font-weight-bold);">$99</p>
      </div>
      <div class="card-footer">
        <button class="btn btn-primary btn-block">Agregar al Carrito</button>
      </div>
    </div>
    
    <!-- Más cards... -->
    
  </div>
</div>
```

**Por qué es correcto:**
- Grid responsive con auto-fill
- Usa var() para gap
- Cards con estructura completa
- Precio destacado con variables
- CTA claro y prominente

---

## 🚀 Quick Start para Claude Code

**Al recibir una tarea de UI, sigue este proceso:**

1. **Identifica el componente** → ¿Es un botón, card, form, modal, tabla?
2. **Usa la clase base** → Empieza con `.btn`, `.card`, `.input`, etc.
3. **Aplica variante** → `.btn-primary`, `.card-accent`, `.input-error`
4. **Usa variables CSS** → Para colores, espaciado, tipografía
5. **Verifica responsive** → ¿Funciona en mobile?
6. **Verifica dark mode** → ¿Se ve bien en ambos themes?
7. **Agrega estados** → hover, focus, active, disabled

**Ejemplo de proceso mental:**

```
Usuario: "Crea un botón para guardar"

1. Identificar: Botón
2. Clase base: .btn
3. Variante: .btn-primary (acción principal)
4. Variables: Ya incluidas en .btn-primary
5. Responsive: Los botones son responsive por defecto
6. Dark mode: var(--brand-primary) se adapta solo
7. Estados: .btn ya tiene hover/focus/active

Resultado:
<button class="btn btn-primary">Guardar</button>
```

---

## 📞 Contacto para Dudas

Si este documento no cubre tu caso de uso, contacta:

Damian Pereyra  
📧 info@matelab.com.uy  
📱 +598 91 670 863

---

**Última actualización:** 12 de Noviembre, 2025  
**Versión:** 1.0
