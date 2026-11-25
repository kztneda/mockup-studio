# Catálogo de valores · SaaS Pack v2.0.0

> Archivo generado desde `packages/shared/src/catalog`. No editar a mano.

Usa siempre el **Valor** exacto. El import también acepta los alias y el nombre (los normaliza), pero el pack queda más claro con el valor canónico.

## Stack tecnológico

### Plataformas objetivo · `AppPlatform`

Dónde corre la aplicación. Define qué tipos de pantalla aplican (web o móvil).

- **Dónde:** `infrastructure.yaml › platform.targets`
- **Valores:** lista (varios)
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `web` | Web | Aplicación en el navegador (SPA, SSR o PWA). | alias: browser, pwa, navegador |
| `mobile` | Móvil | iOS y/o Android, nativo o multiplataforma. | alias: ios, android, movil, app |
| `desktop` | Desktop | macOS, Windows y/o Linux. | alias: escritorio, windows, macos |

### Framework móvil · `MobileTech`

Tecnología de la app móvil. Solo aplica si platform.targets incluye mobile.

- **Dónde:** `infrastructure.yaml › platform.mobile`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `expo` | Multiplataforma | Expo (React Native) | React Native gestionado: OTA updates, EAS Build y sin Xcode/Android Studio para empezar. Mejor opción si el web es React. | lenguaje typescript |
| `react-native` | Multiplataforma | React Native (bare) | Control total del código nativo; elegir solo si se necesitan módulos nativos propios. | lenguaje typescript · alias: rn, reactnative |
| `flutter` | Multiplataforma | Flutter | Dart con motor gráfico propio; UI idéntica en iOS/Android y alto rendimiento. | lenguaje dart |
| `kotlin-multiplatform` | Multiplataforma | Kotlin Multiplatform | Lógica compartida en Kotlin y UI nativa o Compose Multiplatform. | lenguaje kotlin · alias: kmp, compose-multiplatform |
| `maui` | Multiplataforma | .NET MAUI | C# y XAML para iOS, Android, Windows y macOS. Natural si el backend es .NET. | lenguaje csharp · alias: xamarin, dotnet-maui |
| `capacitor` | Híbrido | Capacitor | Empaqueta la web app existente como app nativa con acceso a APIs del dispositivo. | lenguaje typescript |
| `ionic` | Híbrido | Ionic | UI kit híbrido sobre Capacitor con Angular, React o Vue. | lenguaje typescript |
| `nativescript` | Híbrido | NativeScript | JavaScript con acceso directo a APIs nativas. | lenguaje typescript |
| `swiftui` | Nativo | Swift / SwiftUI (iOS) | Nativo iOS. Máxima calidad en Apple, sin código compartido con Android. | lenguaje swift · alias: swift, ios-native |
| `jetpack-compose` | Nativo | Kotlin / Jetpack Compose (Android) | Nativo Android con UI declarativa. | lenguaje kotlin · alias: kotlin, android-native, compose |

### Framework desktop · `DesktopTech`

Tecnología de la app de escritorio. Solo aplica si platform.targets incluye desktop.

- **Dónde:** `infrastructure.yaml › platform.desktop`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `electron` | Electron | Node.js + Chromium; reutiliza el frontend web. Binarios pesados. | lenguaje typescript |
| `tauri` | Tauri | WebView del sistema + Rust; binarios ligeros y seguros, reutiliza el frontend web. | lenguaje rust |
| `wails` | Wails | WebView + Go; similar a Tauri para equipos Go. | lenguaje go |
| `maui` | .NET MAUI | Desktop y móvil con C#/XAML. | lenguaje csharp |
| `wpf` | WPF | UI Windows madura en .NET; solo Windows. | lenguaje csharp |
| `avalonia` | Avalonia UI | XAML multiplataforma (Windows, macOS, Linux) en .NET. | lenguaje csharp |
| `flutter` | Flutter Desktop | El mismo código Flutter de móvil compilado a escritorio. | lenguaje dart |
| `qt` | Qt | C++/QML nativo, ideal para apps industriales o de alto rendimiento. | lenguaje cpp |

### Frontend web · `FrontendTech`

Framework de la interfaz web. No mezclar ecosistemas (p. ej. react con nuxt).

- **Dónde:** `infrastructure.yaml › stack.frontend`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `nextjs` | React | Next.js | React con SSR/SSG y App Router. Elegir cuando hay SEO, landing pública o se quiere un solo framework full-stack. | genera código · lenguaje typescript · alias: next |
| `react` | React | React (SPA con Vite) | SPA pura; ideal para paneles internos sin SEO. | lenguaje typescript · alias: reactjs, vite |
| `react-router` | React | React Router / Remix | React full-stack centrado en web standards y loaders. | lenguaje typescript · alias: remix |
| `vue` | Vue | Vue 3 | Framework progresivo; SPA. | lenguaje typescript · alias: vuejs |
| `nuxt` | Vue | Nuxt | Vue con SSR/SSG. | lenguaje typescript |
| `angular` | Angular | Angular | Framework completo con DI; habitual en enterprise y banca. | lenguaje typescript |
| `svelte` | Svelte | Svelte | Compilado, mínimo runtime; SPA. | lenguaje typescript |
| `sveltekit` | Svelte | SvelteKit | Svelte con SSR/SSG y rutas por archivos. | lenguaje typescript |
| `solid` | Otros | SolidJS | Reactividad fina, muy rápido. | lenguaje typescript · alias: solidjs, solidstart |
| `astro` | Otros | Astro | Sitios de contenido con islas interactivas; ideal para marketing/docs. | lenguaje typescript |
| `qwik` | Otros | Qwik | Resumabilidad: carga casi nula de JS inicial. | lenguaje typescript |
| `blazor` | .NET | Blazor | UI web en C#. Natural con backend .NET. | lenguaje csharp · requiere backend: dotnet |
| `htmx` | Server-side | HTMX + plantillas del servidor | HTML renderizado en el servidor con interactividad declarativa; mínimo JS. | lenguaje html · alias: server-rendered, mvc |

### Backend · `BackendTech`

Framework del servidor. El lenguaje determina los ORMs compatibles.

- **Dónde:** `infrastructure.yaml › stack.backend`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `nestjs` | Node.js | NestJS | Node.js modular con DI y decorators; estructura enterprise. | genera código · lenguaje typescript · alias: nest |
| `express` | Node.js | Express | Minimalista y universal; requiere definir la estructura a mano. | lenguaje typescript · alias: expressjs, node |
| `fastify` | Node.js | Fastify | Node.js de alto rendimiento con schemas JSON. | lenguaje typescript |
| `hono` | Node.js | Hono | Ultraligero; corre en edge (Cloudflare Workers, Bun, Deno). | lenguaje typescript |
| `adonisjs` | Node.js | AdonisJS | Full-stack estilo Laravel para Node. | lenguaje typescript · alias: adonis |
| `dotnet` | .NET | .NET (ASP.NET Core) | C# de alto rendimiento, tipado fuerte; excelente para ERPs y enterprise. | lenguaje csharp · alias: aspnet, aspnetcore, net, csharp, c#, dotnet-core |
| `spring` | JVM | Spring Boot | Java/Kotlin, el estándar enterprise en JVM. | lenguaje java · alias: springboot, java |
| `quarkus` | JVM | Quarkus | Java nativo para contenedores; arranque rápido y poca memoria. | lenguaje java |
| `ktor` | JVM | Ktor | Kotlin ligero con corrutinas. | lenguaje kotlin |
| `django` | Python | Django | Python con baterías incluidas: ORM, admin y auth. | lenguaje python |
| `fastapi` | Python | FastAPI | Python async con tipado y OpenAPI automático; ideal con IA/ML. | lenguaje python |
| `laravel` | PHP | Laravel | PHP productivo con ecosistema completo. | lenguaje php · alias: php |
| `rails` | Ruby | Ruby on Rails | Convención sobre configuración; muy productivo para MVPs. | lenguaje ruby · alias: ruby, ror |
| `go` | Go | Go (Gin/Echo/Fiber) | Binarios pequeños, alta concurrencia, bajo consumo. | lenguaje go · alias: golang, gin, echo, fiber |
| `axum` | Rust | Rust (Axum/Actix) | Máximo rendimiento y seguridad de memoria; curva alta. | lenguaje rust · alias: rust, actix |
| `phoenix` | Elixir | Elixir / Phoenix | BEAM: tiempo real y tolerancia a fallos de forma nativa. | lenguaje elixir · alias: elixir |

### Estilo de API · `ApiStyle`

Cómo expone el backend sus operaciones.

- **Dónde:** `infrastructure.yaml › stack.apiStyle`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `rest` | REST | Recursos HTTP con OpenAPI. Opción por defecto. |  |
| `graphql` | GraphQL | Consultas flexibles desde el cliente; útil con muchos clientes distintos. |  |
| `grpc` | gRPC | Binario y tipado; comunicación entre microservicios. |  |
| `trpc` | tRPC | Tipos compartidos end-to-end en monorepos TypeScript. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `odata` | OData | Consultas estandarizadas sobre REST; común en .NET y ERPs. |  |
| `websocket` | WebSocket API | Canal bidireccional para operaciones en tiempo real. |  |
| `webhooks` | Webhooks salientes | Notifica eventos a sistemas de terceros. |  |

### Base de datos · `DatabaseTech`

Motor de datos principal. Define los tipos de campo nativos disponibles.

- **Dónde:** `infrastructure.yaml › stack.database`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `postgresql` | Relacional | PostgreSQL | Opción por defecto: robusto, JSONB, búsqueda de texto y extensiones. | alias: postgres, pg, psql |
| `mysql` | Relacional | MySQL | Muy difundido y económico de hospedar. | genera código |
| `mariadb` | Relacional | MariaDB | Fork abierto de MySQL, compatible en la mayoría de casos. |  |
| `sqlserver` | Relacional | SQL Server | Estándar en ecosistemas Microsoft/.NET y ERPs. | alias: mssql, azure-sql |
| `oracle` | Relacional | Oracle Database | Enterprise y gobierno; licencia costosa. |  |
| `sqlite` | Relacional | SQLite | Embebida; demos, apps locales o edge (Turso/libSQL). |  |
| `cockroachdb` | Relacional distribuida | CockroachDB | SQL compatible con Postgres, distribuido globalmente. | alias: cockroach |
| `mongodb` | Documentos | MongoDB | Documentos con esquema flexible; catálogos variables y contenido. | alias: mongo |
| `dynamodb` | Documentos | DynamoDB | Clave-valor serverless de AWS; acceso por patrones conocidos. |  |
| `cosmosdb` | Documentos | Azure Cosmos DB | Multi-modelo distribuido de Azure. | alias: cosmos |
| `firestore` | Documentos | Firestore | Documentos con sincronización en tiempo real para apps móviles. | alias: firebase |
| `cassandra` | Columnar | Cassandra / ScyllaDB | Escrituras masivas y series largas. | alias: scylladb |
| `clickhouse` | Analítica | ClickHouse | OLAP columnar para analítica y reportes sobre millones de filas. |  |

### ORM / acceso a datos · `OrmTech`

Capa de acceso a datos. Debe coincidir con el lenguaje del backend.

- **Dónde:** `infrastructure.yaml › stack.orm`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `prisma` | TypeScript | Prisma | Esquema declarativo, migraciones y tipos generados. | genera código · requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `drizzle` | TypeScript | Drizzle | SQL tipado y ligero. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `typeorm` | TypeScript | TypeORM | Decoradores, Active Record o Data Mapper. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `mikro-orm` | TypeScript | MikroORM | Unit of Work e Identity Map al estilo Doctrine/Hibernate. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `sequelize` | TypeScript | Sequelize | ORM clásico de Node. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `kysely` | TypeScript | Kysely | Query builder tipado sin magia. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs |
| `mongoose` | TypeScript | Mongoose | ODM para MongoDB. | requiere backend: nestjs \| express \| fastify \| hono \| adonisjs · requiere base de datos: mongodb |
| `efcore` | .NET | Entity Framework Core | ORM oficial de .NET con migraciones y LINQ. | requiere backend: dotnet · alias: ef, entityframework |
| `dapper` | .NET | Dapper | Micro-ORM de .NET: SQL a mano, máximo rendimiento. Se combina con EF Core. | requiere backend: dotnet |
| `hibernate` | JVM | Hibernate / JPA | Estándar JVM de persistencia. | requiere backend: spring \| quarkus \| ktor · alias: jpa, spring-data |
| `django-orm` | Python | Django ORM | ORM integrado de Django. | requiere backend: django |
| `sqlalchemy` | Python | SQLAlchemy | ORM y toolkit SQL de Python. | requiere backend: fastapi \| django · alias: sqlmodel |
| `eloquent` | PHP | Eloquent | Active Record de Laravel. | requiere backend: laravel |
| `active-record` | Ruby | Active Record | ORM de Rails. | requiere backend: rails |
| `gorm` | Go | GORM / sqlc | Acceso a datos en Go. | requiere backend: go · alias: sqlc |
| `ecto` | Elixir | Ecto | Acceso a datos de Elixir. | requiere backend: phoenix |
| `diesel` | Rust | Diesel / SQLx | Acceso a datos tipado en Rust. | requiere backend: axum · alias: sqlx, seaorm |

### Cache · `CacheTech`

Cache en memoria. Incluir si hay sesiones, rate limiting, colas ligeras o consultas costosas.

- **Dónde:** `infrastructure.yaml › stack.cache`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `redis` | Redis | Cache, pub/sub, locks y base de colas (BullMQ). |  |
| `valkey` | Valkey | Fork abierto de Redis, compatible a nivel protocolo. |  |
| `dragonfly` | Dragonfly | Compatible con Redis, multi-hilo y más eficiente en memoria. |  |
| `memcached` | Memcached | Cache clave-valor simple, sin persistencia. |  |
| `in-memory` | Cache en proceso | Cache local del servidor; solo para una instancia. | alias: memory, imemorycache |

### Mensajería y colas · `BrokerTech`

Message broker o sistema de jobs. Incluir si hay workflows, eventos asíncronos o tareas en segundo plano.

- **Dónde:** `infrastructure.yaml › stack.messageBroker`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `rabbitmq` | Broker | RabbitMQ | AMQP simple y confiable; correcto para la mayoría de SaaS. | alias: amqp |
| `kafka` | Streaming | Apache Kafka | Streaming con replay; solo con volúmenes muy altos o event sourcing. | alias: redpanda |
| `nats` | Broker | NATS / JetStream | Mensajería ligera y muy rápida. |  |
| `sqs` | Cloud | Amazon SQS/SNS | Colas administradas de AWS. | alias: sns |
| `azure-service-bus` | Cloud | Azure Service Bus | Broker administrado de Azure. | alias: servicebus |
| `google-pubsub` | Cloud | Google Pub/Sub | Mensajería administrada de GCP. | alias: pubsub |
| `bullmq` | Jobs | BullMQ | Colas de jobs con reintentos y retrasos sobre Redis (Node). | requiere cache: redis \| valkey \| dragonfly |
| `hangfire` | Jobs | Hangfire | Jobs en segundo plano para .NET con dashboard. | requiere backend: dotnet |
| `celery` | Jobs | Celery | Jobs distribuidos para Python. | requiere backend: django \| fastapi |
| `sidekiq` | Jobs | Sidekiq | Jobs para Ruby sobre Redis. | requiere backend: rails |
| `db-queue` | Jobs | Cola en base de datos | Tabla de jobs con SKIP LOCKED; sin servicios extra. | alias: outbox, pg-boss |

### Almacenamiento de archivos · `StorageTech`

Dónde se guardan archivos subidos, imágenes y exportaciones.

- **Dónde:** `infrastructure.yaml › stack.storage`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `s3` | Amazon S3 | Almacenamiento de objetos estándar; API compatible con casi todos. | alias: aws-s3 |
| `r2` | Cloudflare R2 | Compatible con S3 sin costo de salida de datos. | alias: cloudflare-r2 |
| `azure-blob` | Azure Blob Storage | Objetos en Azure. | alias: blob |
| `gcs` | Google Cloud Storage | Objetos en GCP. |  |
| `minio` | MinIO | S3 self-hosted; on-premise o desarrollo local. |  |
| `backblaze-b2` | Backblaze B2 | Compatible con S3 y muy económico. | alias: b2 |
| `cloudinary` | Cloudinary | Imágenes y video con transformaciones al vuelo. |  |
| `uploadthing` | UploadThing | Subidas administradas para apps TypeScript. |  |
| `local-disk` | Disco local | Volumen del servidor; solo para una instancia. | alias: filesystem, local |

### Búsqueda · `SearchTech`

Motor de búsqueda de texto. Incluir si hay catálogos grandes o búsqueda tolerante a errores.

- **Dónde:** `infrastructure.yaml › stack.search`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `database-fts` | Full-text de la base de datos | Búsqueda nativa del motor; suficiente para la mayoría. | alias: postgres-fts, fts, fulltext |
| `meilisearch` | Meilisearch | Instantánea y tolerante a typos; fácil de operar. |  |
| `typesense` | Typesense | Similar a Meilisearch, con búsqueda vectorial. |  |
| `elasticsearch` | Elasticsearch | Búsqueda y analítica a gran escala. | alias: elastic |
| `opensearch` | OpenSearch | Fork abierto de Elasticsearch (AWS). |  |
| `algolia` | Algolia | Búsqueda SaaS administrada. |  |
| `pgvector` | pgvector / búsqueda vectorial | Búsqueda semántica con embeddings (IA, RAG). | alias: vector, embeddings |

### Tiempo real · `RealtimeTech`

Canal para notificaciones en vivo, chat o colaboración.

- **Dónde:** `infrastructure.yaml › stack.realtime`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `websocket` | WebSocket nativo | Bidireccional sin dependencias. | alias: ws |
| `socketio` | Socket.IO | WebSocket con reconexión y salas (Node). | alias: socket.io |
| `signalr` | SignalR | Tiempo real de .NET. | requiere backend: dotnet |
| `sse` | Server-Sent Events | Unidireccional servidor → cliente; simple y compatible con proxies. |  |
| `pusher` | Pusher | Canales administrados. |  |
| `ably` | Ably | Mensajería en tiempo real administrada con garantías de entrega. |  |
| `mercure` | Mercure | Hub SSE autohospedado. |  |

## Infraestructura

### Hosting / nube · `HostingTech`

Dónde se despliega la plataforma.

- **Dónde:** `infrastructure.yaml › infrastructure.hosting`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `aws` | Nube pública | AWS | Catálogo más amplio de servicios administrados. | alias: amazon |
| `azure` | Nube pública | Microsoft Azure | Natural con .NET, SQL Server y Microsoft 365/Entra ID. |  |
| `gcp` | Nube pública | Google Cloud | Fuerte en datos, Kubernetes (GKE) e IA. | alias: google-cloud |
| `vercel` | PaaS | Vercel | Frontend Next.js y funciones serverless. |  |
| `netlify` | PaaS | Netlify | Sitios estáticos y funciones. |  |
| `cloudflare` | PaaS | Cloudflare | Edge: Workers, Pages, R2, D1. | alias: workers, pages |
| `fly` | PaaS | Fly.io | Contenedores cerca del usuario. | alias: flyio |
| `railway` | PaaS | Railway | Despliegue simple de servicios y bases de datos. |  |
| `render` | PaaS | Render | PaaS sencillo para web services y workers. |  |
| `heroku` | PaaS | Heroku | PaaS clásico. |  |
| `digitalocean` | VPS | DigitalOcean | VPS y servicios administrados económicos. | alias: do |
| `hetzner` | VPS | Hetzner | VPS y bare metal muy económicos (UE). |  |
| `vps` | VPS | VPS genérico | Servidor Linux administrado por el equipo (Docker/Portainer). | alias: linode, vultr |
| `on-premise` | Propio | On-premise | Infraestructura del cliente; común en gobierno y ERPs. | alias: onprem, local |

### Contenedores y orquestación · `ContainerTech`

Cómo se empaquetan y orquestan los servicios.

- **Dónde:** `infrastructure.yaml › infrastructure.containerization`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `docker` | Docker | Imagen por servicio. |  |
| `docker-compose` | Docker Compose | Varios servicios en un host; ideal en VPS. | alias: compose, portainer |
| `kubernetes` | Kubernetes | Orquestación para muchos servicios o alta disponibilidad. | alias: k8s, eks, aks, gke |
| `helm` | Helm | Paquetes para Kubernetes. | requiere contenedores y orquestación: kubernetes |
| `podman` | Podman | Contenedores sin daemon, compatible con Docker. |  |
| `ecs` | AWS ECS / Fargate | Contenedores administrados de AWS sin Kubernetes. | alias: fargate |
| `cloud-run` | Google Cloud Run | Contenedores serverless. | alias: azure-container-apps |
| `serverless` | Funciones serverless | Lambda, Azure Functions o similares. | alias: lambda, azure-functions |

### Infraestructura como código · `IacTech`

Herramienta para declarar la infraestructura.

- **Dónde:** `infrastructure.yaml › infrastructure.iac`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `terraform` | Terraform | Multi-nube y el más difundido. |  |
| `opentofu` | OpenTofu | Fork abierto de Terraform. |  |
| `pulumi` | Pulumi | IaC en TypeScript, C#, Python o Go. |  |
| `bicep` | Bicep | IaC nativo de Azure. |  |
| `cloudformation` | CloudFormation / CDK | IaC nativo de AWS. | alias: cdk, aws-cdk |
| `ansible` | Ansible | Configuración de servidores y despliegues en VPS. |  |

### Observabilidad · `ObservabilityTech`

Logs, métricas, trazas y errores.

- **Dónde:** `infrastructure.yaml › infrastructure.observability`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `opentelemetry` | Estándar | OpenTelemetry | Instrumentación estándar de trazas, métricas y logs; agnóstico del proveedor. | alias: otel |
| `prometheus` | Métricas | Prometheus | Métricas y alertas. |  |
| `grafana` | Métricas | Grafana | Dashboards sobre Prometheus, Loki o Tempo. |  |
| `loki` | Logs | Grafana Loki | Logs indexados por etiquetas, económico. |  |
| `elk` | Logs | Elastic (ELK) | Logs y búsqueda con Elasticsearch y Kibana. | alias: elastic-stack, kibana, logstash |
| `seq` | Logs | Seq | Logs estructurados; muy usado con Serilog en .NET. |  |
| `jaeger` | Trazas | Jaeger / Tempo | Trazas distribuidas. | alias: tempo |
| `sentry` | Errores | Sentry | Errores y rendimiento en frontend y backend. |  |
| `datadog` | SaaS | Datadog | Observabilidad completa administrada. |  |
| `new-relic` | SaaS | New Relic | APM administrado. | alias: newrelic |
| `app-insights` | SaaS | Azure Application Insights | APM de Azure. | alias: application-insights, azure-monitor |
| `cloudwatch` | SaaS | AWS CloudWatch | Logs y métricas de AWS. |  |

### CI/CD · `CicdTech`

Pipeline de integración y despliegue.

- **Dónde:** `infrastructure.yaml › infrastructure.cicd`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `github-actions` | GitHub Actions | CI/CD integrado en GitHub. | alias: github, gha |
| `gitlab-ci` | GitLab CI/CD | CI/CD integrado en GitLab. | alias: gitlab |
| `azure-devops` | Azure DevOps Pipelines | CI/CD de Microsoft. | alias: azure-pipelines, azure |
| `bitbucket-pipelines` | Bitbucket Pipelines | CI/CD de Bitbucket. | alias: bitbucket |
| `woodpecker` | Woodpecker CI | CI ligero autohospedado. |  |
| `jenkins` | Jenkins | CI autohospedado clásico. |  |
| `circleci` | CircleCI | CI administrado. |  |
| `argocd` | Argo CD | GitOps para Kubernetes. | requiere contenedores y orquestación: kubernetes · alias: gitops, flux |

## Modelo de dominio

### Tipo de SaaS · `SaaSType`

Modelo de negocio. Influye en multi-tenant, billing y roles.

- **Dónde:** `project.yaml › project.saasType`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `B2B` | B2B | Empresas como clientes; casi siempre multi-tenant con roles por organización. |  |
| `B2C` | B2C | Personas como clientes; registro abierto y alcance por usuario. |  |
| `B2B2C` | B2B2C / Marketplace | Empresas que sirven a sus clientes a través de la plataforma (marketplaces, white-label). | alias: marketplace |
| `B2G` | B2G (Gobierno) | Gobierno; auditoría estricta, on-premise frecuente. | alias: gov, govtech |
| `Internal` | Interno | Herramienta interna de una sola organización. | alias: interno, backoffice |

### Tipo de campo · `FieldType`

Tipo de dato de un campo. Los tipos semánticos (email, url, money…) se almacenan con su tipo base (storage) y además comunican la validación esperada.

- **Dónde:** `modules/*.yaml › entities[].fields[].type`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `string` | Texto | Texto corto (VARCHAR) | Texto de hasta maxLength (255 por defecto). | alias: varchar, nvarchar |
| `text` | Texto | Texto largo | Texto sin límite práctico. | alias: longtext, clob |
| `char` | Texto | Texto de longitud fija | Códigos de longitud fija (usa maxLength). | alias: nchar |
| `int` | Número | Entero (32 bits) | Entero de -2^31 a 2^31. | alias: integer, int32 |
| `bigint` | Número | Entero grande (64 bits) | Contadores grandes o ids numéricos. | alias: long, int64 |
| `smallint` | Número | Entero pequeño (16 bits) | Rangos pequeños. | alias: short, int16 |
| `tinyint` | Número | Entero mínimo (8 bits) | 0-255 (o -128 a 127). | solo sqlserver/mysql/mariadb · alias: byte |
| `decimal` | Número | Decimal exacto | Precisión exacta (precision = dígitos totales). | alias: numeric |
| `float` | Número | Flotante | Aproximado; medidas científicas, nunca dinero. | alias: real, single |
| `double` | Número | Flotante doble | Aproximado de doble precisión. |  |
| `boolean` | Lógico | Booleano | Verdadero o falso. | alias: bool, bit |
| `date` | Fecha y hora | Fecha | Solo fecha, sin hora. |  |
| `time` | Fecha y hora | Hora | Solo hora del día. |  |
| `datetime` | Fecha y hora | Fecha y hora | Instante; se guarda en UTC. | alias: datetime2 |
| `timestamp` | Fecha y hora | Fecha y hora con zona | Instante con zona horaria. | alias: timestamptz, datetimeoffset |
| `uuid` | Identidad | UUID / GUID | Identificador único; úsalo para llaves foráneas (xxxId). | alias: guid, uniqueidentifier |
| `json` | Estructurado | JSON | Documento JSON. |  |
| `jsonb` | Estructurado | JSONB | JSON binario indexable (PostgreSQL). | solo postgresql/cockroachdb |
| `blob` | Estructurado | Binario | Bytes crudos; preferir storage externo para archivos. | alias: binary, bytes, varbinary |
| `enum` | Estructurado | Enumeración | Uno de enumValues. Los estados de una máquina de estados usan enum. |  |
| `array` | Estructurado | Arreglo | Lista de valores; se almacena como JSON si el motor no tiene arreglos. |  |
| `money` | Número | Dinero | Importe monetario exacto (decimal 19,4). Acompañar de un campo currency si hay multimoneda. | alias: currency-amount, amount |
| `percentage` | Semántico | Porcentaje | Porcentaje 0-100 con decimales. | se guarda como decimal · alias: percent |
| `email` | Semántico | Email | Correo electrónico validado; normalizar a minúsculas. | se guarda como string |
| `phone` | Semántico | Teléfono | Teléfono en formato E.164 (+5215512345678). | se guarda como string · alias: telefono, tel |
| `url` | Semántico | URL | URL absoluta validada. | se guarda como string · alias: link, uri |
| `slug` | Semántico | Slug | Identificador legible en URLs (minúsculas y guiones); normalmente único. | se guarda como string |
| `password` | Semántico | Contraseña (hash) | Hash (argon2/bcrypt), nunca texto plano ni devuelto por la API. | se guarda como string · alias: password-hash, passwordhash |
| `richtext` | Semántico | Texto enriquecido | HTML sanitizado de un editor. | se guarda como text · alias: html, wysiwyg |
| `markdown` | Semántico | Markdown | Texto en Markdown. | se guarda como text · alias: md |
| `color` | Semántico | Color | Color hex (#RRGGBB). | se guarda como string · alias: hex |
| `rating` | Semántico | Calificación | Entero acotado (p. ej. 1-5) con validation.min/max. | se guarda como smallint · alias: stars, score |
| `duration` | Semántico | Duración | Duración en segundos (o minutos, indicarlo en la descripción). | se guarda como int |
| `country` | Semántico | País (ISO 3166) | Código ISO 3166-1 alfa-2 (MX, US). | se guarda como string · alias: country-code |
| `currency` | Semántico | Moneda (ISO 4217) | Código de moneda ISO 4217 (MXN, USD). | se guarda como string · alias: currency-code |
| `locale` | Semántico | Idioma / locale | Etiqueta BCP 47 (es-MX). | se guarda como string · alias: language |
| `ip-address` | Semántico | Dirección IP | IPv4 o IPv6. | se guarda como string · alias: ip, inet |
| `file` | Semántico | Archivo | Clave o URL del archivo en el storage (no el binario). | se guarda como string · alias: attachment, document |
| `image` | Semántico | Imagen | Clave o URL de la imagen en el storage. | se guarda como string · alias: photo, avatar, picture |
| `geopoint` | Semántico | Coordenadas | Latitud y longitud { lat, lng }. | se guarda como json · alias: location, latlng, geography |

### Sensibilidad del campo · `FieldSensitivity`

Clasificación del dato. Define cifrado, logs y exposición en la API.

- **Dónde:** `modules/*.yaml › entities[].fields[].sensitivity`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `pii` | Dato personal (PII) | Identifica a una persona: no registrar en logs; exportable y borrable a petición (LFPDPPP/GDPR). | alias: personal |
| `secret` | Secreto | Credenciales o tokens: cifrar en reposo y nunca devolver en la API. | alias: credential |
| `financial` | Dato financiero | Tarjetas, cuentas o datos fiscales: cifrar, auditar acceso y enmascarar al mostrar. | alias: pci, payment |
| `health` | Dato de salud | Información médica: cifrar, auditar todo acceso y restringir por rol. | alias: phi, medical |

### Alcance de la entidad · `EntityScope`

A quién pertenecen los registros. Si se omite, se hereda del proyecto (tenant si multiTenant.enabled).

- **Dónde:** `modules/*.yaml › entities[].scope`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `tenant` | Por tenant | Pertenece a una organización; todas las consultas filtran por tenant. | alias: organization, company |
| `global` | Global | Compartida por todos (catálogos, configuración del sistema). | alias: shared, catalog |
| `user` | Por usuario | Pertenece a una persona; solo su dueño la ve. | alias: personal, owner |

### Tipo de relación · `RelationType`

Cardinalidad. En ManyToOne/OneToOne la llave (sourceField) vive en source; en OneToMany vive en target (targetField).

- **Dónde:** `relations.yaml › relations[].type`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `ManyToOne` | Muchos a uno | Muchos source apuntan a un target (Factura → Cliente). La más común. | alias: n:1, belongsto |
| `OneToMany` | Uno a muchos | Un source tiene muchos target (Cliente → Facturas). | alias: 1:n, hasmany |
| `OneToOne` | Uno a uno | Exactamente uno; sourceField debe ser único. | alias: 1:1, hasone |
| `ManyToMany` | Muchos a muchos | Requiere tabla intermedia; preferir una entidad explícita si la unión tiene datos. | alias: n:m, n:n |

### Acción de permiso · `PermissionAction`

Operación que un rol puede ejecutar sobre un recurso (módulo o entidad).

- **Dónde:** `roles.yaml › roles[].permissions[].actions`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `create` | Crear | Alta de registros. |  |
| `read` | Ver | Ver el detalle de un registro. | alias: view, get |
| `list` | Listar | Ver listados y buscar. | alias: search, browse |
| `update` | Editar | Modificar registros. | alias: edit |
| `delete` | Eliminar | Eliminar (o borrado lógico). | alias: remove |
| `restore` | Restaurar | Recuperar registros con borrado lógico. |  |
| `archive` | Archivar | Sacar de circulación sin borrar. |  |
| `export` | Exportar | Descargar datos (CSV, Excel, PDF). | alias: download |
| `import` | Importar | Carga masiva. | alias: upload |
| `approve` | Aprobar | Aprobar o rechazar solicitudes. | alias: authorize |
| `publish` | Publicar | Hacer visible a terceros. |  |
| `cancel` | Cancelar | Anular operaciones (pedidos, facturas). | alias: void |
| `assign` | Asignar | Asignar responsables o recursos. |  |
| `share` | Compartir | Compartir con otros usuarios o externos. |  |
| `audit` | Auditar | Ver historial de cambios y actividades. | alias: history |
| `manage` | Administrar | Todas las acciones, incluida la configuración del recurso. | alias: admin, all, * |

### Tipo de pantalla · `ScreenType`

Patrón de UI. Los tipos web aplican a web/desktop y los de navegación móvil a mobile.

- **Dónde:** `modules/*.yaml › screens[].type`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `Dashboard` | Web | Dashboard | Resumen con KPIs y widgets. | web/desktop |
| `List` | Web | Listado | Tabla con filtros, orden y paginación. | web/desktop · alias: table, grid, index |
| `Detail` | Web | Detalle | Vista de un registro con pestañas de relacionados. | web/desktop · alias: show, view |
| `Form` | Web | Formulario | Alta o edición. | web/desktop · alias: edit, create |
| `Wizard` | Web | Asistente | Proceso guiado en pasos. | web/desktop · alias: stepper |
| `Report` | Web | Reporte | Consulta con filtros y exportación. | web/desktop |
| `Kanban` | Web | Kanban | Tarjetas por estado; ideal con máquinas de estado. | web/desktop · alias: board, pipeline |
| `Calendar` | Web | Calendario | Eventos o reservas por fecha. | web/desktop/mobile · alias: agenda, schedule |
| `Gantt` | Web | Cronograma (Gantt) | Barras en el tiempo con dependencias; planeación de proyectos. | web/desktop · alias: cronograma |
| `Timeline` | Web | Línea de tiempo | Hechos en orden cronológico: actividad reciente, historial de un registro. | web/desktop/mobile · alias: activity-feed, linea-de-tiempo |
| `Gallery` | Web | Galería | Tarjetas o miniaturas: plantillas, archivos, catálogos visuales. | web/desktop/mobile · alias: cards, galeria |
| `Tree` | Web | Árbol jerárquico | Registros anidados: organigrama, objetivos y resultados clave, categorías. | web/desktop · alias: hierarchy, org-chart, okr-tree |
| `Workload` | Web | Carga de trabajo | Capacidad y asignación por persona en el tiempo. | web/desktop · alias: capacity, resource-planning |
| `Editor` | Web | Editor visual | Lienzo para construir: flujos de automatización, apps, formularios. | web/desktop · alias: builder, canvas, designer, app-builder, flow-editor |
| `Map` | Web | Mapa | Registros georreferenciados. | web/desktop/mobile |
| `Chat` | Web | Chat / Mensajes | Conversaciones en tiempo real. | web/desktop/mobile · alias: inbox, messages |
| `Settings` | Web | Configuración | Preferencias de la cuenta o del tenant. | web/desktop/mobile · alias: preferences |
| `Auth` | Web | Autenticación | Login, registro o recuperación. | web/desktop/mobile · alias: login, signin, register |
| `Landing` | Web | Página pública | Página pública sin sesión (SEO). | web · alias: home, marketing |
| `Stack` | Móvil | Stack | Pantalla en una pila de navegación. | mobile |
| `Tab` | Móvil | Tab | Sección de la barra de pestañas inferior. | mobile · alias: tabs |
| `Drawer` | Móvil | Drawer | Menú lateral deslizable. | mobile |
| `Modal` | Móvil | Modal | Pantalla superpuesta a pantalla completa. | mobile |
| `BottomSheet` | Móvil | Bottom sheet | Panel inferior deslizable. | mobile · alias: sheet |

### Método HTTP · `HttpMethod`

Verbo del endpoint.

- **Dónde:** `modules/*.yaml › apis[].method`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `GET` | GET | Leer. |  |
| `POST` | POST | Crear o ejecutar una acción. |  |
| `PUT` | PUT | Reemplazar completo. |  |
| `PATCH` | PATCH | Actualización parcial. |  |
| `DELETE` | DELETE | Eliminar. |  |
| `HEAD` | HEAD | Solo encabezados. |  |
| `OPTIONS` | OPTIONS | Capacidades / CORS. |  |

### Nodo de workflow (diagrama) · `WorkflowNodeType`

Forma del nodo en el diagrama del workflow.

- **Dónde:** `modules/*.yaml › workflows[].nodes[].type`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `start` | Inicio | Punto de entrada. |  |
| `action` | Acción | Paso automático. |  |
| `approval` | Aprobación | Espera a una persona. |  |
| `decision` | Decisión | Bifurcación por condición. |  |
| `parallel` | Paralelo | Ramas que corren a la vez y se unen. |  |
| `wait` | Espera | Pausa hasta una fecha o evento. |  |
| `end` | Fin | Punto de salida. |  |

### Paso de workflow · `WorkflowStepType`

Tipo de paso en la secuencia del workflow. config lleva los parámetros del paso.

- **Dónde:** `modules/*.yaml › workflows[].steps[].type`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `trigger` | Disparador | Evento que inicia el workflow (config.event). |  |
| `condition` | Condición | Bifurca según una expresión (config.condition). | alias: if, branch |
| `action` | Acción | Operación del sistema (config.service). |  |
| `approval` | Aprobación | Espera aprobación de un rol (config.approverRole, config.timeoutHours). |  |
| `notification` | Notificación | Avisa por email, push, SMS o WhatsApp (config.channel, config.template). | alias: notify, email, sms |
| `delay` | Espera | Pausa un tiempo (config.duration). | alias: wait, sleep |
| `webhook` | Webhook / HTTP | Llama a un sistema externo (config.url, config.method). | alias: http, http-request, api-call |
| `script` | Script | Lógica personalizada (config.handler). | alias: code, function |
| `ai` | Paso de IA | Clasificar, extraer o generar con un modelo (config.prompt, config.model). | alias: llm, agent |
| `loop` | Iteración | Repite pasos por cada elemento (config.items). | alias: foreach |
| `parallel` | Paralelo | Ejecuta ramas a la vez. |  |
| `subworkflow` | Sub-workflow | Invoca otro workflow (config.workflow). |  |
| `end` | Fin | Termina el workflow. |  |

### Disparador de evento · `EventTrigger`

Qué provoca el evento de dominio.

- **Dónde:** `modules/*.yaml › events[].trigger`, `project.yaml › events[].trigger`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `on_create` | Al crear | Se crea un registro. | alias: oncreate, created |
| `on_update` | Al actualizar | Se modifica un registro. | alias: onupdate, updated |
| `on_delete` | Al eliminar | Se elimina un registro. | alias: ondelete, deleted |
| `on_state_change` | Al cambiar de estado | Una transición de la máquina de estados. | alias: onstatechange, transition |
| `on_approve` | Al aprobar | Se aprueba una solicitud. |  |
| `on_reject` | Al rechazar | Se rechaza una solicitud. |  |
| `on_login` | Al iniciar sesión | Un usuario inicia sesión. |  |
| `scheduled` | Programado (cron) | Hora o intervalo programado. | alias: cron, schedule |
| `webhook` | Webhook externo | Un sistema externo llama vía HTTP. | alias: onwebhook |
| `manual` | Manual | Lo dispara un usuario o el código explícitamente. | alias: oncustom, custom |

### Reacción al evento · `EventAction`

Qué hace el sistema cuando ocurre el evento.

- **Dónde:** `modules/*.yaml › events[].action`, `project.yaml › events[].action`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `send_email` | Enviar email | Email transaccional. |  |
| `send_notification` | Notificación push / in-app | Notificación al usuario. | alias: push |
| `send_sms` | Enviar SMS / WhatsApp | Mensaje al teléfono. | alias: whatsapp |
| `call_webhook` | Llamar webhook | Avisa a un sistema externo. |  |
| `trigger_workflow` | Iniciar workflow | Arranca un workflow del módulo. |  |
| `update_record` | Actualizar registro | Modifica otros datos (p. ej. saldos). |  |
| `enqueue_job` | Encolar job | Tarea en segundo plano. | alias: job |
| `log` | Registrar actividad | Solo deja traza en Actividades. | alias: audit |

### Widget de dashboard · `WidgetType`

Visualización de un widget.

- **Dónde:** `project.yaml › dashboards[].type`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `kpi` | Indicador | KPI | Número grande con variación. | alias: metric, stat |
| `card` | Indicador | Tarjeta | Resumen breve con texto. |  |
| `progress` | Indicador | Progreso | Avance hacia una meta. |  |
| `gauge` | Indicador | Medidor | Valor dentro de un rango. |  |
| `line` | Gráfica | Líneas | Tendencia en el tiempo. | alias: trend |
| `area` | Gráfica | Área | Tendencia acumulada. |  |
| `bar` | Gráfica | Barras | Comparación entre categorías. | alias: column |
| `pie` | Gráfica | Pastel / dona | Proporción de pocas categorías. | alias: donut |
| `funnel` | Gráfica | Embudo | Conversión por etapas. |  |
| `heatmap` | Gráfica | Mapa de calor | Intensidad por dos dimensiones. |  |
| `chart` | Gráfica | Gráfica genérica | Gráfica configurable en config. |  |
| `table` | Datos | Tabla | Filas con columnas. |  |
| `list` | Datos | Lista | Elementos recientes o pendientes. |  |
| `timeline` | Datos | Línea de tiempo | Actividad reciente en orden. | alias: activity |
| `calendar` | Datos | Calendario | Eventos por fecha. |  |
| `map` | Datos | Mapa | Datos georreferenciados. |  |

## Negocio, identidad e integraciones

### Integración · `IntegrationProvider`

Servicio de terceros. Activar solo las que el proyecto usa; config lleva los configKeys del proveedor.

- **Dónde:** `integrations.yaml › integrations[].provider`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `stripe` | Pagos | Stripe | Pagos, suscripciones y facturación global. | config: publicKey, secretKey, webhookSecret |
| `mercadopago` | Pagos | Mercado Pago | Tarjeta, OXXO y SPEI en México y LATAM. | config: accessToken, publicKey, webhookSecret · alias: mercado-pago |
| `conekta` | Pagos | Conekta | Tarjeta, OXXO y SPEI en México. | config: publicKey, privateKey, webhookSecret |
| `openpay` | Pagos | Openpay | Tarjeta y efectivo en México. | config: merchantId, privateKey, publicKey |
| `paypal` | Pagos | PayPal | Pagos con cuenta PayPal y tarjeta. | config: clientId, clientSecret, webhookId |
| `paddle` | Pagos | Paddle | Merchant of record: cobra e impuestos globales por ti. | config: apiKey, clientToken, webhookSecret |
| `lemonsqueezy` | Pagos | Lemon Squeezy | Merchant of record para software. | config: apiKey, storeId, webhookSecret · alias: lemon-squeezy |
| `adyen` | Pagos | Adyen | Pagos enterprise multipaís. | config: apiKey, merchantAccount, hmacKey |
| `facturapi` | Facturación | Facturapi | CFDI 4.0 (SAT) vía API. | config: apiKey, organizationId |
| `facturama` | Facturación | Facturama | CFDI 4.0 (SAT). | config: user, password |
| `sendgrid` | Email | SendGrid | Email transaccional y marketing. | config: apiKey, fromEmail, fromName |
| `ses` | Email | Amazon SES | Email transaccional económico sobre AWS. | config: region, fromEmail, configurationSet · alias: aws-ses |
| `resend` | Email | Resend | Email para desarrolladores con plantillas React. | config: apiKey, fromEmail |
| `postmark` | Email | Postmark | Email transaccional de alta entregabilidad. | config: serverToken, fromEmail |
| `mailgun` | Email | Mailgun | Email transaccional. | config: apiKey, domain, fromEmail |
| `brevo` | Email | Brevo | Email y marketing. | config: apiKey, fromEmail · alias: sendinblue |
| `twilio` | Mensajería | Twilio | SMS, voz y verificación. | config: accountSid, authToken, fromNumber |
| `whatsapp` | Mensajería | WhatsApp Business | Mensajes y plantillas por WhatsApp Cloud API. | config: phoneNumberId, accessToken, businessAccountId · alias: whatsapp-cloud |
| `firebase-fcm` | Mensajería | Firebase Cloud Messaging | Notificaciones push móviles y web. | config: projectId, clientEmail, privateKey · alias: fcm, push |
| `onesignal` | Mensajería | OneSignal | Push, in-app y email. | config: appId, apiKey |
| `slack` | Mensajería | Slack | Notificaciones y bots en Slack. | config: botToken, signingSecret |
| `telegram` | Mensajería | Telegram | Bots y notificaciones. | config: botToken |
| `anthropic` | IA | Anthropic (Claude) | Modelos Claude para generación, extracción y agentes. | config: apiKey, model, maxTokens · alias: claude |
| `openai` | IA | OpenAI | Modelos GPT y embeddings. | config: apiKey, model, maxTokens |
| `google-gemini` | IA | Google Gemini | Modelos Gemini. | config: apiKey, model · alias: gemini, vertex-ai |
| `azure-openai` | IA | Azure OpenAI | Modelos OpenAI dentro de Azure. | config: endpoint, apiKey, deployment |
| `aws-bedrock` | IA | AWS Bedrock | Modelos fundacionales administrados en AWS. | config: region, modelId · alias: bedrock |
| `aws` | Cloud | Amazon Web Services | Credenciales genéricas de AWS. | config: accessKeyId, secretAccessKey, region |
| `azure` | Cloud | Microsoft Azure | Credenciales genéricas de Azure. | config: tenantId, clientId, clientSecret |
| `gcp` | Cloud | Google Cloud | Credenciales genéricas de GCP. | config: projectId, clientEmail, privateKey · alias: google-cloud |
| `auth0` | Identidad | Auth0 | Identidad administrada. | config: domain, clientId, clientSecret |
| `clerk` | Identidad | Clerk | Auth con componentes listos para React. | config: publishableKey, secretKey |
| `authentik` | Identidad | authentik | IdP self-hosted (OIDC/SAML). | config: serverUrl, clientId, clientSecret, flowSlug |
| `keycloak` | Identidad | Keycloak | IAM open source. | config: serverUrl, realm, clientId, clientSecret |
| `keygen` | Identidad | Keygen | Licencias de software y entitlements. | config: accountId, productId, adminToken, apiUrl · alias: keygen-sh |
| `posthog` | Analítica | PostHog | Analítica de producto, feature flags y replays. | config: apiKey, host |
| `google-analytics` | Analítica | Google Analytics | Analítica web. | config: measurementId · alias: ga4, ga |
| `mixpanel` | Analítica | Mixpanel | Analítica por eventos. | config: projectToken |
| `segment` | Analítica | Segment | Enrutador de eventos de analítica. | config: writeKey |
| `google-maps` | Mapas | Google Maps | Mapas, geocodificación y rutas. | config: apiKey |
| `mapbox` | Mapas | Mapbox | Mapas personalizables. | config: accessToken |
| `hubspot` | CRM y soporte | HubSpot | CRM y marketing. | config: accessToken |
| `salesforce` | CRM y soporte | Salesforce | CRM enterprise. | config: instanceUrl, clientId, clientSecret |
| `zendesk` | CRM y soporte | Zendesk | Tickets de soporte. | config: subdomain, email, apiToken |
| `intercom` | CRM y soporte | Intercom | Chat de soporte in-app. | config: accessToken |
| `docusign` | Documentos | DocuSign | Firma electrónica. | config: integrationKey, userId, accountId, privateKey |
| `google-calendar` | Productividad | Google Calendar | Sincronización de agenda. | config: clientId, clientSecret |
| `microsoft-graph` | Productividad | Microsoft 365 (Graph) | Correo, calendario y archivos de Microsoft 365. | config: tenantId, clientId, clientSecret · alias: outlook, office365 |
| `zoom` | Productividad | Zoom | Videollamadas. | config: accountId, clientId, clientSecret |
| `shippo` | Logística | Shippo / Skydropx | Cotización y guías de envío. | config: apiKey · alias: skydropx, easypost |

### Proveedor de autenticación · `AuthProvider`

Métodos de inicio de sesión habilitados.

- **Dónde:** `project.yaml › security.auth.providers`
- **Valores:** lista (varios)
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `local` | Propio | Email y contraseña | Usuarios propios con hash argon2/bcrypt. | alias: password, credentials |
| `magic-link` | Propio | Magic link / OTP por email | Sin contraseña: enlace o código por correo. | alias: otp, passwordless |
| `passkeys` | Propio | Passkeys (WebAuthn) | Biometría o llave de seguridad. | alias: webauthn, fido2 |
| `phone-otp` | Propio | OTP por SMS/WhatsApp | Código al teléfono; común en apps móviles B2C. | alias: sms |
| `google` | Social | Google | OAuth de Google. | config: clientId, clientSecret |
| `microsoft` | Social | Microsoft / Entra ID | Cuentas Microsoft y corporativas. | config: clientId, clientSecret, issuerUrl · alias: azure-ad, entra |
| `apple` | Social | Apple | Obligatorio en iOS si hay otros logins sociales. | config: clientId, teamId, keyId, privateKey |
| `github` | Social | GitHub | Para productos de desarrolladores. | config: clientId, clientSecret |
| `facebook` | Social | Facebook | Login de Meta. | config: clientId, clientSecret · alias: meta |
| `oauth2` | Empresarial | OAuth2 / OIDC genérico | Cualquier IdP compatible con OpenID Connect. | config: clientId, clientSecret, issuerUrl · alias: oidc |
| `saml` | Empresarial | SAML 2.0 | SSO corporativo; requisito habitual en enterprise. | config: entryPoint, issuer, cert · alias: sso |
| `authentik` | Empresarial | authentik | IdP self-hosted. | config: clientId, clientSecret, issuerUrl |
| `keycloak` | Empresarial | Keycloak | IAM open source. | config: clientId, clientSecret, issuerUrl, realm |
| `auth0` | Administrado | Auth0 | Identidad administrada. | config: clientId, clientSecret, issuerUrl |
| `clerk` | Administrado | Clerk | Auth administrado para apps React/Next. | config: publishableKey, secretKey |
| `cognito` | Administrado | AWS Cognito | Identidad de AWS. | config: clientId, clientSecret, issuerUrl |
| `firebase-auth` | Administrado | Firebase Auth | Auth de Firebase. | config: projectId, apiKey · alias: firebase |
| `supabase-auth` | Administrado | Supabase Auth | Auth de Supabase. | config: url, anonKey · alias: supabase |
| `keygen` | Licencias | Keygen (licencias) | Activación por licencia de software. | config: accountId, productId |

### Proveedor de cobro · `BillingProvider`

Quién procesa las suscripciones.

- **Dónde:** `project.yaml › billing.provider`
- **Valores:** uno
- **Fuera del catálogo:** permitido como `custom:<valor>` (p. ej. `custom:mi-herramienta`)

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `stripe` | Stripe | Suscripciones, prorrateo y portal de cliente. |  |
| `mercadopago` | Mercado Pago | Suscripciones con medios locales de LATAM. |  |
| `conekta` | Conekta | Suscripciones en México. |  |
| `openpay` | Openpay | Cargos recurrentes en México. |  |
| `paddle` | Paddle | Merchant of record: impuestos globales incluidos. |  |
| `lemonsqueezy` | Lemon Squeezy | Merchant of record para software. |  |
| `paypal` | PayPal | Suscripciones PayPal. |  |
| `chargebee` | Chargebee | Orquestación de suscripciones sobre varios gateways. |  |
| `manual` | Manual / transferencia | Facturación y cobro fuera de la plataforma. | alias: offline, invoice |
| `none` | Sin cobro | Producto gratuito o interno. | alias: free |

### Periodicidad del plan · `BillingInterval`

Cada cuánto se cobra un plan.

- **Dónde:** `project.yaml › billing.plans[].interval`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `monthly` | Mensual | Cada mes. | alias: month, mensual |
| `quarterly` | Trimestral | Cada 3 meses. | alias: quarter |
| `yearly` | Anual | Cada año; suele llevar descuento. | alias: annual, year, anual |
| `weekly` | Semanal | Cada semana. | alias: week |
| `one-time` | Pago único | Un solo cobro (licencia perpetua). | alias: lifetime, once |
| `usage` | Por consumo | Se cobra lo consumido al cierre del periodo. | alias: metered, payg |

### Estrategia multi-tenant · `MultiTenantStrategy`

Cómo conviven los tenants en la infraestructura.

- **Dónde:** `project.yaml › multiTenant.strategy`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `shared` | Compartida | Una app y una base para todos; la opción más económica. |  |
| `isolated` | Aislada | Infraestructura dedicada por tenant; enterprise o regulado. |  |
| `hybrid` | Híbrida | Compartida por defecto y dedicada para los planes altos. |  |

### Nivel de aislamiento de datos · `IsolationLevel`

Cómo se separan los datos de cada tenant.

- **Dónde:** `project.yaml › multiTenant.isolationLevel`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `row` | Por fila (tenantId) | Columna tenantId en cada tabla; filtros obligatorios (o RLS). | alias: column, discriminator |
| `schema` | Por schema | Un schema por tenant en la misma base. |  |
| `database` | Por base de datos | Una base por tenant; máximo aislamiento. |  |

## Diseño de interfaz

### Librería de componentes · `UIComponentLibrary`

Sistema de componentes de la interfaz. Debe corresponder al framework frontend.

- **Dónde:** `ui-design.yaml › componentLibrary`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `material-ui` | React | Material UI | Material Design completo; ideal para paneles densos. | alias: mui |
| `shadcn-ui` | React | shadcn/ui | Componentes Radix + Tailwind copiados al proyecto; máxima personalización. | alias: shadcn |
| `ant-design` | React | Ant Design | Enterprise, tablas y formularios muy completos. | alias: antd |
| `mantine` | React | Mantine | Completo, con hooks y buen DX. |  |
| `chakra-ui` | React | Chakra UI | Accesible y modular. | alias: chakra |
| `fluent-ui` | React | Fluent UI | Diseño Microsoft; encaja con apps tipo Office/Teams. | alias: fluent |
| `tailwind` | Agnóstico | Tailwind CSS | Utility-first sin componentes; diseño propio. | alias: tailwindcss |
| `daisyui` | Agnóstico | daisyUI | Componentes CSS sobre Tailwind. |  |
| `bootstrap` | Agnóstico | Bootstrap | Clásico y conocido. |  |
| `primefaces` | Agnóstico | PrimeReact / PrimeNG / PrimeVue | Suite enterprise para React, Angular y Vue. | alias: primereact, primeng, primevue |
| `angular-material` | Angular | Angular Material | Material Design oficial de Angular. |  |
| `vuetify` | Vue | Vuetify | Material Design para Vue. |  |
| `quasar` | Vue | Quasar | Vue para web, móvil y desktop. |  |
| `nativewind` | Móvil | NativeWind | Tailwind para React Native. |  |
| `tamagui` | Móvil | Tamagui | UI compartida web + React Native. |  |
| `react-native-paper` | Móvil | React Native Paper | Material Design para React Native. | alias: rn-paper |
| `custom` | Otros | Propia | Design system propio o sin librería. | alias: none, propia |

### Tema por defecto · `ThemeMode`

Modo de color inicial.

- **Dónde:** `ui-design.yaml › defaultThemeMode`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `light` | Claro | Fondo claro. |  |
| `dark` | Oscuro | Fondo oscuro. |  |
| `system` | Sistema | Sigue la preferencia del sistema operativo. | alias: auto |

### Navegación · `NavLayoutType`

Estructura de navegación principal.

- **Dónde:** `ui-design.yaml › layout.navType`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `sidebar-left` | Sidebar izquierdo | Estándar en paneles administrativos. |  |
| `sidebar-right` | Sidebar derecho | Para idiomas RTL o preferencia de marca. |  |
| `mini-sidebar` | Mini sidebar | Solo iconos; maximiza el área de trabajo. | alias: collapsed |
| `topnav` | Barra superior | Pocas secciones; apps de consumo. | alias: top |
| `topnav-sidebar` | Barra superior + sidebar | Módulos arriba y submenú lateral; ERPs grandes. | alias: hybrid |
| `bottom-tabs` | Tabs inferiores | Navegación móvil o PWA. | alias: tabs |

### Densidad · `DesignDensity`

Espaciado general de la interfaz.

- **Dónde:** `ui-design.yaml › layout.density`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `compact` | Compacta | Más información por pantalla; ERPs y backoffice. |  |
| `comfortable` | Cómoda | Balance entre densidad y legibilidad. |  |
| `spacious` | Espaciosa | Amplia y táctil; apps de consumo. |  |

### Redondeo de bordes · `BorderRadiusPreset`

Forma de botones, inputs y tarjetas.

- **Dónde:** `ui-design.yaml › shape.borderRadiusPreset`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `sharp` | Recto (2px) | Sobrio, corporativo. |  |
| `soft` | Suave (4px) | Discreto. |  |
| `rounded` | Redondeado (8px) | Moderno y neutro. |  |
| `large` | Amplio (16px) | Amigable, apps de consumo. |  |
| `pill` | Píldora (24px) | Botones totalmente redondeados. |  |

### Tipografía · `UIFontFamily`

Familia tipográfica (Google Fonts salvo system-ui). Con custom se usa customFontFamily/customFontUrl.

- **Dónde:** `ui-design.yaml › typography.fontFamily`, `ui-design.yaml › typography.headingFontFamily`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Grupo | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- | --- |
| `inter` | Sans | Inter | Neutra y muy legible en UI. |  |
| `roboto` | Sans | Roboto | Material Design. |  |
| `open-sans` | Sans | Open Sans | Humanista y amigable. |  |
| `lato` | Sans | Lato | Cálida y profesional. |  |
| `nunito` | Sans | Nunito | Redondeada, amigable. |  |
| `poppins` | Sans | Poppins | Geométrica, para marca y títulos. |  |
| `montserrat` | Sans | Montserrat | Geométrica con carácter. |  |
| `manrope` | Sans | Manrope | Moderna, ideal para fintech. |  |
| `dm-sans` | Sans | DM Sans | Compacta y limpia. |  |
| `ibm-plex-sans` | Sans | IBM Plex Sans | Técnica, corporativa. |  |
| `source-sans` | Sans | Source Sans 3 | Legible en textos largos. | alias: source-sans-pro |
| `space-grotesk` | Display | Space Grotesk | Con personalidad; estética tech/street. |  |
| `geist` | Sans | Geist | De Vercel, minimalista. |  |
| `system-ui` | Sistema | Fuente del sistema | Sin descarga; la del sistema operativo. | alias: system |
| `custom` | Otros | Personalizada | Definida en customFontFamily y customFontUrl. |  |

### Estilo de botón · `ButtonStyle`

Variante principal de los botones.

- **Dónde:** `ui-design.yaml › shape.buttonStyle`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `filled` | Relleno | Fondo sólido. | alias: contained, solid |
| `soft` | Tonal | Fondo tenue del color primario. | alias: tonal |
| `outlined` | Contorno | Solo borde. |  |
| `ghost` | Fantasma | Sin fondo ni borde. | alias: text |

### Estilo de input · `InputStyle`

Variante de los campos de formulario.

- **Dónde:** `ui-design.yaml › shape.inputStyle`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `outlined` | Contorno | Borde completo. |  |
| `filled` | Relleno | Fondo tenue. |  |
| `standard` | Subrayado | Solo línea inferior. | alias: underline |

### Elevación · `ElevationStyle`

Cómo se separan las superficies.

- **Dónde:** `ui-design.yaml › shape.elevationStyle`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `flat` | Plano | Sin sombras ni bordes. |  |
| `border` | Bordes | Separación con líneas finas. |  |
| `shadow` | Sombras | Profundidad con sombras. |  |
| `glass` | Vidrio | Translúcido con desenfoque. | alias: glassmorphism |

### Espaciado de letras · `LetterSpacing`

Tracking del texto.

- **Dónde:** `ui-design.yaml › typography.letterSpacing`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `tight` | Cerrado | Más compacto. |  |
| `normal` | Normal | Por defecto de la fuente. |  |
| `wide` | Abierto | Más aire; títulos en mayúsculas. |  |

### Accesibilidad · `AccessibilityLevel`

Nivel WCAG 2.2 objetivo.

- **Dónde:** `ui-design.yaml › accessibilityLevel`
- **Valores:** uno
- **Fuera del catálogo:** no permitido

| Valor | Nombre | Cuándo usarlo | Notas |
| --- | --- | --- | --- |
| `none` | Sin objetivo | Sin requisito formal. |  |
| `A` | WCAG A | Mínimo. |  |
| `AA` | WCAG AA | Estándar legal habitual: contraste 4.5:1, teclado completo. |  |
| `AAA` | WCAG AAA | Máximo; gobierno o salud. |  |
