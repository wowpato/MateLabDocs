# 🧉 Yerba - Arquitectura Técnica Completa
## Sistema SaaS Modular para Gestión Empresarial

**Empresa:** MateLab  
**Producto:** Yerba Core + Ecosistema de Plugins  
**Versión:** 1.0  
**Fecha:** 12 de Noviembre, 2025  
**Autor:** Damian Pereyra

---

## 📋 Tabla de Contenidos

1. [Visión General](#visión-general)
2. [Stack Tecnológico](#stack-tecnológico)
3. [Arquitectura de Alto Nivel](#arquitectura-de-alto-nivel)
4. [Yerba Core (Orquestador)](#yerba-core-orquestador)
5. [Sistema de Plugins](#sistema-de-plugins)
6. [Event Bus](#event-bus)
7. [Base de Datos y Multitenancy](#base-de-datos-y-multitenancy)
8. [APIs y Comunicación](#apis-y-comunicación)
9. [Autenticación y Autorización](#autenticación-y-autorización)
10. [Deployment e Infraestructura](#deployment-e-infraestructura)
11. [Escalabilidad](#escalabilidad)
12. [Monitoreo y Logging](#monitoreo-y-logging)
13. [Seguridad](#seguridad)
14. [Roadmap de Desarrollo](#roadmap-de-desarrollo)

---

## 🎯 Visión General

### Concepto

Yerba es un **SaaS modular multitenancy** que permite a empresas contratar solo los módulos (plugins) que necesitan. Los plugins se comunican entre sí mediante un **Event Bus**, permitiendo:

- **Desacoplamiento total** entre plugins
- **Activación/desactivación dinámica** de funcionalidades por cliente
- **Escalabilidad independiente** de cada componente
- **Tolerancia a fallos** (si un plugin falla, no afecta a otros)

### Principios Arquitectónicos

1. **Plugin-First Architecture** - Todo es un plugin (excepto el core)
2. **Event-Driven** - Comunicación asíncrona mediante eventos
3. **Multi-Tenant** - Un solo despliegue, múltiples clientes
4. **API-First** - Todas las funcionalidades expuestas vía API
5. **Cloud-Native** - Diseñado para la nube desde el inicio
6. **Zero-Downtime Deployments** - Actualizaciones sin interrupciones
7. **Dependency-Aware Plugins** - Los plugins validan sus dependencias antes de activarse

---

## 💻 Stack Tecnológico

### Backend

#### Core Framework: **Node.js 20.x + NestJS 10.x**

**Por qué NestJS:**
- ✅ Arquitectura modular nativa (perfecto para plugins)
- ✅ TypeScript out-of-the-box (type safety)
- ✅ Dependency Injection (facilita testing y plugins)
- ✅ Decorators para eventos y metadata
- ✅ Soporte nativo para microservicios
- ✅ Documentación Swagger automática
- ✅ Gran comunidad y ecosistema maduro

**Alternativa considerada:** Express + custom architecture  
**Decisión:** NestJS por su arquitectura modular ya establecida

---

#### Lenguaje: **TypeScript 5.x**

**Por qué TypeScript:**
- ✅ Type safety para plugins (contratos claros)
- ✅ Mejor IntelliSense y DX
- ✅ Menos bugs en producción
- ✅ Refactoring más seguro
- ✅ Interfaces para event schemas

---

#### Event Bus / Message Broker: **RabbitMQ 3.12**

**Por qué RabbitMQ:**
- ✅ Pattern Pub/Sub nativo
- ✅ Dead Letter Queues (DLQ) para eventos fallidos
- ✅ Message persistence y durabilidad
- ✅ Priority queues
- ✅ Soporte para routing complejo
- ✅ Management UI incluida
- ✅ Alta disponibilidad con clustering

**Alternativa considerada:** Redis Pub/Sub, Apache Kafka  
**Decisión:** RabbitMQ por flexibilidad y características avanzadas

**Librería:** `@nestjs/microservices` + `amqplib`

---

#### Base de Datos Principal: **PostgreSQL 16.x**

**Por qué PostgreSQL:**
- ✅ JSONB para schemas dinámicos (plugins variables)
- ✅ Row Level Security (RLS) para multitenancy
- ✅ Transacciones ACID
- ✅ Índices avanzados (GIN, GIST)
- ✅ Full-text search nativo
- ✅ Particionamiento de tablas
- ✅ Extensiones (pg_cron, postgis si se necesita)
- ✅ Open source y maduro

**ORM:** Prisma 5.x

**Por qué Prisma:**
- ✅ Type-safe query builder
- ✅ Schema migrations automáticas
- ✅ Prisma Studio (GUI para DB)
- ✅ Relaciones type-safe
- ✅ Soporte multi-schema (para multitenancy)

**Alternativa considerada:** TypeORM, Drizzle  
**Decisión:** Prisma por DX superior y type safety

---

#### Cache: **Redis 7.x**

**Usos:**
- Session storage
- API response caching
- Rate limiting
- Plugin state caching
- Pub/Sub secundario (para eventos en tiempo real WebSocket)

**Librería:** `ioredis`

---

#### Object Storage: **MinIO (S3-compatible)**

**Por qué MinIO:**
- ✅ S3-compatible (fácil migrar a AWS S3)
- ✅ Self-hosted (control total)
- ✅ Más económico que S3 en inicio
- ✅ Encryption en reposo

**Uso:**
- Almacenamiento de archivos de clientes
- Backups de base de datos
- Imágenes de productos
- Documentos generados (PDFs, Excel)

**Alternativa en producción:** AWS S3 / DigitalOcean Spaces

---

### Frontend

#### Framework Principal: **Next.js 14.x (App Router)**

**Por qué Next.js:**
- ✅ SSR + SSG + CSR según necesidad
- ✅ File-based routing
- ✅ API routes integradas
- ✅ Image optimization
- ✅ SEO-friendly
- ✅ Streaming y Suspense
- ✅ Server Components
- ✅ Gran ecosistema

---

#### UI Library: **React 18.x**

#### Lenguaje: **TypeScript 5.x**

---

#### Styling: **TailwindCSS 4.x**

**Por qué Tailwind:**
- ✅ Utility-first (rápido desarrollo)
- ✅ Purge CSS automático (bundle pequeño)
- ✅ Variables CSS para themes
- ✅ Responsive design fácil
- ✅ Dark mode built-in

**Complementos:**
- `tailwindcss-animate` - Animaciones
- CSS Variables para theme system de MateLab

---

#### State Management: **Zustand + React Query (TanStack Query)**

**Zustand** para estado global de UI:
- ✅ Simple y liviano
- ✅ No boilerplate
- ✅ DevTools integradas
- ✅ TypeScript-first

**React Query** para estado del servidor:
- ✅ Caching automático
- ✅ Background refetching
- ✅ Optimistic updates
- ✅ Pagination y infinite scroll
- ✅ Request deduplication

**Alternativa considerada:** Redux Toolkit, Jotai  
**Decisión:** Zustand + React Query por simplicidad

---

#### Forms: **React Hook Form + Zod**

**Por qué React Hook Form:**
- ✅ Performante (uncontrolled)
- ✅ Validación flexible
- ✅ DevTools

**Zod:**
- ✅ Schema validation type-safe
- ✅ Mismo schema en frontend y backend
- ✅ Error messages customizables

---

#### UI Components: **shadcn/ui** (Radix UI + Tailwind)

**Por qué shadcn/ui:**
- ✅ Components copiables (no librería)
- ✅ Accesibilidad (Radix UI)
- ✅ Customizable 100%
- ✅ Tailwind-based

**Componentes adicionales:**
- `lucide-react` - Iconos
- `recharts` - Gráficos
- `@tanstack/react-table` - Tablas complejas

---

#### Realtime: **Socket.IO (WebSocket)**

**Usos:**
- Notificaciones en tiempo real
- Updates de plugins activos
- Colaboración multi-usuario
- Stock updates en vivo

---

### DevOps & Infrastructure

#### Containerización: **Docker + Docker Compose**

**Estructura:**
```
yerba-backend/
yerba-frontend/
postgres/
redis/
rabbitmq/
minio/
```

---

#### Orquestación: **Kubernetes (K8s)**

**Por qué Kubernetes:**
- ✅ Auto-scaling de pods
- ✅ Rolling updates
- ✅ Self-healing
- ✅ Service discovery
- ✅ ConfigMaps y Secrets
- ✅ Ingress para routing

**Alternativa inicial:** Docker Swarm  
**Decisión:** K8s para escalabilidad futura

---

#### CI/CD: **GitHub Actions**

**Pipeline:**
1. Lint + Test
2. Build Docker images
3. Push a registry
4. Deploy a staging
5. Tests E2E
6. Deploy a producción (manual approval)

---

#### Hosting

**Fase 1 (MVP):** DigitalOcean Kubernetes  
**Fase 2 (Escala):** AWS EKS o GCP GKE

**Por qué DigitalOcean inicial:**
- ✅ Más económico
- ✅ K8s administrado simple
- ✅ Soporte decente
- ✅ Datacenter cerca (Miami)

**Migración futura a AWS:**
- Mayor escalabilidad
- Más servicios integrados
- Multi-region

---

#### Monitoreo

**Stack:**
- **Grafana** - Dashboards
- **Prometheus** - Métricas
- **Loki** - Logs
- **Tempo** - Traces (OpenTelemetry)

**Alerting:** Grafana Alerting + Slack/Email

---

#### Logging: **Winston** (backend) + **Pino** (performance crítica)

**Log Aggregation:** Loki

**Estructura de logs:**
```json
{
  "timestamp": "ISO8601",
  "level": "info|warn|error",
  "tenantId": "uuid",
  "userId": "uuid",
  "plugin": "stock|sales|etc",
  "event": "event_name",
  "message": "...",
  "metadata": {}
}
```

---

#### Error Tracking: **Sentry**

**Cobertura:**
- Backend (NestJS)
- Frontend (Next.js)
- Source maps
- Release tracking
- Performance monitoring

---

## 🏗️ Arquitectura de Alto Nivel

### Diagrama de Componentes

```
┌─────────────────────────────────────────────────────────────┐
│                         INTERNET                            │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │  Load Balancer │
              │   (Nginx/K8s)  │
              └────────┬───────┘
                       │
           ┌───────────┴───────────┐
           │                       │
           ▼                       ▼
   ┌───────────────┐      ┌──────────────┐
   │   Frontend    │      │   Backend    │
   │   Next.js     │◄────►│   NestJS     │
   │  (SSR + SPA)  │      │  (API + Core)│
   └───────────────┘      └──────┬───────┘
                                 │
                  ┌──────────────┼──────────────┐
                  │              │              │
                  ▼              ▼              ▼
         ┌─────────────┐ ┌─────────────┐ ┌──────────┐
         │   Plugin    │ │   Plugin    │ │  Plugin  │
         │   Stock     │ │   Sales     │ │   Buy    │
         └──────┬──────┘ └──────┬──────┘ └────┬─────┘
                │               │              │
                └───────────────┼──────────────┘
                                │
                                ▼
                        ┌───────────────┐
                        │   Event Bus   │
                        │   RabbitMQ    │
                        └───────┬───────┘
                                │
                ┌───────────────┼───────────────┐
                │               │               │
                ▼               ▼               ▼
        ┌──────────────┐ ┌───────────┐ ┌──────────┐
        │  PostgreSQL  │ │   Redis   │ │  MinIO   │
        │  (Database)  │ │  (Cache)  │ │(Storage) │
        └──────────────┘ └───────────┘ └──────────┘
```

---

### Flujo de Datos Típico

**Ejemplo: Venta de producto**

1. **Usuario** hace clic en "Vender Producto" (Frontend)
2. **Frontend** llama a API: `POST /api/sales/create`
3. **API Gateway** (NestJS) valida autenticación y tenant
4. **Plugin Sales** procesa la venta:
   - Valida stock disponible (llamada interna)
   - Crea registro de venta en DB
   - Emite evento `sale.created` al Event Bus
5. **Event Bus** distribuye evento a:
   - **Plugin Stock** (escucha `sale.created`)
     - Reduce stock del producto
     - Emite evento `stock.updated`
   - **Plugin Analytics** (escucha `sale.created`)
     - Actualiza métricas de ventas
6. **Frontend** recibe respuesta y actualiza UI
7. **WebSocket** notifica cambio de stock en tiempo real

---

## 🎛️ Yerba Core (Orquestador)

### Responsabilidades

El **Yerba Core** NO es un plugin, es el **orquestador** del sistema.

**Funciones principales:**

1. **Plugin Lifecycle Management**
   - Registro de plugins
   - Activación/desactivación por tenant
   - Dependency resolution
   - Health checks

2. **Event Bus Management**
   - Inicialización de RabbitMQ
   - Configuración de exchanges y queues
   - Retry logic
   - Dead letter handling

3. **API Gateway**
   - Routing a plugins
   - Autenticación global
   - Rate limiting
   - Request logging

4. **Tenant Management**
   - Creación de tenants
   - Configuración de tenants
   - Billing tracking (qué plugins tiene activos)

5. **Authentication & Authorization**
   - Login/logout
   - JWT tokens
   - Permissions (RBAC)
   - Session management

6. **Configuration Management**
   - Variables de entorno
   - Feature flags
   - Plugin configurations

---

### Estructura del Core

```
src/
├── core/
│   ├── plugins/
│   │   ├── plugin.registry.ts        # Registro de plugins
│   │   ├── plugin.loader.ts          # Carga dinámica
│   │   ├── plugin.interface.ts       # Contrato de plugins
│   │   └── plugin.manager.ts         # Lifecycle
│   ├── events/
│   │   ├── event-bus.service.ts      # Event Bus wrapper
│   │   ├── event.interface.ts        # Event schema
│   │   └── event.decorators.ts       # @OnEvent()
│   ├── auth/
│   │   ├── auth.service.ts
│   │   ├── jwt.strategy.ts
│   │   ├── guards/
│   │   └── decorators/
│   ├── tenant/
│   │   ├── tenant.service.ts
│   │   ├── tenant.guard.ts           # RLS enforcement
│   │   └── tenant.interceptor.ts
│   └── api/
│       ├── api-gateway.controller.ts
│       └── api.module.ts
├── plugins/
│   ├── products/                     # Plugin Products (BASE)
│   ├── stock/                        # Plugin Stock
│   ├── sales/                        # Plugin Sales
│   ├── buy/                          # Plugin Buy
│   ├── analytics/                    # Plugin Analytics (Yerbera)
│   └── call/                         # Plugin Call (Yerba Call)
├── shared/
│   ├── database/
│   ├── config/
│   └── utils/
└── main.ts
```

---

### Plugin Lifecycle

```typescript
// Lifecycle de un plugin

1. REGISTRATION
   PluginRegistry.register(StockPlugin)

2. INITIALIZATION
   plugin.onInit()
   - Conectar a DB
   - Registrar eventos
   - Validar dependencies

3. ACTIVATION (por tenant)
   TenantService.activatePlugin(tenantId, 'stock')
   - Crear schemas de DB si es necesario
   - Iniciar listeners de eventos
   - plugin.onActivate(tenantId)

4. RUNNING
   - Plugin escucha eventos
   - Plugin expone endpoints
   - Plugin procesa requests

5. DEACTIVATION (por tenant)
   TenantService.deactivatePlugin(tenantId, 'stock')
   - Detener listeners
   - plugin.onDeactivate(tenantId)

6. SHUTDOWN
   plugin.onDestroy()
   - Cleanup de recursos
```

---

## 🔌 Sistema de Plugins

### Catálogo de Plugins y Dependencias

#### Yerba Products (Plugin Base - OBLIGATORIO)

**Descripción:** Gestión del catálogo de productos del comercio.

**Dependencias:** Ninguna (plugin base)

**Funcionalidades:**
- CRUD de productos
- Categorías y etiquetas
- Búsqueda y filtros
- Gestión de precios (venta y costo)
- Códigos SKU y códigos de barras
- Imágenes de productos
- Metadata extensible

**Eventos que emite:**
- `product.created` - Cuando se crea un producto
- `product.updated` - Cuando se actualiza un producto
- `product.deleted` - Cuando se elimina un producto
- `product.priceChanged` - Cuando cambia el precio

**API Endpoints:**
- `GET /api/products` - Listar productos
- `GET /api/products/:id` - Obtener producto
- `POST /api/products` - Crear producto
- `PUT /api/products/:id` - Actualizar producto
- `DELETE /api/products/:id` - Eliminar producto
- `GET /api/products/search` - Búsqueda avanzada

---

#### Yerba Stock (Gestión de Inventario)

**Descripción:** Control de stock e inventario de productos.

**Dependencias:** `['products']`

**Funcionalidades:**
- Control de stock por producto
- Gestión de múltiples depósitos/almacenes
- Alertas de stock mínimo
- Historial de movimientos de stock
- Ajustes de inventario
- Ubicaciones físicas dentro de depósitos

**Eventos que escucha:**
- `product.created` - Inicializa stock en 0
- `product.deleted` - Elimina registros de stock
- `sale.created` - Reduce stock (desde Sales)
- `purchase.completed` - Aumenta stock (desde Buy)

**Eventos que emite:**
- `stock.updated` - Cuando cambia el stock
- `stock.low` - Cuando stock < stock mínimo
- `stock.empty` - Cuando stock = 0
- `stock.adjusted` - Cuando se hace un ajuste manual

**API Endpoints:**
- `GET /api/stock` - Listar stock de todos los productos
- `GET /api/stock/:productId` - Obtener stock de un producto
- `PUT /api/stock/:productId` - Ajustar stock manualmente
- `GET /api/stock/movements` - Historial de movimientos
- `GET /api/stock/low` - Productos con stock bajo

**Validación de activación:**
```typescript
async onActivate(tenantId: string): Promise<void> {
  // Verificar que Products esté activo
  const productsActive = await this.pluginManager.isPluginActive(tenantId, 'products');
  if (!productsActive) {
    throw new Error('El plugin "products" debe estar activo para usar "stock"');
  }
  // Inicializar stock...
}
```

---

#### Yerba Sales (Sistema de Ventas/POS)

**Descripción:** Punto de venta y gestión de ventas.

**Dependencias:** `['products', 'stock']`

**Funcionalidades:**
- Registro de ventas
- Punto de venta (POS)
- Múltiples métodos de pago
- Gestión de clientes (básico)
- Facturación y tickets
- Descuentos y promociones
- Devoluciones

**Eventos que escucha:**
- `product.deleted` - Marca ventas relacionadas
- `stock.empty` - Bloquea venta de producto sin stock

**Eventos que emite:**
- `sale.created` - Cuando se registra una venta
- `sale.cancelled` - Cuando se cancela una venta
- `sale.refunded` - Cuando se hace una devolución
- `payment.received` - Cuando se recibe un pago

**API Endpoints:**
- `POST /api/sales/create` - Crear venta
- `GET /api/sales` - Listar ventas
- `GET /api/sales/:id` - Obtener venta
- `POST /api/sales/:id/refund` - Hacer devolución
- `GET /api/sales/daily` - Ventas del día

**Validación de activación:**
```typescript
async onActivate(tenantId: string): Promise<void> {
  const requiredPlugins = ['products', 'stock'];
  for (const plugin of requiredPlugins) {
    const isActive = await this.pluginManager.isPluginActive(tenantId, plugin);
    if (!isActive) {
      throw new Error(`El plugin "${plugin}" debe estar activo para usar "sales"`);
    }
  }
  // Inicializar...
}
```

---

#### Yerba Buy (Gestión de Compras)

**Descripción:** Gestión de compras a proveedores.

**Dependencias:** `['products', 'stock']`

**Funcionalidades:**
- Órdenes de compra
- Gestión de proveedores
- Recepción de mercadería
- Control de costos
- Historial de compras

**Eventos que escucha:**
- `product.deleted` - Marca órdenes relacionadas
- `stock.low` - Genera sugerencias de compra

**Eventos que emite:**
- `purchase.created` - Cuando se crea una orden
- `purchase.completed` - Cuando se recibe la mercadería
- `purchase.cancelled` - Cuando se cancela una orden
- `supplier.created` - Cuando se crea un proveedor

**API Endpoints:**
- `POST /api/purchases/create` - Crear orden de compra
- `GET /api/purchases` - Listar órdenes
- `PUT /api/purchases/:id/complete` - Marcar como recibida
- `GET /api/suppliers` - Listar proveedores

**Validación de activación:**
```typescript
async onActivate(tenantId: string): Promise<void> {
  const requiredPlugins = ['products', 'stock'];
  for (const plugin of requiredPlugins) {
    const isActive = await this.pluginManager.isPluginActive(tenantId, plugin);
    if (!isActive) {
      throw new Error(`El plugin "${plugin}" debe estar activo para usar "buy"`);
    }
  }
}
```

---

#### Yerbera (Analytics y Reportes)

**Descripción:** Sistema de analytics, métricas y reportes visuales.

**Dependencias:** `['products']` (opcional: `['sales', 'buy', 'stock']`)

**Funcionalidades:**
- Dashboard de métricas
- Reportes de ventas
- Análisis de rentabilidad
- Productos más vendidos
- Tendencias temporales
- Exportación a Excel/PDF

**Eventos que escucha:**
- `sale.created` - Actualiza métricas de ventas
- `purchase.completed` - Actualiza métricas de compras
- `stock.updated` - Actualiza gráficos de inventario
- `product.created` - Actualiza catálogo

**Eventos que emite:**
- `report.generated` - Cuando se genera un reporte
- `alert.threshold` - Cuando se supera un umbral

**API Endpoints:**
- `GET /api/analytics/dashboard` - Dashboard general
- `GET /api/analytics/sales` - Análisis de ventas
- `GET /api/analytics/products` - Análisis de productos
- `POST /api/analytics/export` - Exportar reportes

**Validación de activación:**
```typescript
async onActivate(tenantId: string): Promise<void> {
  // Products es obligatorio
  const productsActive = await this.pluginManager.isPluginActive(tenantId, 'products');
  if (!productsActive) {
    throw new Error('El plugin "products" debe estar activo para usar "analytics"');
  }

  // Los demás son opcionales pero se detectan para funcionalidades
  const salesActive = await this.pluginManager.isPluginActive(tenantId, 'sales');
  const buyActive = await this.pluginManager.isPluginActive(tenantId, 'buy');
  const stockActive = await this.pluginManager.isPluginActive(tenantId, 'stock');

  this.features = {
    salesAnalytics: salesActive,
    purchaseAnalytics: buyActive,
    stockAnalytics: stockActive,
  };
}
```

---

#### Yerba Call (CRM y Call Center)

**Descripción:** Gestión de clientes y call center.

**Dependencias:** `['products']` (opcional: `['sales']`)

**Funcionalidades:**
- Gestión de clientes (CRM)
- Historial de llamadas
- Seguimiento de consultas
- Tickets de soporte
- Notas y comentarios

**Eventos que escucha:**
- `sale.created` - Asocia venta a cliente
- `product.created` - Actualiza catálogo visible

**Eventos que emite:**
- `customer.created` - Cuando se crea un cliente
- `customer.updated` - Cuando se actualiza un cliente
- `call.logged` - Cuando se registra una llamada
- `ticket.created` - Cuando se crea un ticket

**API Endpoints:**
- `GET /api/customers` - Listar clientes
- `POST /api/customers` - Crear cliente
- `GET /api/calls` - Historial de llamadas
- `POST /api/tickets` - Crear ticket

---

### Grafo de Dependencias

```
Yerba Products (base)
      │
      ├─────────────┬─────────────┬─────────────┐
      │             │             │             │
      ▼             ▼             ▼             ▼
 Yerba Stock   Yerba Call    Yerbera      (otros plugins)
      │             │         (opcional: sales, buy, stock)
      ├─────┬───────┘
      │     │
      ▼     ▼
 Yerba Sales
      │
      ▼
 Yerba Buy

Leyenda:
━━━━━ Dependencia obligatoria
╌╌╌╌╌ Dependencia opcional
```

**Orden de activación recomendado:**
1. **Yerba Products** (base, sin dependencias)
2. **Yerba Stock** (depende de Products)
3. **Yerba Sales** (depende de Products + Stock)
4. **Yerba Buy** (depende de Products + Stock)
5. **Yerbera** (depende de Products, opcional: Sales, Buy, Stock)
6. **Yerba Call** (depende de Products, opcional: Sales)

**Restricciones:**
- ❌ NO se puede activar Stock sin Products
- ❌ NO se puede activar Sales sin Products y Stock
- ❌ NO se puede activar Buy sin Products y Stock
- ❌ NO se puede desactivar Products si hay otros plugins activos que dependen de él
- ✅ Se puede activar Yerbera con solo Products (funcionalidad limitada)
- ✅ Se puede activar Yerba Call con solo Products (funcionalidad limitada)

---

### Contrato de Plugin (Interface)

```typescript
// src/core/plugins/plugin.interface.ts

export interface IPlugin {
  // Metadata
  name: string;
  version: string;
  description: string;
  dependencies: string[];  // Otros plugins requeridos
  
  // Lifecycle hooks
  onInit(): Promise<void>;
  onActivate(tenantId: string): Promise<void>;
  onDeactivate(tenantId: string): Promise<void>;
  onDestroy(): Promise<void>;
  
  // Event subscription
  getEventSubscriptions(): EventSubscription[];
  
  // API endpoints
  getRoutes(): RouteDefinition[];
  
  // Database schema (opcional)
  getDatabaseSchema?(): DatabaseSchema;
  
  // Health check
  healthCheck(tenantId: string): Promise<HealthStatus>;
}

export interface EventSubscription {
  event: string;              // 'sale.created'
  handler: string;            // 'handleSaleCreated'
  priority?: number;          // Para orden de ejecución
}

export interface RouteDefinition {
  path: string;               // '/stock/products'
  method: 'GET' | 'POST' | 'PUT' | 'DELETE';
  handler: string;            // 'getProducts'
  auth: boolean;              // Requiere autenticación
  permissions?: string[];     // ['stock:read']
}
```

---

## 🔄 Event Bus

### Arquitectura de Eventos

```
┌────────────────────────────────────────────────────────┐
│                    RabbitMQ                            │
│                                                        │
│  ┌────────────┐       ┌────────────┐                 │
│  │  Exchange  │──────►│   Queue    │──► Plugin Stock │
│  │  (Topic)   │       │ stock.*    │                 │
│  │            │       └────────────┘                 │
│  │            │                                       │
│  │            │       ┌────────────┐                 │
│  │            │──────►│   Queue    │──► Plugin Sales │
│  │            │       │ sale.*     │                 │
│  │            │       └────────────┘                 │
│  │            │                                       │
│  │            │       ┌────────────┐                 │
│  │            │──────►│   Queue    │──► Plugin Analy │
│  │            │       │  *.* (all) │                 │
│  └────────────┘       └────────────┘                 │
│                                                        │
│  ┌────────────┐                                       │
│  │    DLQ     │  Dead Letter Queue (eventos fallidos)│
│  └────────────┘                                       │
└────────────────────────────────────────────────────────┘
```

---

### Event Schema

```typescript
// src/core/events/event.interface.ts

export interface YerbaEvent<T = any> {
  // Metadata
  id: string;              // UUID del evento
  type: string;            // 'sale.created', 'stock.updated'
  version: string;         // '1.0' para versionado
  timestamp: Date;         // Cuándo se emitió
  
  // Context
  tenantId: string;        // Tenant que emitió
  userId?: string;         // Usuario que causó el evento
  source: string;          // Plugin que emitió ('sales')
  
  // Payload
  payload: T;              // Data específica del evento
  
  // Retry logic
  attemptNumber?: number;  // Para retry
  maxAttempts?: number;    // Máximo de reintentos
}

// Ejemplos de payloads

export interface SaleCreatedPayload {
  saleId: string;
  productId: string;
  quantity: number;
  price: number;
  customerId?: string;
}

export interface StockUpdatedPayload {
  productId: string;
  previousStock: number;
  newStock: number;
  reason: 'sale' | 'purchase' | 'adjustment';
}
```

---

## 🗄️ Base de Datos y Multitenancy

### Estrategia de Multitenancy

**Opción elegida:** **Schema-per-tenant** híbrido

**Por qué:**
- ✅ Aislamiento fuerte de datos por tenant
- ✅ Migraciones independientes por tenant
- ✅ Backup/restore por tenant
- ✅ Mejor que row-level cuando hay muchos tenants
- ❌ Más complejo que database-per-tenant
- ✅ Menos infraestructura que database-per-tenant

---

### Estructura de Base de Datos

```sql
-- Schema público (metadata global)
CREATE SCHEMA public;

-- Tablas globales en schema público
CREATE TABLE public.tenants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  slug VARCHAR(100) UNIQUE NOT NULL,
  status VARCHAR(50) DEFAULT 'active',
  plan VARCHAR(50),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE public.tenant_plugins (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES public.tenants(id),
  plugin_name VARCHAR(100) NOT NULL,
  is_active BOOLEAN DEFAULT TRUE,
  config JSONB,
  activated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(tenant_id, plugin_name)
);

CREATE TABLE public.users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES public.tenants(id),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(50) DEFAULT 'user',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Schema por tenant (uno por cada cliente)
-- Ejemplo: tenant_abc123

CREATE SCHEMA tenant_abc123;

-- ========================================
-- PLUGIN: Products (BASE)
-- ========================================

CREATE TABLE tenant_abc123.products (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sku VARCHAR(100) UNIQUE NOT NULL,
  barcode VARCHAR(100),
  name VARCHAR(255) NOT NULL,
  description TEXT,
  category VARCHAR(100),
  brand VARCHAR(100),
  tags JSONB DEFAULT '[]',

  -- Pricing
  price DECIMAL(10, 2) NOT NULL,          -- Precio de venta
  cost DECIMAL(10, 2),                    -- Costo de compra

  -- Flags
  is_active BOOLEAN DEFAULT TRUE,

  -- Metadata extensible (para plugins adicionales)
  metadata JSONB DEFAULT '{}',

  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_products_sku ON tenant_abc123.products(sku);
CREATE INDEX idx_products_barcode ON tenant_abc123.products(barcode);
CREATE INDEX idx_products_category ON tenant_abc123.products(category);
CREATE INDEX idx_products_active ON tenant_abc123.products(is_active);

-- ========================================
-- PLUGIN: Stock
-- ========================================

CREATE TABLE tenant_abc123.stock (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  product_id UUID NOT NULL REFERENCES tenant_abc123.products(id) ON DELETE CASCADE,
  warehouse_id UUID,                      -- NULL = depósito principal

  -- Stock quantities
  quantity INTEGER NOT NULL DEFAULT 0,
  min_stock INTEGER DEFAULT 0,
  max_stock INTEGER,

  -- Location
  location VARCHAR(100),                  -- Ubicación física (ej: "Estante A3")

  -- Metadata
  metadata JSONB DEFAULT '{}',

  -- Timestamps
  last_movement TIMESTAMP,
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE(product_id, warehouse_id)        -- Un registro por producto por depósito
);

CREATE INDEX idx_stock_product ON tenant_abc123.stock(product_id);
CREATE INDEX idx_stock_warehouse ON tenant_abc123.stock(warehouse_id);
CREATE INDEX idx_stock_low ON tenant_abc123.stock(quantity) WHERE quantity <= min_stock;

-- Historial de movimientos de stock
CREATE TABLE tenant_abc123.stock_movements (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  product_id UUID NOT NULL REFERENCES tenant_abc123.products(id),
  stock_id UUID NOT NULL REFERENCES tenant_abc123.stock(id),

  -- Movement info
  type VARCHAR(50) NOT NULL,              -- 'sale', 'purchase', 'adjustment', 'return'
  quantity INTEGER NOT NULL,              -- Positivo o negativo
  previous_quantity INTEGER NOT NULL,
  new_quantity INTEGER NOT NULL,

  -- Context
  reason TEXT,
  reference_id UUID,                      -- ID de la venta/compra que causó el movimiento
  user_id UUID,

  -- Metadata
  metadata JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_movements_product ON tenant_abc123.stock_movements(product_id);
CREATE INDEX idx_movements_stock ON tenant_abc123.stock_movements(stock_id);
CREATE INDEX idx_movements_type ON tenant_abc123.stock_movements(type);
CREATE INDEX idx_movements_reference ON tenant_abc123.stock_movements(reference_id);

-- ========================================
-- PLUGIN: Sales
-- ========================================

CREATE TABLE tenant_abc123.sales (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sale_number VARCHAR(50) UNIQUE NOT NULL,  -- Número de factura/ticket

  -- Customer info (básico, mejora con plugin Call)
  customer_id UUID,
  customer_name VARCHAR(255),

  -- Totals
  subtotal DECIMAL(10, 2) NOT NULL,
  tax DECIMAL(10, 2) DEFAULT 0,
  discount DECIMAL(10, 2) DEFAULT 0,
  total DECIMAL(10, 2) NOT NULL,

  -- Payment
  payment_method VARCHAR(50),             -- 'cash', 'card', 'transfer'
  payment_status VARCHAR(50) DEFAULT 'paid',

  -- Status
  status VARCHAR(50) DEFAULT 'completed', -- 'completed', 'cancelled', 'refunded'

  -- User who made the sale
  user_id UUID,

  -- Metadata
  metadata JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_sales_number ON tenant_abc123.sales(sale_number);
CREATE INDEX idx_sales_customer ON tenant_abc123.sales(customer_id);
CREATE INDEX idx_sales_status ON tenant_abc123.sales(status);
CREATE INDEX idx_sales_date ON tenant_abc123.sales(created_at);

-- Items de cada venta
CREATE TABLE tenant_abc123.sale_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sale_id UUID NOT NULL REFERENCES tenant_abc123.sales(id) ON DELETE CASCADE,
  product_id UUID NOT NULL REFERENCES tenant_abc123.products(id),

  -- Quantities and prices
  quantity INTEGER NOT NULL,
  unit_price DECIMAL(10, 2) NOT NULL,
  subtotal DECIMAL(10, 2) NOT NULL,
  tax DECIMAL(10, 2) DEFAULT 0,
  discount DECIMAL(10, 2) DEFAULT 0,

  -- Metadata
  metadata JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_sale_items_sale ON tenant_abc123.sale_items(sale_id);
CREATE INDEX idx_sale_items_product ON tenant_abc123.sale_items(product_id);

-- ========================================
-- PLUGIN: Buy
-- ========================================

CREATE TABLE tenant_abc123.suppliers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  contact_name VARCHAR(255),
  email VARCHAR(255),
  phone VARCHAR(50),
  address TEXT,
  tax_id VARCHAR(50),

  -- Status
  is_active BOOLEAN DEFAULT TRUE,

  -- Metadata
  metadata JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE tenant_abc123.purchases (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  purchase_number VARCHAR(50) UNIQUE NOT NULL,
  supplier_id UUID NOT NULL REFERENCES tenant_abc123.suppliers(id),

  -- Totals
  subtotal DECIMAL(10, 2) NOT NULL,
  tax DECIMAL(10, 2) DEFAULT 0,
  total DECIMAL(10, 2) NOT NULL,

  -- Status
  status VARCHAR(50) DEFAULT 'pending',   -- 'pending', 'completed', 'cancelled'

  -- Dates
  order_date DATE DEFAULT CURRENT_DATE,
  received_date DATE,

  -- User
  user_id UUID,

  -- Metadata
  metadata JSONB DEFAULT '{}',

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE tenant_abc123.purchase_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  purchase_id UUID NOT NULL REFERENCES tenant_abc123.purchases(id) ON DELETE CASCADE,
  product_id UUID NOT NULL REFERENCES tenant_abc123.products(id),

  quantity INTEGER NOT NULL,
  unit_cost DECIMAL(10, 2) NOT NULL,
  subtotal DECIMAL(10, 2) NOT NULL,

  created_at TIMESTAMP DEFAULT NOW()
);

-- Etc para otros plugins (Analytics, Call)...
```

---

## 🔐 Autenticación y Autorización

### JWT Strategy

```typescript
// src/core/auth/jwt.strategy.ts

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      secretOrKey: process.env.JWT_SECRET,
      ignoreExpiration: false,
    });
  }
  
  async validate(payload: JwtPayload) {
    return {
      userId: payload.sub,
      email: payload.email,
      tenantId: payload.tenantId,
      role: payload.role,
      permissions: payload.permissions,
    };
  }
}

// JWT Payload
interface JwtPayload {
  sub: string;        // User ID
  email: string;
  tenantId: string;
  role: string;
  permissions: string[];
  iat: number;
  exp: number;
}
```

---

## 🚀 Deployment e Infraestructura

### Docker Compose (Desarrollo)

```yaml
# docker-compose.yml

version: '3.8'

services:
  # PostgreSQL
  postgres:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: yerba
      POSTGRES_USER: yerba
      POSTGRES_PASSWORD: yerba_dev_password
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - yerba-network

  # Redis
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - yerba-network

  # RabbitMQ
  rabbitmq:
    image: rabbitmq:3-management-alpine
    ports:
      - "5672:5672"   # AMQP
      - "15672:15672" # Management UI
    environment:
      RABBITMQ_DEFAULT_USER: yerba
      RABBITMQ_DEFAULT_PASS: yerba_dev_password
    volumes:
      - rabbitmq_data:/var/lib/rabbitmq
    networks:
      - yerba-network

  # MinIO (S3-compatible)
  minio:
    image: minio/minio:latest
    command: server /data --console-address ":9001"
    ports:
      - "9000:9000"  # API
      - "9001:9001"  # Console
    environment:
      MINIO_ROOT_USER: yerba
      MINIO_ROOT_PASSWORD: yerba_dev_password
    volumes:
      - minio_data:/data
    networks:
      - yerba-network

  # Backend
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      NODE_ENV: development
      DATABASE_URL: postgresql://yerba:yerba_dev_password@postgres:5432/yerba
      REDIS_URL: redis://redis:6379
      RABBITMQ_URL: amqp://yerba:yerba_dev_password@rabbitmq:5672
      MINIO_ENDPOINT: minio
      MINIO_PORT: 9000
      MINIO_ACCESS_KEY: yerba
      MINIO_SECRET_KEY: yerba_dev_password
      JWT_SECRET: dev_jwt_secret_change_in_prod
    depends_on:
      - postgres
      - redis
      - rabbitmq
      - minio
    volumes:
      - ./backend:/app
      - /app/node_modules
    networks:
      - yerba-network

  # Frontend
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3001:3000"
    environment:
      NODE_ENV: development
      NEXT_PUBLIC_API_URL: http://localhost:3000
    depends_on:
      - backend
    volumes:
      - ./frontend:/app
      - /app/node_modules
      - /app/.next
    networks:
      - yerba-network

volumes:
  postgres_data:
  redis_data:
  rabbitmq_data:
  minio_data:

networks:
  yerba-network:
    driver: bridge
```

---

## 📈 Escalabilidad

### Estrategias de Escalado

#### 1. Horizontal Scaling (Backend)

```yaml
# HPA (Horizontal Pod Autoscaler)
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: yerba-backend-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: yerba-backend
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
```

#### 2. Database Read Replicas

```
┌──────────────┐
│   Primary    │───── Writes
│  PostgreSQL  │
└──────┬───────┘
       │
       │ Replication
       │
   ┌───┴────┬────────┐
   │        │        │
   ▼        ▼        ▼
┌──────┐ ┌──────┐ ┌──────┐
│Read  │ │Read  │ │Read  │
│Rep 1 │ │Rep 2 │ │Rep 3 │
└──────┘ └──────┘ └──────┘
```

---

## 📊 Monitoreo y Logging

### Métricas con Prometheus

```typescript
// src/shared/metrics/metrics.service.ts

import { register, Counter, Histogram, Gauge } from 'prom-client';

@Injectable()
export class MetricsService {
  // HTTP Requests
  private httpRequestsTotal = new Counter({
    name: 'http_requests_total',
    help: 'Total HTTP requests',
    labelNames: ['method', 'route', 'status'],
  });
  
  private httpRequestDuration = new Histogram({
    name: 'http_request_duration_seconds',
    help: 'HTTP request duration',
    labelNames: ['method', 'route'],
    buckets: [0.1, 0.5, 1, 2, 5],
  });
  
  // Events
  private eventsPublished = new Counter({
    name: 'events_published_total',
    help: 'Total events published',
    labelNames: ['event_type', 'tenant_id'],
  });
  
  // Methods
  recordRequest(method: string, route: string, status: number) {
    this.httpRequestsTotal.inc({ method, route, status });
  }
  
  getMetrics(): string {
    return register.metrics();
  }
}
```

---

## 🔒 Seguridad

### Checklist de Seguridad

#### 1. Authentication & Authorization
- ✅ JWT con expiración corta (1h)
- ✅ Refresh tokens con rotación
- ✅ RBAC (Role-Based Access Control)
- ✅ Permissions granulares por plugin
- ✅ 2FA opcional para admin

#### 2. Data Protection
- ✅ Encryption at rest (PostgreSQL + MinIO)
- ✅ Encryption in transit (TLS/HTTPS)
- ✅ Password hashing (bcrypt)
- ✅ Secrets management (Kubernetes Secrets)

#### 3. Input Validation
- ✅ DTO validation con class-validator
- ✅ SQL injection prevention (Prisma)
- ✅ XSS prevention (sanitization)
- ✅ CSRF tokens (frontend)

---

## 🛣️ Roadmap de Desarrollo

### Fase 1: MVP (Semanas 1-10)

**Objetivo:** Core funcional con 3 plugins básicos (Products, Stock, Sales)

**Semanas 1-2: Setup & Core**
- Setup monorepo (backend + frontend)
- Configurar Docker Compose
- Implementar Yerba Core con Plugin Manager
- Sistema de autenticación (JWT)
- Multitenancy básico (schema-per-tenant)
- Gestión de tenants

**Semanas 3-4: Event Bus & Plugin System**
- Integrar RabbitMQ
- Implementar Event Bus Service
- Plugin Registry con validación de dependencias
- Plugin Loader dinámico
- Sistema de activación/desactivación por tenant
- Manejo de Dead Letter Queues

**Semanas 5-6: Plugin Products (BASE)**
- CRUD completo de productos
- Sistema de categorías y etiquetas
- Gestión de SKU y códigos de barras
- Gestión de precios (venta y costo)
- Búsqueda y filtros
- Imágenes de productos (integración con MinIO)
- Eventos: `product.created`, `product.updated`, `product.deleted`, `product.priceChanged`
- API REST completa

**Semanas 7-8: Plugin Stock**
- Sistema de stock por producto (1:1 con Products)
- Gestión de múltiples depósitos
- Alertas de stock mínimo
- Historial de movimientos de stock
- Ajustes manuales de inventario
- Validación de dependencia con Products
- Eventos: `stock.updated`, `stock.low`, `stock.empty`
- Listeners de eventos de Products
- API REST completa

**Semanas 9-10: Plugin Sales + Frontend Básico**
- Sistema de ventas (POS)
- Registro de ventas con múltiples items
- Múltiples métodos de pago
- Validación de dependencias (Products + Stock)
- Reducción automática de stock via eventos
- Facturación básica / tickets
- Eventos: `sale.created`, `sale.cancelled`
- **Frontend básico:**
  - Login y autenticación
  - Dashboard principal
  - Módulo de productos (CRUD)
  - Módulo de stock (visualización y ajustes)
  - Módulo de ventas (POS básico)
  - Notificaciones en tiempo real (WebSocket)

---

### Fase 2: Productización (Semanas 11-18)

**Objetivo:** Sistema listo para primeros clientes con analytics y compras

**Semanas 11-12: Plugin Buy (Compras)**
- Gestión de proveedores
- Órdenes de compra
- Recepción de mercadería
- Integración con Stock (aumenta inventario)
- Validación de dependencias (Products + Stock)
- Eventos: `purchase.created`, `purchase.completed`, `purchase.cancelled`
- API REST completa
- Frontend: Módulo de compras

**Semanas 13-14: Plugin Analytics (Yerbera)**
- Dashboard de métricas generales
- Reportes de ventas (si Sales está activo)
- Reportes de compras (si Buy está activo)
- Análisis de inventario (si Stock está activo)
- Gráficos con Recharts
- Exportación a Excel/PDF
- Validación de dependencias con detección de features
- Frontend: Dashboard de analytics

**Semanas 15-16: Mejoras de UX y Onboarding**
- Wizard de onboarding para nuevos tenants
- Selección de plugins a activar
- Datos de ejemplo (seed data)
- Mejoras visuales y animaciones
- Dark mode refinado
- Tutoriales in-app

**Semanas 17-18: Infraestructura y Testing**
- Deploy a Kubernetes (staging)
- CI/CD completo con GitHub Actions
- Monitoreo (Prometheus + Grafana + Loki)
- Tests E2E (Playwright/Cypress)
- Tests de carga (k6)
- Documentación de API (Swagger)
- Deploy a producción
- Beta con primeros 3-5 clientes

---

### Fase 3: Expansión y Escalabilidad (Meses 5-7)

**Objetivo:** Nuevos plugins y mejoras de escalabilidad

**Mes 5: Plugin Call (CRM)**
- Gestión completa de clientes
- Historial de llamadas y comunicaciones
- Sistema de tickets de soporte
- Integración con Sales (historial de compras)
- Notas y seguimientos
- Validación de dependencias (Products, opcional Sales)

**Mes 6: Optimización y Escalabilidad**
- Read replicas para PostgreSQL
- Caching agresivo con Redis
- CDN para assets estáticos (CloudFlare/AWS CloudFront)
- Optimización de queries
- Índices avanzados en DB
- Compresión de assets frontend

**Mes 7: Features Empresariales**
- Multi-warehouse avanzado (Stock)
- Roles y permisos granulares
- Audit logs
- Reportes programados (Yerbera)
- Integración con e-commerce (API pública via Bombilla)
- Onboarding de 20-30 clientes adicionales

---

## 📞 Contacto

**Damian Pereyra**  
MateLab  
📧 info@matelab.com.uy  
📱 +598 91 670 863

---

**Última actualización:** 12 de Noviembre, 2025  
**Versión:** 1.0
