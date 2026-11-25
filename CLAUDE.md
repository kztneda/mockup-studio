# Mockup Studio

Aplicación de escritorio local (Windows) para generar mockups 2D y 3D de prendas a partir de bases propias o del proveedor, aplicar diseños de Illustrator, simular técnica y acabado, generar lotes, archivos de producción por grupo de talla y calcular el costo de producción por pieza con maquila.

Tipo Internal · idioma `es` · moneda MXN · zona America/Mexico_City (en base de datos todo va en UTC).

## Stack
- Plataformas objetivo: Desktop
- Framework desktop: WPF
- Frontend web: React (SPA con Vite)
- Backend: .NET (ASP.NET Core)
- Estilo de API: REST
- Base de datos: SQLite
- ORM / acceso a datos: Entity Framework Core
- Cache: Cache en proceso
- Mensajería y colas: Cola en base de datos
- Almacenamiento de archivos: Disco local
- Búsqueda: Full-text de la base de datos
- Tiempo real: SignalR

## Reglas
- Monorepo con tipos y esquemas de validación compartidos; no duplicar modelos entre apps.
- Toda tabla incluye `id`, `created_at` y `updated_at` (y `deleted_at` si tiene borrado lógico); no se declaran como campos del spec.
- Código en camelCase; tablas y columnas en snake_case; JSON de la API en snake_case.
- Llaves foráneas reales por cada relación (restrict al borrar). Entidades con borrado lógico usan `deleted_at` y toda consulta lo filtra.
- Autenticación: custom:sin-autenticacion-localhost. Nunca guardar secretos en el repositorio.
- Auditoría activa (retención 730 días): registrar quién, qué y cuándo.
- Permisos: el de una entidad reemplaza al de su módulo para ese rol; sin permiso explícito, el rol no puede.
- No inventes entidades, campos ni rutas que no estén en el spec del módulo; si falta algo, pregunta.

## Comandos
- `pnpm install` · `pnpm dev` · `pnpm test` · `pnpm type-check` · `pnpm build`
- `dotnet build` · `dotnet test`

## Cómo trabajar
1. Lee `.planning/roadmap.md` y toma el siguiente módulo pendiente.
2. Lee solo `.planning/modules/<módulo>/spec.md` de ese módulo (y `.planning/modules/_platform/spec.md` si tocas billing, seguridad o tenants).
3. Orden: migración → entidad y repositorio → servicio → endpoints → pantallas → tests.
4. Cumple los criterios de aceptación del spec y corre los tests y el type-check antes de pasar al siguiente módulo.

## Módulos (en orden de construcción)
- `sistema` — Bitácora de actividades, marcas, parámetros, cola de trabajos en segundo plano y respaldos. (5 entidades)
- `catalogo` — Proveedores, modelos de prenda, colores, grupos de talla, zonas y áreas de impresión, y escalones de precio de referencia. (7 entidades)
- `bases` — Fotos de prendas en blanco preparadas para mockup: recorte, mapas, zonas detectadas y escenas. (3 entidades)
- `disenos` — Diseños por marca, artes importados de Illustrator, fuentes y composiciones (diseño aplicado a un modelo con técnica, acabado y capas). (5 entidades)
- `ia` — Plantillas de prompts, consumo y costo de Anthropic y Gemini, y contenido de texto generado. (3 entidades)
- `mockups` — Perfiles de exportación, lotes automáticos (composiciones x colores x vistas x escenas x perfiles) y galería de resultados. (3 entidades)
- `costos` — Tarifas de maquila por reglas, costos adicionales y cotizaciones de costo por pieza. (4 entidades)
- `produccion` — Archivos de producción por zona y grupo de talla y paquetes para el maquilador. (2 entidades)
- `modelos-3d` — Fase 2: modelos .glb por prenda hechos en Marvelous Designer, piezas del patrón de corte y materiales de tela para el visor 3D, GIF y video 360. (3 entidades)

Diseño de interfaz: `DESIGN.md`. Diagrama de entidades: `docs/er.mmd`.

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).
