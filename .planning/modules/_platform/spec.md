# Plataforma (transversal)

## Roles
| Rol | Descripción | Sistema |
| --- | --- | --- |
| Propietario | Único usuario de la instalación local; acceso total. | sí |

## Políticas
| Política | Claims | Condición |
| --- | --- | --- |
| Usuario único y solo localhost |  |  |
| Tabla Actividades |  |  |
| IdUltimaActividad en todas las tablas |  |  |
| Modelos alineados C# y TypeScript |  |  |
| Claves de API cifradas |  |  |
| IA opcional con aprobación |  |  |
| Reparto de proveedores de IA |  |  |
| Pipeline local determinista |  |  |
| Licencias de modelos locales |  |  |
| Recoloreo de prendas |  |  |
| Motor de render único |  |  |
| Grupos de talla y escalado del arte |  |  |
| Área de impresión configurable |  |  |
| Archivos de producción |  |  |
| Fórmula de costo con maquila |  |  |
| Resolución de tarifa de maquila |  |  |
| Cotización congelada |  |  |
| Sincronización con M&O |  |  |
| Almacenamiento local |  |  |
| Respaldo al homelab |  |  |
| Eliminación lógica |  |  |
| Logging |  |  |
| Nomenclatura de exportación |  |  |
| Instalación y actualizaciones |  |  |

## Multitenant
Desactivado.

## Seguridad
- Proveedores de autenticación: custom:sin-autenticacion-localhost
- Sesión: 3600s · token de acceso: 86400s
- Cifrado en reposo: sí · en tránsito: no (DPAPI de Windows (solo claves de API))
- Límite de peticiones: desactivado
- Auditoría: activa, 730 días

## Billing
Proveedor none · moneda MXN · prueba 0 días.

- El webhook del proveedor es la fuente de verdad del estado de pago; guardar el id de cada evento para ignorar duplicados.
- Aplicar los límites del plan en el servidor, no solo en la interfaz.

## Integraciones activas
- anthropic
- google-gemini
- custom:moplayeras-shopify
- custom:onnx-birefnet
- custom:velopack
- custom:respaldo-homelab

## Infraestructura
- Hosting / nube: On-premise
- Contenedores y orquestación: sin definir
- Infraestructura como código: sin definir
- Observabilidad: serilog-archivo
- CI/CD: GitHub Actions

## Eventos globales
| Evento | Se emite cuando | Payload |
| --- | --- | --- |
| `respaldo.programado` | scheduled |  |
| `catalogo.sincronizacion-programada` | scheduled |  |
