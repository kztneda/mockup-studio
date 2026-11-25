# Mockup Studio · SaaS Pack v2.0.0

Definición completa de la plataforma en YAML, dividida por archivos para que personas e IAs la lean y editen por partes.
Para trabajar con una IA: dale este README y CATALOG.md, y solo los archivos del módulo en curso.

Contenido: `project.yaml`, `infrastructure.yaml`, `ui-design.yaml`, `roles.yaml`, `integrations.yaml`, `relations.yaml`, `modules/sistema.yaml`, `modules/ia.yaml`, `modules/catalogo.yaml`, `modules/bases.yaml`, `modules/disenos.yaml`, `modules/mockups.yaml`, `modules/produccion.yaml`, `modules/costos.yaml`, `modules/modelos-3d.yaml`.

## Archivos

| Archivo | kind | Contenido |
| --- | --- | --- |
| `project.yaml` | `project` | Proyecto, multi-tenant, seguridad, billing (planes), políticas, eventos globales y widgets del dashboard. **Obligatorio.** |
| `infrastructure.yaml` | `infrastructure` | `platform` (web/móvil/desktop), `stack` (frontend, backend, apiStyle, database, orm, cache, messageBroker, storage, search, realtime) e `infrastructure` (hosting, containerization, iac, observability, cicd). |
| `ui-design.yaml` | `ui-design` | Librería de componentes, colores, tipografía, layout, forma y branding. |
| `roles.yaml` | `roles` | Roles con sus permisos anidados. |
| `integrations.yaml` | `integrations` | Servicios de terceros (`provider`, `enabled`, `config`). |
| `relations.yaml` | `relations` | Relaciones entre entidades (cruzan módulos). |
| `modules/<slug>.yaml` | `module` | Un módulo: `entities`, `screens`, `apis`, `workflows`, `events` y `reports`. |
| `CATALOG.md` | — | Todos los valores válidos de cada enum con su descripción. |
| `schema/<kind>.schema.json` | — | JSON Schema de cada archivo (autocompletado y validación en el editor). |

Todos los YAML empiezan con `kind`. Por eso el pack también puede viajar como **un solo texto YAML** con los documentos separados por `---`: el import de SaaS Architect acepta el zip, los archivos sueltos o ese texto pegado.

## Referencias (slugs)

No hay ids aleatorios: todo se referencia por **slug** (minúsculas, números y guiones).

| Qué | Formato | Ejemplo | Dónde se usa |
| --- | --- | --- | --- |
| Módulo | `<modulo>` | `ventas` | `slug` del módulo; `resource` de un permiso |
| Entidad | `<modulo>.<entidad>` | `ventas.factura` | `relations[].source/target`, `screens[].entity`, `reports[].entity`, `resource` de un permiso |
| Rol | `<rol>` | `gerente-ventas` | `requiredRoles`, `apis[].roles`, `stateMachine.transitions[].roles` |
| Nodo de workflow | `key` local | `aprobar` | `workflows[].edges[].from/to` |

- El `slug` se puede omitir: se deriva del `name` ("Órdenes de Compra" → `ordenes-de-compra`, "CompanyMember" → `company-member`).
- Dentro de un módulo, una entidad propia se puede citar solo como `<entidad>`.
- Los campos se citan por `name` (`sourceField`, `targetField`, `indexes[].fields`, `reports[].columns`, `stateMachine.field`).

## Convenciones

- **Nombres:** entidades en PascalCase singular (`Factura`), campos en camelCase (`fechaEmision`), `tableName` en snake_case plural (`facturas`).
- **Campos automáticos:** no declares `id`, `createdAt`, `updatedAt` ni `deletedAt`; se generan (`deletedAt` solo con `softDelete: true`). Con `scope: tenant` se agrega la llave del tenant si falta; si la usas en un índice, declárala como campo (`workspaceId`, `organizationId`… de tipo `uuid`) y úsala con el mismo nombre en todas las entidades del proyecto.
- **Llaves foráneas:** campo `<entidad>Id` de tipo `uuid` + una relación en `relations.yaml` (`ManyToOne` desde la entidad que guarda la llave).
- **Tipos semánticos:** prefiere `email`, `phone`, `money`, `url`, `image`… sobre `string`/`decimal`: comunican validación y se almacenan con su tipo base.
- **Estados:** campo `enum` cuyos `enumValues` son los estados en MAYÚSCULAS + `stateMachine` **completa**: `field`, `initial`, `states` (lista de `{ name, label?, isFinal? }`, uno por valor del enum) y `transitions`. En cada transición `from` es una **lista** aunque sea un solo estado (`from: [BORRADOR]`), `action` es el comando que la dispara (`confirmar`) y `event` el evento que emite (`factura.pagada`).
- **Textos obligatorios:** toda pantalla lleva `menuLabel` y todo paso de workflow lleva `label`, aunque repitan el `name`. Los `defaultValue` son siempre texto entre comillas (`"false"`, `"0"`, `"BORRADOR"`), nunca números ni booleanos sueltos.
- **Reportes:** `filters` son solo los nombres de los campos por los que se puede filtrar; una condición fija con valor va en `conditions: [{ field: status, operator: eq, value: CONFIRMADA }]`.
- **Diagramas de workflow:** da `key` a los pasos y únelos con `edges: [{ from: inicio, to: cobro, label: "sí" }]`; los nodos del diagrama se arman solos a partir de los pasos.
- **Eventos:** `name` como `entidad.accion` en pasado (`order.paid`), `trigger` y `action` del catálogo.
- **Valores por defecto:** las claves que se omiten toman el valor por defecto del schema (`isRequired: false`, `isNullable: true`, `auth: true`, `enabled: true`…).
- **Fuera del catálogo:** si una tecnología o tipo no existe, usa `custom:<valor>` en los enums que lo permiten (ver CATALOG.md). El import lo acepta y lo informa.
- **Solo claves de la referencia:** usa únicamente las claves de "Campos de cada documento" (más abajo) y respeta el tipo: números sin comillas, `true`/`false` sin comillas, listas como `[a, b]`. No inventes claves ni cambies sus nombres (`title`, no `name`, en los widgets; `mobileTech`, no `mobile`).
- **Límites de plan:** números; `-1` significa sin límite (no escribas `unlimited`). Un precio a la medida es `price: 0` con `contactSales: true`. Para precio mensual y anual del mismo plan declara dos planes.
- **Comillas:** escribe en bloques YAML (una clave por línea) o, en mapas `{ }`, pon entre comillas dobles todo texto con comas, dos puntos, `#` o corchetes. Una coma sin comillas dentro de `{ }` parte el texto en claves falsas.
- **Lo que no tiene campo:** decisiones y reglas de negocio van en `policies` (nombre + descripción); datos técnicos sueltos, en `extensions` del documento (clave = ruta con puntos). Se conservan al importar y exportar.
- **Entrega por partes:** el documento `project` puede traer permisos o pantallas que apuntan a módulos que llegan después; al importar todo junto se resuelven.

## Ejemplo mínimo

```yaml
kind: project
project: { name: Facturador, saasType: B2B, currency: MXN }
multiTenant: { enabled: true }
---
kind: infrastructure
platform: { targets: [web] }
stack: { frontend: [nextjs], backend: [nestjs], database: [mysql], orm: [prisma] }
---
kind: roles
roles:
  - slug: admin
    name: Administrador
    isSystem: true
    permissions:
      - { resource: ventas, actions: [manage] }
---
kind: module
slug: ventas
name: Ventas
entities:
  - name: Factura
    tableName: facturas
    scope: tenant
    fields:
      - { name: folio, type: string, maxLength: 20, isRequired: true, isUnique: true }
      - { name: total, type: money, isRequired: true }
      - { name: status, type: enum, enumValues: [BORRADOR, TIMBRADA, CANCELADA], defaultValue: "BORRADOR" }
    stateMachine:
      field: status
      initial: BORRADOR
      states:
        - { name: BORRADOR, label: Borrador }
        - { name: TIMBRADA, label: Timbrada }
        - { name: CANCELADA, label: Cancelada, isFinal: true }
      transitions:
        - { from: [BORRADOR], to: TIMBRADA, action: timbrar, event: factura.timbrada, roles: [admin] }
        - { from: [BORRADOR, TIMBRADA], to: CANCELADA, action: cancelar, event: factura.cancelada, roles: [admin] }
screens:
  - { name: Facturas, type: List, route: /ventas/facturas, menuLabel: Facturas, entity: ventas.factura }
apis:
  - { method: GET, path: /facturas, name: Listar facturas, entity: ventas.factura }
reports:
  - { name: Facturas timbradas, entity: ventas.factura, columns: [folio, total], filters: [status], conditions: [{ field: status, operator: eq, value: TIMBRADA }] }
```

## Validar

Importa el pack en SaaS Architect (Proyectos → Importar): los errores indican archivo, línea y ruta (`modules/ventas.yaml › entities[0].fields[2].type`). Las advertencias (claves desconocidas, referencias a roles inexistentes, incompatibilidades de stack) no bloquean el import.

## Campos de cada documento

Solo estas claves son válidas. `[Nombre]` es una lista de valores del catálogo (ver CATALOG.md); `key[]` es una lista de objetos con los campos indicados debajo; `# requerido` marca lo obligatorio y el resto es opcional.

### kind: project

```
extensions: mapa libre  # Datos sin campo propio, por ruta con puntos ("project.appUrl": …); se conservan sin afectar al modelo
schemaVersion: texto  # por defecto "2.0.0"
project: objeto  # requerido
  name: texto  # requerido
  slug: texto  # Identificador corto en minúsculas (repositorio, paquetes, subdominio)
  tagline: texto
  description: texto  # por defecto ""
  version: texto  # por defecto "1.0.0"
  language: texto  # por defecto "es"
  languages: [texto]
  timezone: texto  # por defecto "America/Mexico_City"
  currency: texto  # por defecto "MXN"
  supportedCurrencies: [texto]
  domain: texto
  saasType: SaaSType  # por defecto "B2B"
  logoUrl: valor
  primaryColor: texto  # por defecto "#1976d2"
multiTenant: objeto
  enabled: true/false  # por defecto false
  strategy: MultiTenantStrategy  # por defecto "shared"
  subdomain: true/false  # por defecto false
  customDomain: true/false  # por defecto false
  isolationLevel: IsolationLevel  # por defecto "row"
security: objeto
  auth: objeto
    providers: [AuthProvider]
    mfa: true/false  # por defecto false
    sessionTimeout: entero  # por defecto 3600
    jwtExpiry: entero  # por defecto 86400
    oauthConfigs: mapa de objeto
  encryption: objeto
    atRest: true/false  # por defecto true
    inTransit: true/false  # por defecto true; true o false (la versión de TLS va en extensions o en policies)
    algorithm: texto  # por defecto "AES-256"
  audit: objeto
    enabled: true/false  # por defecto true
    retention: entero  # por defecto 90
  rateLimit: objeto
    enabled: true/false  # por defecto true
    requestsPerMinute: entero  # por defecto 60
billing: objeto
  provider: BillingProvider  # por defecto "stripe"
  trialDays: entero  # por defecto 14
  currency: texto  # por defecto "MXN"
  plans[]: lista de objetos
    slug: texto
    name: texto  # requerido
    price: número  # requerido
    currency: texto
    contactSales: true/false  # true si el precio se cotiza con ventas (price: 0)
    interval: BillingInterval  # requerido
    features: [texto]
    limits: mapa de número  # Límites del plan por clave; números, -1 = sin límite (no escribas "unlimited")
    isPopular: true/false  # por defecto false
policies[]: lista de objetos
  name: texto  # requerido
  description: texto  # por defecto ""
  claims: [texto]
  conditions: texto
events[]: lista de objetos
  name: texto  # requerido
  description: texto  # por defecto ""
  trigger: EventTrigger  # requerido
  action: EventAction
  payload: texto  # por defecto ""
  entity: texto
dashboards[]: lista de objetos
  type: WidgetType  # requerido
  title: texto  # requerido
  dataSource: texto  # por defecto ""
  config: mapa libre  # Parámetros del widget: entity, metric (count|sum|avg), field, groupBy, filter, dateField, interval, sort, limit, target…
  position: objeto
    x: número  # requerido
    y: número  # requerido
    w: número  # requerido
    h: número  # requerido
```

### kind: infrastructure

```
extensions: mapa libre  # Datos sin campo propio, por ruta con puntos ("project.appUrl": …); se conservan sin afectar al modelo
platform: objeto
  targets: [AppPlatform]
  mobileTech: MobileTech
  desktopTech: DesktopTech
stack: objeto
  frontend: [FrontendTech]
  backend: [BackendTech]
  apiStyle: [ApiStyle]
  database: [DatabaseTech]
  orm: [OrmTech]
  cache: [CacheTech]
  messageBroker: [BrokerTech]
  storage: [StorageTech]
  search: [SearchTech]
  realtime: [RealtimeTech]
infrastructure: objeto
  hosting: [HostingTech]
  containerization: [ContainerTech]
  iac: [IacTech]
  observability: [ObservabilityTech]
  cicd: [CicdTech]
```

### kind: ui-design

```
componentLibrary: UIComponentLibrary  # por defecto "material-ui"
defaultThemeMode: ThemeMode  # por defecto "light"
generalInstructions: texto
colors: objeto
  primary: texto  # por defecto "#1976d2"
  secondary: texto  # por defecto "#9c27b0"
  accent: texto  # por defecto "#ff9800"
  error: texto  # por defecto "#d32f2f"
  warning: texto  # por defecto "#ed6c02"
  success: texto  # por defecto "#2e7d32"
  info: texto  # por defecto "#0288d1"
  backgroundDefault: texto  # por defecto "#f5f5f5"
  backgroundPaper: texto  # por defecto "#ffffff"
  textPrimary: texto  # por defecto "#212121"
  textSecondary: texto  # por defecto "#757575"
typography: objeto
  fontFamily: UIFontFamily  # por defecto "inter"
  customFontFamily: texto
  customFontUrl: texto
  baseFontSizePx: número  # por defecto 14
  headingFontFamily: UIFontFamily
  lineHeight: número  # por defecto 1.5
  letterSpacing: LetterSpacing  # por defecto "normal"
layout: objeto
  navType: NavLayoutType  # por defecto "sidebar-left"
  sidebarWidthPx: número  # por defecto 240
  contentMaxWidthPx: número  # por defecto 0
  density: DesignDensity  # por defecto "comfortable"
  topbarHeightPx: número  # por defecto 64
  footerEnabled: true/false  # por defecto false
  breadcrumbsEnabled: true/false  # por defecto true
shape: objeto
  borderRadiusPreset: BorderRadiusPreset  # por defecto "rounded"
  customBorderRadiusPx: número
  buttonStyle: ButtonStyle  # por defecto "filled"
  inputStyle: InputStyle  # por defecto "outlined"
  elevationStyle: ElevationStyle  # por defecto "shadow"
branding: objeto
  logoUrl: texto
  faviconUrl: texto
  brandName: texto
  brandTagline: texto
  loginBackground: texto
  splashScreenEnabled: true/false  # por defecto false
animationsEnabled: true/false  # por defecto true
rtlSupport: true/false  # por defecto false
accessibilityLevel: AccessibilityLevel  # por defecto "AA"
customCss: texto
designNotes: texto
extensions: mapa libre  # Datos sin campo propio, por ruta con puntos ("project.appUrl": …); se conservan sin afectar al modelo
```

### kind: roles

```
roles[]: lista de objetos
  slug: texto
  name: texto  # requerido
  description: texto  # por defecto ""
  isSystem: true/false  # por defecto false
  scope: texto  # global = rol de la plataforma, fuera de cualquier tenant; tenant = rol dentro de un tenant
  color: texto  # por defecto "#9c27b0"
  permissions[]: lista de objetos
    resource: texto  # requerido; "<modulo>" o "<modulo>.<entidad>"
    actions: [PermissionAction]
```

### kind: integrations

```
integrations[]: lista de objetos
  provider: IntegrationProvider  # requerido
  enabled: true/false  # por defecto true
  config: mapa de texto  # Claves de configuración del proveedor; todos los valores son texto (variables como "${STRIPE_SECRET_KEY}", números y booleanos entre comillas)
```

### kind: relations

```
relations[]: lista de objetos
  type: RelationType  # requerido
  sourceField: texto  # por defecto ""
  targetField: texto  # por defecto ""
  label: texto
  source: texto  # requerido
  target: texto  # requerido
```

### kind: module

```
slug: texto
name: texto  # requerido
description: texto  # por defecto ""
icon: texto  # por defecto "Folder"
color: texto  # por defecto "#1976d2"
order: número  # por defecto 0
isCore: true/false  # por defecto false
phase: entero
entities[]: lista de objetos
  slug: texto
  name: texto  # requerido
  description: texto  # por defecto ""
  icon: texto  # por defecto "TableChart"
  tableName: texto  # requerido
  position: objeto
    x: número  # requerido
    y: número  # requerido
  scope: EntityScope
  softDelete: true/false
  audited: true/false
  indexes[]: lista de objetos
    fields: [texto]  # requerido
    unique: true/false  # por defecto false
  fields[]: lista de objetos
    name: texto  # requerido
    type: FieldType  # requerido
    description: texto
    isRequired: true/false  # por defecto false
    isNullable: true/false  # por defecto true
    defaultValue: texto  # Siempre texto, entre comillas: "false", "0", "BORRADOR"
    maxLength: número
    precision: número  # Dígitos totales de un decimal
    scale: entero  # Dígitos decimales de un decimal (2 por defecto)
    isIndexed: true/false  # por defecto false
    isUnique: true/false  # por defecto false
    enumValues: [texto]
    validation: objeto
      min: número
      max: número
      pattern: texto
    sensitivity: FieldSensitivity
  stateMachine: objeto
    field: texto  # requerido
    initial: texto  # requerido
    states[]: lista de objetos  # requerido
      name: texto  # requerido
      label: texto
      isFinal: true/false
    transitions[]: lista de objetos
      from: [texto]  # requerido; Lista de estados de origen: [BORRADOR] (aunque sea uno solo)
      to: texto  # requerido
      action: texto  # Comando que dispara la transición (confirmar, cancelar)
      event: texto
      roles: [texto]
      guard: texto
      description: texto
screens[]: lista de objetos
  name: texto  # requerido
  type: ScreenType  # requerido
  route: texto  # requerido
  menuLabel: texto  # requerido
  menuIcon: texto  # por defecto "Article"
  requiredRoles: [texto]
  auth: true/false  # false = pantalla pública, sin sesión (por defecto true)
  entity: texto
apis[]: lista de objetos
  name: texto  # Nombre corto de la operación ("Crear evento")
  controller: texto
  method: HttpMethod  # requerido
  path: texto  # requerido
  description: texto  # por defecto ""
  requestSchema: mapa libre
  responseSchema: mapa libre
  auth: true/false  # por defecto true
  roles: [texto]
  tags: [texto]
  entity: texto  # Entidad principal: "<modulo>.<entidad>" (o solo "<entidad>" dentro de su módulo)
workflows[]: lista de objetos
  name: texto  # requerido
  description: texto  # por defecto ""
  trigger: texto
  steps[]: lista de objetos
    type: WorkflowStepType  # requerido
    label: texto  # requerido
    description: texto
    config: mapa libre
    key: texto  # Identificador del paso para unirlo en edges; con key y edges el diagrama se arma solo
  nodes[]: lista de objetos
    type: WorkflowNodeType  # requerido
    label: texto  # requerido
    position: objeto
      x: número  # requerido
      y: número  # requerido
    config: mapa libre
    key: texto  # requerido
  edges[]: lista de objetos
    from: texto  # requerido
    to: texto  # requerido
    label: texto
events[]: lista de objetos
  name: texto  # requerido
  description: texto  # por defecto ""
  trigger: EventTrigger  # requerido
  action: EventAction
  payload: texto  # por defecto ""
  entity: texto
reports[]: lista de objetos
  name: texto  # requerido
  description: texto  # por defecto ""
  columns: [texto]
  filters: [texto]  # Nombres de los campos por los que la persona puede filtrar (solo nombres)
  conditions[]: lista de objetos  # Condiciones fijas que el reporte siempre aplica: { field: status, operator: eq, value: CONFIRMADA }
    field: texto  # requerido
    operator: texto  # eq, neq, lt, lte, gt, gte, in, contains…
    value: valor
  entity: texto  # requerido
```
