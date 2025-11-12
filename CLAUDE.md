# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Tipo de Repositorio

Este es un **repositorio de documentación** (MateLabDocs) que contiene las guías de diseño, marca y estilo para el ecosistema MateLab. No contiene código fuente ejecutable.

### Estructura del Repositorio

```
matelab/
├── CLAUDE.md                              # Este archivo
└── biblia/                                # Documentación de referencia
    ├── MATELAB_DESIGN_SYSTEM.md          # Sistema de diseño visual completo
    ├── MATELAB_BRAND_TRAINING.md         # Información de marca y comunicación
    └── MATELAB_STYLE_GUIDE_FOR_AI.md     # Guía de implementación para IA
```

### Comandos Comunes

Como este es un repositorio de documentación sin código, los únicos comandos relevantes son de Git:

```bash
# Ver cambios
git status
git diff

# Agregar y commitear documentación
git add .
git commit -m "Actualizar documentación de [tema]"

# Pushear cambios
git push
```

## Proyecto MateLab

**MateLab** - Sistema SaaS modular (Yerba) para gestión empresarial de comercios uruguayos.

**Desarrollador:** Damian Pereyra
**Contacto:** info@matelab.com.uy | +598 91 670 863
**Ubicación:** Florida, Uruguay

## Arquitectura del Sistema

### Ecosistema de Productos (Naming interno)

- **Yerba** - SaaS modular (producto core)
- **Bombilla** - API/SDK para integraciones
- **Termo** - Sistema de respaldos/backup
- **Calabaza** - CRM/App móvil
- **Cebador** - Panel de administración/orquestador
- **Yerbera** - Analytics/Reportes

### Módulos de Yerba

1. **Yerba Stock** - Control de inventario y depósitos
2. **Yerba Sales** - Sistema de ventas y punto de venta
3. **Yerba Buy** - Gestión de compras y proveedores
4. **Yerbera** - Analytics y reportes visuales
5. **Yerba Call** - Call center y gestión de clientes

## Filosofía de Diseño y Marca

### Principios Core

1. **Calidez Profesional** - Colores naturales, interfaces cercanas pero profesionales
2. **Claridad Funcional** - Jerarquía visual clara, información accesible
3. **Identidad Uruguaya** - Referencias culturales sutiles, colores tierra y naturaleza
4. **Accesibilidad First** - Contraste WCAG AA mínimo (4.5:1), AAA para críticos (7:1)

### Tono de Voz

- **Tuteo (vos/tú)** en toda la comunicación - NUNCA usar "usted"
- **Cercano pero profesional** - Sin jerga técnica innecesaria
- **Honesto y directo** - Sin letra chica ni compromisos ocultos
- **Optimista y constructivo** - Enfocado en soluciones

**Tagline:** "Soluciones digitales con sabor uruguayo"
**Metáfora central:** "Como un buen mate, estamos para acompañarte"

### Palabras Características

**Usar:**
- Charlamos, tu negocio, empezás/arrancás, sencillo/simple, acompañarte, sin complicaciones

**Evitar:**
- Enterprise, solución integral, revolucionar, líder del mercado, innovación disruptiva, ecosistema digital

## Sistema de Diseño (CSS)

### Reglas de Oro (SIEMPRE APLICAR)

#### 1. Variables CSS Obligatorias

```css
/* NUNCA usar valores hardcodeados */
❌ color: #3a5a40; padding: 16px;
✅ color: var(--brand-primary); padding: var(--space-4);
```

#### 2. Theme Awareness

El sistema soporta **Light Mode (default)** y **Dark Mode** con `data-theme="light|dark"` en el elemento `<html>`.

```css
/* Las variables se adaptan automáticamente */
background: var(--bg-primary);
color: var(--text-primary);
border: 1px solid var(--border-light);
```

#### 3. Clases Semánticas

Usar clases de componentes existentes ANTES de crear CSS custom.

```html
✅ <button class="btn btn-primary">Guardar</button>
❌ <button style="background: #3a5a40; padding: 12px 24px;">
```

### Paleta de Colores (Variables)

#### Colores de Marca
- `--brand-primary` - Verde Mate (#3a5a40) - Botones primarios, enlaces
- `--brand-secondary` - Marrón Calabaza (#a67c52) - Elementos secundarios
- `--brand-accent` - Verde Salvia (#a3b18a) - Bordes suaves, elementos discretos
- `--brand-cta` - Terracota (#d4a574) - Call to Action de máxima prioridad

#### Backgrounds
- `--bg-primary` - Crema (#f5f1e8) en light, oscuro en dark
- `--bg-secondary` - Blanco (#ffffff) en light, para cards/paneles
- `--bg-tertiary` - Para elementos elevados (dropdowns, tooltips)

#### Texto
- `--text-primary` - Texto principal (negro en light, blanco suave en dark)
- `--text-secondary` - Texto secundario (descripciones, labels)
- `--text-tertiary` - Metadata, timestamps
- `--text-disabled` - Texto deshabilitado
- `--text-inverse` - Texto sobre fondos oscuros

#### Semánticos
- `--success-500` (#2fb35c) - Éxito, confirmaciones
- `--warning-500` (#f9c018) - Advertencias no críticas
- `--error-500` (#f44336) - Errores, validaciones fallidas
- `--info-500` (#1976d2) - Mensajes informativos

### Tipografía

```css
/* Fuentes */
--font-display: 'Poppins'  /* Para h1, h2, h3 */
--font-sans: 'Inter'       /* Para todo lo demás */
--font-mono: 'JetBrains Mono' /* Para código */

/* Tamaños (escala 1.250 - Major Third) */
--text-xs: 0.75rem    /* 12px - captions */
--text-sm: 0.875rem   /* 14px - labels */
--text-base: 1rem     /* 16px - body (DEFAULT) */
--text-lg: 1.125rem   /* 18px - lead text */
--text-xl: 1.25rem    /* 20px - subsections */
--text-2xl: 1.5rem    /* 24px - card titles */
--text-3xl: 1.875rem  /* 30px - section titles */
--text-4xl: 2.25rem   /* 36px - page titles */
--text-5xl: 3rem      /* 48px - hero */

/* Pesos */
--font-weight-normal: 400    /* Body text */
--font-weight-medium: 500    /* Labels, botones */
--font-weight-semibold: 600  /* h4-h6 */
--font-weight-bold: 700      /* h1-h3 */
```

### Sistema de Espaciado (Base 8px)

```css
--space-2: 0.5rem    /* 8px - gap mínimo */
--space-3: 0.75rem   /* 12px - padding de botón vertical */
--space-4: 1rem      /* 16px - padding de inputs */
--space-6: 1.5rem    /* 24px - padding de cards */
--space-8: 2rem      /* 32px - margin entre secciones */
--space-12: 3rem     /* 48px - margin entre secciones grandes */
--space-16: 4rem     /* 64px - margin entre major sections */

/* Radios */
--radius-input: 0.375rem   /* 6px - inputs */
--radius-button: 0.5rem    /* 8px - botones */
--radius-card: 0.75rem     /* 12px - cards */
--radius-modal: 1rem       /* 16px - modales */
--radius-full: 9999px      /* Circular */
```

### Componentes UI

#### Botones
```html
<button class="btn btn-primary">Acción Principal</button>
<button class="btn btn-secondary">Acción Secundaria</button>
<button class="btn btn-cta">¡Comprar Ahora!</button>
<button class="btn btn-danger">Eliminar</button>
<button class="btn btn-ghost">Ver más</button>

<!-- Tamaños -->
<button class="btn btn-sm btn-primary">Small</button>
<button class="btn btn-lg btn-primary">Large</button>
<button class="btn btn-block btn-primary">Full Width</button>

<!-- Solo ícono -->
<button class="btn btn-icon btn-ghost">×</button>
```

#### Cards
```html
<div class="card">
  <div class="card-header">
    <h3 class="card-title">Título</h3>
    <p class="card-subtitle">Subtítulo</p>
  </div>
  <div class="card-body">
    Contenido principal
  </div>
  <div class="card-footer">
    <button class="btn btn-secondary">Cancelar</button>
    <button class="btn btn-primary">Confirmar</button>
  </div>
</div>
```

#### Forms
```html
<div class="form-group">
  <label class="label label-required">Nombre</label>
  <input type="text" class="input" placeholder="Tu nombre">
  <span class="helper-text">Mínimo 3 caracteres</span>
</div>

<!-- Con error -->
<input type="email" class="input input-error">
```

#### Alerts
```html
<div class="alert alert-success">
  <svg class="alert-icon"><!-- check --></svg>
  <div class="alert-content">
    <strong class="alert-title">¡Éxito!</strong>
    <p class="alert-message">Operación completada.</p>
  </div>
</div>
```

### Responsive Design (Mobile First)

```css
/* Breakpoints */
--breakpoint-sm: 640px    /* Mobile landscape */
--breakpoint-md: 768px    /* Tablet portrait */
--breakpoint-lg: 1024px   /* Tablet landscape / Desktop */
--breakpoint-xl: 1280px   /* Desktop */

/* Patrón común */
.container {
  padding: var(--space-4);
  flex-direction: column;
}

@media (min-width: 768px) {
  .container {
    padding: var(--space-6);
    flex-direction: row;
  }
}
```

### Animaciones

```css
/* Transiciones estándar */
--transition-fast: 0.15s ease
--transition-base: 0.2s ease    /* DEFAULT */
--transition-slow: 0.3s ease

/* SIEMPRE animar hover, focus, active states */
.btn {
  transition: all var(--transition-base);
}
```

### Gradientes

**✅ Usar en:** Hero sections, botones CTA especiales, overlays sobre imágenes

**❌ NO usar en:** Texto body, botones secundarios, inputs, navegación, tablas

```css
--gradient-primary: linear-gradient(135deg, var(--mate-green-500), var(--mate-green-600))
--gradient-hero: linear-gradient(135deg, var(--mate-green-500), var(--salvia-green-400), var(--crema-200))
```

## Anti-Patrones (NUNCA HACER)

```css
/* ❌ NUNCA colores hardcodeados */
background: #3a5a40;

/* ❌ NUNCA valores de espaciado arbitrarios */
padding: 17px; margin-bottom: 23px;

/* ❌ NUNCA fuentes hardcodeadas */
font-family: 'Poppins', sans-serif;

/* ❌ NUNCA estilos inline */
<div style="padding: 20px; background: #3a5a40;">
```

```html
<!-- ❌ NUNCA crear custom CSS cuando existe componente -->
<button style="background: green; padding: 10px;">

<!-- ✅ SIEMPRE usar componentes existentes -->
<button class="btn btn-primary">
```

## Checklist Pre-Commit

Antes de hacer commit de código CSS/HTML:

- [ ] ¿Usaste SOLO variables CSS (no valores hardcodeados)?
- [ ] ¿Usaste clases existentes antes de crear nuevas?
- [ ] ¿El contraste cumple WCAG AA (4.5:1)?
- [ ] ¿Funciona en AMBOS themes (light y dark)?
- [ ] ¿Usaste el sistema de espaciado de 8px?
- [ ] ¿Los componentes interactivos tienen hover/focus/active?
- [ ] ¿Funciona en mobile (<640px)?
- [ ] ¿Tiene navegación por teclado?
- [ ] ¿Los nombres de clases son semánticos?

## Proceso para Crear UI

Al recibir una tarea de UI, seguir este proceso:

1. **Identificar componente** → ¿Botón, card, form, modal, tabla?
2. **Usar clase base** → `.btn`, `.card`, `.input`, etc.
3. **Aplicar variante** → `.btn-primary`, `.card-accent`
4. **Usar variables CSS** → Para colores, espaciado, tipografía
5. **Verificar responsive** → ¿Funciona en mobile?
6. **Verificar dark mode** → ¿Se ve bien en ambos themes?
7. **Agregar estados** → hover, focus, active, disabled

## Comunicación con Usuarios

### Estructura de Mensajes

```
1. Saludo cercano: "Hola [Nombre],"
2. Empatía: "Entiendo que necesitás [situación]"
3. Mensaje principal (directo, sin rodeos)
4. Acción clara: "Probá y avisame"
5. Cierre cálido: "Un abrazo," o "Cualquier cosa, acá estoy,"
```

### Call to Actions Típicos

- "Hablemos tomando un mate"
- "Sin compromisos, sin letra chica"
- "Charlemos sobre tu negocio"
- "Cualquier cosa, nos avisás"

### Ejemplos de Comunicación

#### Mensaje de Error
```
❌ Ups, algo no salió como esperábamos

No pudimos procesar tu solicitud en este momento.

Ya estamos trabajando para solucionarlo. Mientras tanto, podés:
• Intentar nuevamente en unos minutos
• Contactarnos si es urgente: +598 91 670 863

Disculpá las molestias.
```

#### Email de Bienvenida
```
Asunto: ¡Bienvenido a MateLab! 🧉

Hola [Nombre],

¡Qué bueno tenerte acá!

Como un buen mate, queremos acompañarte en cada paso.

Ya tenés todo listo para empezar a usar MateLab. Acá te dejo algunos pasos:

1. Ingresá a tu panel
2. Configurá tus primeros productos
3. Hacé tu primera venta de prueba

Cualquier duda, acá estamos.

Un abrazo,
Damian
```

## Documentos de Referencia

- `biblia/MATELAB_DESIGN_SYSTEM.md` - Sistema de diseño completo con todas las variables CSS
- `biblia/MATELAB_BRAND_TRAINING.md` - Información de marca, tono, valores, comunicación
- `biblia/MATELAB_STYLE_GUIDE_FOR_AI.md` - Guía detallada de implementación CSS/HTML

## Audiencia Objetivo

**Comercios PyME uruguayos:**
- 1-50 empleados
- Buscan profesionalizar gestión
- No tienen equipo técnico
- Priorizan simplicidad sobre funcionalidad exhaustiva
- Valoran trato personalizado y proveedores locales
- Sensibles al precio

**Pain points:** Gestión manual en Excel, falta de control de stock, dificultad para tomar decisiones, miedo a sistemas complejos

## Diferenciadores Clave

vs Competencia Internacional:
- Soporte local en Uruguay (no call centers extranjeros)
- Precios en pesos uruguayos
- Trato directo con desarrolladores
- Entendimiento de realidad local

vs Software Tradicional:
- Cloud (no instalación)
- Actualizaciones automáticas
- Pago por uso/módulo

vs Excel:
- Automatización
- Multi-usuario sin conflictos
- Reportes automáticos
- Respaldo automático

## Valores Fundamentales

1. **Cercanía** - Trato directo, personal y humano
2. **Simplicidad** - Fácil de usar, sin complicaciones
3. **Honestidad** - Transparencia total, sin letra chica
4. **Evolución Continua** - Mejora basada en feedback real
5. **Identidad Uruguaya** - Orgullosos de ser uruguayos
