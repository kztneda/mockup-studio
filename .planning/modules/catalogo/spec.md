# Módulo: Catálogo de prendas

Proveedores, modelos de prenda, colores, grupos de talla, zonas y áreas de impresión, y escalones de precio de referencia.

## Entidades

### Proveedor (`proveedores`)
_alcance: global · borrado lógico · auditada_
Proveedor de prendas (M&O) o maquilador.

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| nombre | `string(120)` | requerido |  |
| tipo | `enum {PRENDAS, MAQUILA, AMBOS}` | requerido |  |
| plataforma | `enum {SHOPIFY, MANUAL}` |  | MANUAL |
| sitioWeb | `url` |  |  |
| contacto | `string(120)` |  |  |
| telefono | `phone` |  |  |
| email | `email` |  |  |
| notas | `text` |  |  |
| activo | `boolean` |  | true |
| ultimaActividadId | `uuid` |  |  |

### ModeloPrenda (`modelos_prenda`)
_alcance: global · borrado lógico · auditada_
Modelo del proveedor (4800, 3320, 5542, 6500, 7810) o prenda genérica.

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| proveedorId | `uuid` | requerido |  |
| codigo | `string(30)` | requerido |  |
| nombre | `string(150)` | requerido |  |
| categoria | `enum {PLAYERA, PLAYERA_VINTAGE, RAGLAN, HOODIE, SUDADERA, SHORT, PANTS, GORRA, TOTE, OTRA}` | requerido |  |
| corte | `enum {REGULAR, OVERSIZE, SLIM, BOXY}` |  | REGULAR |
| gramaje | `smallint` |  |  |
| composicion | `string(150)` |  |  |
| tallasDisponibles | `array` |  |  |
| urlProducto | `url` |  |  |
| handleTienda | `string(200)` |  |  |
| precioReferencia | `money` |  |  |
| imagenReferencia | `image` |  |  |
| descripcion | `text` |  |  |
| activo | `boolean` |  | true |
| sincronizadoEn | `datetime` |  |  |
| ultimaActividadId | `uuid` |  |  |

Índices compuestos: `(proveedorId, codigo)` único

### ColorPrenda (`colores_prenda`)
_alcance: global_
Color disponible de un modelo.

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| modeloPrendaId | `uuid` | requerido |  |
| nombre | `string(80)` | requerido |  |
| codigoProveedor | `string(80)` |  |  |
| hex | `color` | requerido |  |
| hexAjustadoManual | `boolean` |  | false |
| esJaspeado | `boolean` |  | false |
| tono | `enum {CLARO, OSCURO}` |  | CLARO |
| composicion | `string(120)` |  |  |
| imagenFrente | `image` |  |  |
| imagenEspalda | `image` |  |  |
| disponible | `boolean` |  | true |
| existencias | `int` |  |  |
| orden | `smallint` |  | 0 |
| ultimaActividadId | `uuid` |  |  |

Índices compuestos: `(modeloPrendaId, nombre)` único

### GrupoTalla (`grupos_talla`)
_alcance: global_
Agrupa tallas que comparten tamaño de arte (XS-M y L-XL).

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| nombre | `string(40)` | requerido, único |  |
| tallas | `array` | requerido |  |
| orden | `smallint` |  | 0 |
| activo | `boolean` |  | true |
| ultimaActividadId | `uuid` |  |  |

### EscalonPrecioProveedor (`escalones_precio_proveedor`)
_alcance: global_
Precio por volumen del proveedor de prendas (referencia).

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| modeloPrendaId | `uuid` | requerido |  |
| cantidadMin | `int` | requerido, mín 1 |  |
| cantidadMax | `int` |  |  |
| precioUnitario | `money` | requerido, mín 0 |  |
| ultimaActividadId | `uuid` |  |  |

### ZonaImpresion (`zonas_impresion`)
_alcance: global_
Zona imprimible de un modelo.

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| modeloPrendaId | `uuid` | requerido |  |
| codigo | `enum {FRENTE, ESPALDA, MANGA_IZQUIERDA, MANGA_DERECHA, CUELLO_EXTERIOR, ETIQUETA_INTERNA, BOLSILLO, CAPUCHA, PIERNA_IZQUIERDA, PIERNA_DERECHA, OTRA}` | requerido |  |
| nombre | `string(80)` | requerido |  |
| vista | `enum {FRENTE, ESPALDA, IZQUIERDA, DERECHA}` | requerido |  |
| orden | `smallint` |  | 0 |
| activa | `boolean` |  | true |
| ultimaActividadId | `uuid` |  |  |

Índices compuestos: `(modeloPrendaId, codigo)` único

### AreaImpresion (`areas_impresion`)
_alcance: global_
Medidas máximas por zona y grupo de talla.

| Campo | Tipo | Reglas | Por defecto |
| --- | --- | --- | --- |
| zonaImpresionId | `uuid` | requerido |  |
| grupoTallaId | `uuid` | requerido |  |
| anchoMaxCm | `decimal(6,2)` |  | 40 |
| altoMaxCm | `decimal(6,2)` |  | 50 |
| distanciaCuelloCm | `decimal(5,2)` |  | 7 |
| ultimaActividadId | `uuid` |  |  |

Índices compuestos: `(zonaImpresionId, grupoTallaId)` único

## Relaciones

- Proveedor.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- ModeloPrenda.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- ModeloPrenda.proveedorId → `ManyToOne` → Proveedor. (proveedor)
- ColorPrenda.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- ColorPrenda.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- GrupoTalla.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- EscalonPrecioProveedor.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- EscalonPrecioProveedor.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- ZonaImpresion.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- ZonaImpresion.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- AreaImpresion.ultimaActividadId → `ManyToOne` → Actividad. (ultimaActividad)
- AreaImpresion.zonaImpresionId → `ManyToOne` → ZonaImpresion. (zona)
- AreaImpresion.grupoTallaId → `ManyToOne` → GrupoTalla. (grupoTalla)
- BaseMockup.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- BaseMockup.colorPrendaId → `ManyToOne` → ColorPrenda. (colorFijo)
- ZonaBase.zonaImpresionId → `ManyToOne` → ZonaImpresion. (zona)
- Composicion.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- CapaComposicion.zonaImpresionId → `ManyToOne` → ZonaImpresion. (zona)
- CapaComposicion.grupoTallaBaseId → `ManyToOne` → GrupoTalla. (grupoTallaBase)
- LoteItem.colorPrendaId → `ManyToOne` → ColorPrenda. (color)
- ArchivoProduccion.zonaImpresionId → `ManyToOne` → ZonaImpresion. (zona)
- ArchivoProduccion.grupoTallaId → `ManyToOne` → GrupoTalla. (grupoTalla)
- TarifaMaquila.proveedorId → `ManyToOne` → Proveedor. (maquilador)
- TarifaMaquila.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- CostoAdicional.proveedorId → `ManyToOne` → Proveedor. (proveedor)
- CotizacionCosto.proveedorId → `ManyToOne` → Proveedor. (maquilador)
- CotizacionPartida.colorPrendaId → `ManyToOne` → ColorPrenda. (color)
- CotizacionPartida.grupoTallaId → `ManyToOne` → GrupoTalla. (grupoTalla)
- Modelo3d.modeloPrendaId → `ManyToOne` → ModeloPrenda. (modelo)
- PiezaPatron.zonaImpresionId → `ManyToOne` → ZonaImpresion. (zona)

## API

| Método | Ruta | Auth | Roles | Descripción |
| --- | --- | --- | --- | --- |
| `GET` | `/api/proveedores` | sí |  |  |
| `POST` | `/api/proveedores` | sí |  |  |
| `PUT` | `/api/proveedores/{id}` | sí |  |  |
| `DELETE` | `/api/proveedores/{id}` | sí |  |  |
| `GET` | `/api/modelos` | sí |  |  |
| `GET` | `/api/modelos/{id}` | sí |  | Incluye colores, zonas, áreas y escalones |
| `POST` | `/api/modelos` | sí |  |  |
| `POST` | `/api/modelos/importar-url` | sí |  | Recibe URL de producto de Shopify y crea modelo con colores |
| `PUT` | `/api/modelos/{id}` | sí |  |  |
| `POST` | `/api/modelos/{id}/sincronizar` | sí |  |  |
| `POST` | `/api/proveedores/{id}/sincronizar` | sí |  |  |
| `PUT` | `/api/colores/{id}` | sí |  |  |
| `PUT` | `/api/modelos/{id}/zonas` | sí |  |  |
| `PUT` | `/api/modelos/{id}/escalones` | sí |  |  |
| `GET` | `/api/grupos-talla` | sí |  |  |
| `PUT` | `/api/grupos-talla` | sí |  |  |

## Pantallas

| Pantalla | Tipo | Ruta | Entidad | Roles |
| --- | --- | --- | --- | --- |
| Proveedores | List | `/catalogo/proveedores` | Proveedor |  |
| Proveedor | Form | `/catalogo/proveedores/:id` | Proveedor |  |
| Modelos de prenda | List | `/catalogo/modelos` | ModeloPrenda |  |
| Modelo de prenda | Detail | `/catalogo/modelos/:id` | ModeloPrenda |  |
| Grupos de talla | Settings | `/catalogo/grupos-talla` | GrupoTalla |  |

## Workflows

### Sincronizar modelo con M&O
Actualiza colores, tallas, existencias, imágenes y precio base desde Shopify.
Se dispara con: `catalogo.sincronizacion-programada`

1. [trigger] Programado o manual
2. [webhook] Leer producto
3. [loop] Por cada variante
4. [action] Actualizar colores y existencias
5. [action] Descargar imágenes nuevas
6. [condition] ¿Cambió el precio base?
7. [notification] Avisar cambio de precio
8. [end] Fin

## Eventos

| Evento | Se emite cuando | Payload |
| --- | --- | --- |
| `modelo-prenda.sincronizado` | manual |  |
| `color-prenda.agotado` | on_update |  |

## Reportes

| Reporte | Entidad | Columnas | Filtros |
| --- | --- | --- | --- |
| Colores por modelo | ColorPrenda | nombre, hex, tono, esJaspeado, existencias, disponible | modeloPrendaId, tono, disponible |
| Áreas de impresión | AreaImpresion | zonaImpresionId, grupoTallaId, anchoMaxCm, altoMaxCm | grupoTallaId |

## Criterios de aceptación

- [ ] CRUD de Proveedor con validación de campos requeridos y únicos.
- [ ] Proveedor: el borrado es lógico (`deleted_at`) y las consultas excluyen lo borrado.
- [ ] Proveedor: cada cambio registra quién, qué y cuándo.
- [ ] CRUD de ModeloPrenda con validación de campos requeridos y únicos.
- [ ] ModeloPrenda: el borrado es lógico (`deleted_at`) y las consultas excluyen lo borrado.
- [ ] ModeloPrenda: cada cambio registra quién, qué y cuándo.
- [ ] CRUD de ColorPrenda con validación de campos requeridos y únicos.
- [ ] CRUD de GrupoTalla con validación de campos requeridos y únicos.
- [ ] CRUD de EscalonPrecioProveedor con validación de campos requeridos y únicos.
- [ ] CRUD de ZonaImpresion con validación de campos requeridos y únicos.
- [ ] CRUD de AreaImpresion con validación de campos requeridos y únicos.
- [ ] Todas las rutas del apartado API existen con el método y la autenticación indicados.
- [ ] Cada pantalla respeta los roles requeridos y define estados de carga, vacío y error.
- [ ] Workflow "Sincronizar modelo con M&O": probar cada transición y los casos de rechazo.
- [ ] Los eventos se emiten con el payload indicado, de forma idempotente.
- [ ] Tests del módulo y type-check sin errores.

## Dónde trabajar
- Web: `apps/web/src/features/catalogo/`
