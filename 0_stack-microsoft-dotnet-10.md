# El Stack de Microsoft con .NET 10: Guía Teórica Completa

## Tabla de Contenidos

1. [Introducción a .NET 10](#introducción-a-net-10)
2. [Arquitectura de .NET 10](#arquitectura-de-net-10)
3. [Common Language Runtime (CLR)](#common-language-runtime-clr)
4. [Librerías Base (BCL)](#librerías-base-bcl)
5. [ASP.NET Core](#aspnet-core)
6. [Entity Framework Core](#entity-framework-core)
7. [Blazor](#blazor)
8. [MAUI (.NET Multi-platform App UI)](#maui-net-multi-platform-app-ui)
9. [Servicios en la Nube con Azure](#servicios-en-la-nube-con-azure)
10. [Herramientas de Desarrollo](#herramientas-de-desarrollo)
11. [Patrones y Mejores Prácticas](#patrones-y-mejores-prácticas)
12. [Seguridad](#seguridad)
13. [Rendimiento y Optimización](#rendimiento-y-optimización)
14. [Testing y Calidad de Código](#testing-y-calidad-de-código)
15. [Conclusiones](#conclusiones)

---

## Introducción a .NET 10

### Historia y Evolución

.NET 10 representa la culminación de más de dos décadas de evolución en la plataforma de desarrollo de Microsoft. Lanzado en noviembre de 2025, .NET 10 es una versión LTS (Long Term Support) que recibirá actualizaciones hasta noviembre de 2028, garantizando estabilidad y soporte extendido para aplicaciones empresariales.

La evolución de .NET ha sido notable:

- **.NET Framework (2002-2019)**: La versión original, exclusiva de Windows
- **.NET Core (2016-2020)**: Reescritura multiplataforma y de código abierto
- **.NET 5+ (2020-presente)**: Unificación de todas las implementaciones en una sola plataforma moderna

### Características Principales de .NET 10

.NET 10 se distingue por:

1. **Multiplataforma**: Ejecuta aplicaciones en Windows, Linux, macOS, iOS, Android y más
2. **Alto Rendimiento**: Optimizaciones en JIT, AOT y gestión de memoria
3. **Código Abierto**: Desarrollo transparente bajo licencia MIT en GitHub
4. **Unificación**: Una sola plataforma para web, móvil, escritorio, IoT y gaming
5. **Moderno**: Soporte para C# 13, F# 9 y las últimas tendencias de desarrollo

### Filosofía de Diseño

.NET 10 se basa en principios fundamentales:

- **Productividad del Desarrollador**: API intuitivas y herramientas poderosas
- **Rendimiento por Defecto**: Optimizaciones automáticas sin sacrificar claridad
- **Seguridad Integrada**: Protección contra vulnerabilidades comunes desde el diseño
- **Flexibilidad**: Desde microservicios hasta monolitos, desde contenedores hasta serverless
- **Interoperabilidad**: Integración con sistemas existentes y tecnologías externas

---

## Arquitectura de .NET 10

### Visión General Arquitectónica

La arquitectura de .NET 10 se estructura en capas claramente definidas:

```
┌─────────────────────────────────────────────────────┐
│        Aplicaciones y Frameworks de Usuario          │
│  (ASP.NET Core, Blazor, MAUI, WPF, Windows Forms)   │
├─────────────────────────────────────────────────────┤
│           Frameworks y Bibliotecas de Alto Nivel     │
│     (Entity Framework, ML.NET, gRPC, SignalR)       │
├─────────────────────────────────────────────────────┤
│        Bibliotecas Base de Clases (BCL)             │
│  (System.*, Collections, IO, Networking, Security)   │
├─────────────────────────────────────────────────────┤
│          Common Language Runtime (CLR)               │
│    (JIT, GC, Type System, Exception Handling)       │
├─────────────────────────────────────────────────────┤
│           Sistema Operativo Subyacente              │
│        (Windows, Linux, macOS, Android, iOS)        │
└─────────────────────────────────────────────────────┘
```

### Componentes Fundamentales

#### 1. Runtime

El runtime de .NET 10 incluye:

- **CoreCLR**: Runtime principal con JIT compilation
- **Mono Runtime**: Para móviles y WebAssembly
- **NativeAOT**: Compilación ahead-of-time para máximo rendimiento

#### 2. Bibliotecas

Las bibliotecas se organizan en:

- **Bibliotecas Base**: Funcionalidad fundamental (tipos básicos, colecciones, I/O)
- **Bibliotecas de Framework**: Características específicas de dominio (web, datos, UI)
- **Bibliotecas de Terceros**: Ecosistema NuGet con millones de paquetes

#### 3. Herramientas

El ecosistema de herramientas comprende:

- **SDK**: Compiladores, herramientas de línea de comandos, templates
- **IDEs**: Visual Studio, Visual Studio Code, Rider
- **Diagnóstico**: Profilers, debuggers, analizadores de rendimiento

### Modelo de Compilación y Ejecución

#### Compilación en Dos Fases

1. **Compilación a IL (Intermediate Language)**:
   - El código fuente (C#, F#, VB.NET) se compila a Common Intermediate Language (CIL)
   - El CIL es código independiente de plataforma y procesador
   - Los metadatos se almacenan en el assembly junto al código IL

2. **Compilación JIT (Just-In-Time)**:
   - En tiempo de ejecución, el CLR compila IL a código nativo
   - Se optimiza para la arquitectura específica del procesador
   - El código nativo se cachea para reutilización

#### Alternativas de Compilación

- **AOT (Ahead-of-Time)**: Compilación previa para inicio instantáneo
- **R2R (Ready-to-Run)**: Híbrido entre IL y código nativo
- **Crossgen**: Generación de código nativo durante la publicación

### Common Language Infrastructure (CLI)

El CLI define los estándares fundamentales:

1. **Common Type System (CTS)**: Sistema unificado de tipos
2. **Common Language Specification (CLS)**: Interoperabilidad entre lenguajes
3. **Virtual Execution System (VES)**: Entorno de ejecución virtual
4. **Metadata**: Información sobre tipos, miembros y referencias

---

## Common Language Runtime (CLR)

### Descripción General del CLR

El CLR es el corazón de .NET 10, responsable de la ejecución de código administrado. Proporciona servicios críticos que liberan al desarrollador de tareas complejas de bajo nivel.

### Gestión de Memoria y Garbage Collection

#### El Heap Administrado

La memoria en .NET se organiza jerárquicamente:

- **Generación 0**: Objetos de vida corta (recolección frecuente)
- **Generación 1**: Buffer entre Gen0 y Gen2
- **Generación 2**: Objetos de vida larga (recolección infrecuente)
- **Large Object Heap (LOH)**: Objetos mayores a 85KB

#### Algoritmos de Recolección

.NET 10 implementa varios modos de GC:

1. **Workstation GC**:
   - Optimizado para aplicaciones de escritorio
   - Menor latencia, pausa más corta
   - Un solo thread de GC

2. **Server GC**:
   - Optimizado para throughput en servidores
   - Múltiples threads de GC (uno por CPU)
   - Mayor rendimiento en cargas altas

3. **Background GC**:
   - Recolección concurrente de Gen2
   - Minimiza pausas perceptibles
   - Aplicaciones más responsivas

#### Gestión de Memoria No Administrada

Para interoperar con código nativo:

- **IDisposable Pattern**: Liberación determinística de recursos
- **using statements**: Garantía automática de limpieza
- **SafeHandles**: Wrappers seguros para handles nativos
- **Span<T> y Memory<T>**: Acceso eficiente a memoria sin asignaciones

### Sistema de Tipos

#### Tipos de Valor vs Tipos de Referencia

**Tipos de Valor (Value Types)**:
- Almacenados en el stack o inline en objetos
- Semántica de copia por valor
- Derivados de System.ValueType
- Ejemplos: int, double, struct, enum

**Tipos de Referencia (Reference Types)**:
- Almacenados en el heap administrado
- Semántica de copia por referencia
- Derivados de System.Object
- Ejemplos: class, interface, delegate, string

#### Genéricos

Los genéricos proporcionan:

- **Seguridad de tipos en tiempo de compilación**
- **Reutilización de código sin boxing**
- **Mejor rendimiento que colecciones no genéricas**
- **Constraints para restringir tipos permitidos**

Características avanzadas:
- Covarianza y contravarianza en interfaces y delegates
- Genéricos de mayor orden
- Especialización de tipos en runtime

### Carga de Assemblies

#### AssemblyLoadContext

.NET 10 utiliza contextos de carga aislados:

- **Carga por Demanda**: Assemblies se cargan cuando se necesitan
- **Descarga de Assemblies**: Liberación de memoria mediante collectible contexts
- **Versionado**: Múltiples versiones del mismo assembly pueden coexistir
- **Plugins**: Aislamiento para extensiones de terceros

#### Strong Names y Firma Digital

- Identidad única mediante clave pública/privada
- Protección contra manipulación
- Verificación de integridad
- Control de versiones estricto

### Ejecución de Código

#### JIT Compilation

El compilador JIT en .NET 10 ofrece:

1. **Tiered Compilation**:
   - Nivel 0: Compilación rápida sin optimizaciones
   - Nivel 1: Optimizaciones completas tras profiling
   - Recompilación dinámica basada en uso real

2. **Profile-Guided Optimization (PGO)**:
   - Instrumentación de código en producción
   - Optimización basada en patrones de uso reales
   - Mejoras continuas de rendimiento

3. **On-Stack Replacement (OSR)**:
   - Reemplazo de código durante ejecución de loops largos
   - Sin necesidad de reinvocación

### Manejo de Excepciones

#### Modelo Estructurado

.NET implementa un sistema robusto:

- **try-catch-finally**: Bloques estructurados de manejo
- **Exception Filters**: Condiciones para captura selectiva
- **Propagación Automática**: Stack unwinding consistente
- **Información Detallada**: Stack traces completos con metadatos

#### Excepciones Personalizadas

Jerarquía recomendada:
```
Exception (base)
├── SystemException
│   ├── ArgumentException
│   ├── InvalidOperationException
│   └── ...
└── ApplicationException (legado, no recomendado)
```

### Interoperabilidad

#### Platform Invoke (P/Invoke)

Llamadas a bibliotecas nativas:
- Marshaling automático de tipos comunes
- Custom marshaling para tipos complejos
- Callbacks desde código nativo
- Gestión de recursos no administrados

#### COM Interop

Integración con componentes COM:
- Runtime Callable Wrappers (RCW)
- COM Callable Wrappers (CCW)
- Type library import
- Event handling bidireccional

---

## Librerías Base (BCL)

### Namespace System

El namespace System contiene los tipos fundamentales:

#### Tipos Primitivos

- **Numéricos**: byte, short, int, long, float, double, decimal
- **Caracteres**: char, string
- **Booleano**: bool
- **Especiales**: DateTime, TimeSpan, Guid, Uri

#### System.Collections

Colecciones optimizadas para diferentes escenarios:

**Genéricas (System.Collections.Generic)**:
- `List<T>`: Array dinámico de acceso rápido
- `Dictionary<TKey, TValue>`: Hash table para búsquedas O(1)
- `HashSet<T>`: Conjunto sin duplicados
- `Queue<T>`: FIFO queue
- `Stack<T>`: LIFO stack
- `LinkedList<T>`: Lista doblemente enlazada
- `SortedList<TKey, TValue>`: Lista ordenada por clave
- `SortedDictionary<TKey, TValue>`: Árbol binario balanceado

**Concurrentes (System.Collections.Concurrent)**:
- `ConcurrentBag<T>`: Colección thread-safe sin orden
- `ConcurrentQueue<T>`: Queue thread-safe
- `ConcurrentStack<T>`: Stack thread-safe
- `ConcurrentDictionary<TKey, TValue>`: Dictionary thread-safe con operaciones atómicas

**Inmutables (System.Collections.Immutable)**:
- `ImmutableList<T>`: Lista inmutable con actualizaciones eficientes
- `ImmutableDictionary<TKey, TValue>`: Dictionary inmutable
- `ImmutableHashSet<T>`: HashSet inmutable

### System.IO

Operaciones de entrada/salida:

#### Archivos y Directorios

- **File / FileInfo**: Operaciones con archivos
- **Directory / DirectoryInfo**: Operaciones con directorios
- **Path**: Manipulación de rutas multiplataforma
- **DriveInfo**: Información sobre unidades de almacenamiento

#### Streams

Abstracción unificada para flujos de datos:

- **FileStream**: Lectura/escritura de archivos
- **MemoryStream**: Stream en memoria
- **BufferedStream**: Buffering para optimización
- **NetworkStream**: Comunicación de red
- **CryptoStream**: Transformación criptográfica de datos
- **GZipStream / DeflateStream**: Compresión de datos

#### Lectura/Escritura de Texto

- **StreamReader / StreamWriter**: Texto con encoding
- **StringReader / StringWriter**: Texto desde/hacia strings
- **BinaryReader / BinaryWriter**: Datos binarios tipados

### System.Threading

Programación concurrente y paralela:

#### Primitivas de Sincronización

- **Monitor**: Lock exclusivo (base de lock en C#)
- **Mutex**: Lock entre procesos
- **Semaphore / SemaphoreSlim**: Control de acceso limitado
- **ReaderWriterLockSlim**: Optimización para lecturas concurrentes
- **ManualResetEvent / AutoResetEvent**: Señalización entre threads
- **CountdownEvent**: Sincronización de múltiples operaciones
- **Barrier**: Sincronización de fases en algoritmos paralelos

#### Task Parallel Library (TPL)

El modelo asíncrono moderno:

**Task y Task<T>**:
- Representación de operación asíncrona
- Composición mediante continuaciones
- Propagación de excepciones
- Cancelación cooperativa mediante CancellationToken

**async/await**:
- Sintaxis simplificada para código asíncrono
- Transformación automática a máquina de estados
- Captura de contexto de sincronización
- Mejor rendimiento que callbacks

**Parallel**:
- `Parallel.For`: Iteraciones paralelas
- `Parallel.ForEach`: Procesamiento paralelo de colecciones
- `Parallel.Invoke`: Ejecución paralela de acciones

**PLINQ (Parallel LINQ)**:
- Extensiones paralelas de LINQ
- Particionamiento automático de datos
- Agregación eficiente de resultados

#### Channels

Sistema moderno de comunicación entre productores y consumidores:
- Alternativa thread-safe a BlockingCollection
- Soporte para backpressure
- Optimizado para escenarios high-throughput

### System.Linq

Language Integrated Query para consultas sobre colecciones:

#### Operadores Estándar

**Filtrado**:
- Where: Filtrado por predicado
- OfType: Filtrado por tipo
- Distinct: Eliminación de duplicados

**Proyección**:
- Select: Transformación de elementos
- SelectMany: Aplanamiento de colecciones anidadas

**Ordenamiento**:
- OrderBy / OrderByDescending
- ThenBy / ThenByDescending

**Agrupamiento**:
- GroupBy: Agrupación por clave
- ToLookup: Índice multivalue

**Agregación**:
- Count / LongCount
- Sum / Average / Min / Max
- Aggregate: Agregación personalizada

**Operaciones de Conjuntos**:
- Union / Intersect / Except
- Concat: Concatenación

**Cuantificadores**:
- Any / All
- Contains

**Ejecución**:
- ToList / ToArray / ToDictionary
- First / FirstOrDefault
- Single / SingleOrDefault
- Last / LastOrDefault

#### Evaluación Diferida

LINQ utiliza evaluación lazy:
- Las consultas se construyen sin ejecutarse
- La ejecución ocurre al enumerar resultados
- Permite optimizaciones y composición eficiente

### System.Text.Json

Serialización JSON moderna y de alto rendimiento:

#### Características

- **Alto rendimiento**: Hasta 2x más rápido que Newtonsoft.Json
- **Bajo consumo de memoria**: Menor allocations
- **Span<T> basado**: Zero-allocation reads cuando es posible
- **Async support**: Serialización/deserialización asíncrona de streams

#### Personalización

- Source generators: Generación en tiempo de compilación
- Custom converters: Lógica personalizada de serialización
- Naming policies: camelCase, snake_case, etc.
- Ignorar propiedades: Condicional o global

### System.Net.Http

Cliente HTTP moderno:

#### HttpClient

Características clave:
- **Reutilizable**: Instancia única para toda la aplicación
- **Connection pooling**: Gestión eficiente de conexiones
- **Async-first**: API completamente asíncrona
- **Handlers**: Pipeline extensible de procesamiento

#### HttpClientFactory

Patrón recomendado en .NET 10:
- Named clients: Clientes configurados por nombre
- Typed clients: Clientes fuertemente tipados
- Resilience: Integración con Polly para retry, circuit breaker
- Logging: Registro automático de requests/responses

### System.Text.RegularExpressions

Expresiones regulares optimizadas:

#### Source Generators

.NET 10 introduce generación en compilación:
- Sin overhead de parsing en runtime
- Mejor rendimiento
- Validación en tiempo de compilación
- IntelliSense mejorado

### Span<T> y Memory<T>

Abstracciones de memoria de alto rendimiento:

#### Span<T>

- Ref struct: Solo puede vivir en el stack
- Zero-allocation slicing: Vistas sin copiar datos
- Unificación: Arrays, strings, stackalloc, memoria nativa
- Seguro: Bounds checking en debug

#### Memory<T>

- Versión heap-friendly de Span<T>
- Puede almacenarse en campos y capturarse en lambdas
- Ideal para operaciones asíncronas

#### ReadOnlySpan<T> / ReadOnlyMemory<T>

Versiones inmutables para seguridad adicional.

---

## ASP.NET Core

### Introducción a ASP.NET Core

ASP.NET Core es el framework web de alto rendimiento y multiplataforma de Microsoft. En .NET 10, continúa su evolución como una de las plataformas web más rápidas y completas disponibles.

### Arquitectura de ASP.NET Core

#### Pipeline de Middleware

El corazón de ASP.NET Core es su pipeline de procesamiento de requests:

```
Request → Middleware 1 → Middleware 2 → ... → Middleware N → Response
           ↓              ↓                    ↓
          next()        next()              Endpoint
```

Características del pipeline:
- **Orden importa**: Los middlewares se ejecutan en secuencia
- **Corte de circuito**: Cualquier middleware puede terminar el pipeline
- **Bidireccional**: Procesamiento en request y response
- **Composable**: Fácil agregar, remover o reordenar middlewares

#### Middleware Común

Middlewares típicos en aplicaciones:

1. **Exception Handling**: Captura y manejo de excepciones
2. **HTTPS Redirection**: Forzar conexiones seguras
3. **Static Files**: Servir archivos estáticos (CSS, JS, imágenes)
4. **Routing**: Mapeo de URLs a endpoints
5. **Authentication**: Verificación de identidad
6. **Authorization**: Control de acceso
7. **CORS**: Cross-Origin Resource Sharing
8. **Response Compression**: Compresión gzip/brotli
9. **Response Caching**: Cache de respuestas HTTP

### Minimal APIs

.NET 10 potencia las Minimal APIs introducidas en .NET 6:

#### Características

- **Menos ceremonia**: Sin controladores ni clases adicionales
- **Route handlers**: Funciones lambda o métodos locales
- **Performance**: Overhead mínimo
- **Filtros**: Procesamiento pre/post endpoint
- **OpenAPI**: Generación automática de documentación

#### Escenarios Ideales

- Microservicios ligeros
- APIs simples
- Prototipado rápido
- Serverless functions

### MVC (Model-View-Controller)

Para aplicaciones más complejas, MVC proporciona estructura:

#### Controladores

Clases que organizan la lógica de endpoints relacionados:

- **Action Methods**: Métodos públicos que representan endpoints
- **Routing**: Mapeo basado en convenciones o atributos
- **Model Binding**: Mapeo automático de datos de request a parámetros
- **Validation**: Validación automática de modelos

#### Vistas (Views)

Templates Razor para generación de HTML:

- **Razor Syntax**: Mezcla de C# y HTML
- **Layouts**: Templates maestros compartidos
- **Partial Views**: Componentes reutilizables
- **View Components**: Componentes con lógica compleja
- **Tag Helpers**: Sintaxis amigable para generación de HTML

#### Modelos (Models)

Representación de datos y lógica de negocio:

- **View Models**: Datos específicos para vistas
- **Data Annotations**: Validación declarativa
- **Binding**: Mapeo bidireccional vista-modelo

### Web API

ASP.NET Core excede en la creación de APIs RESTful:

#### Content Negotiation

Respuestas en múltiples formatos:
- JSON (por defecto)
- XML
- Protobuf
- Formatos personalizados

#### Versionado de APIs

Estrategias soportadas:
- URL path: `/api/v1/products`
- Query string: `/api/products?api-version=1.0`
- Header: `api-version: 1.0`
- Media type: `application/json; v=1.0`

#### OpenAPI (Swagger)

Documentación automática de APIs:
- Especificación OpenAPI 3.0
- UI interactiva con Swagger UI
- Generación de clientes automática
- Source generators en .NET 10

### Inyección de Dependencias

DI es fundamental en ASP.NET Core:

#### Lifetimes

- **Transient**: Nueva instancia cada vez
- **Scoped**: Instancia por request
- **Singleton**: Instancia única para toda la aplicación

#### Patrones Avanzados

- **Factory pattern**: Creación compleja de instancias
- **Keyed services**: Múltiples implementaciones por clave
- **Service locator pattern**: Resolución dinámica
- **Decoradores**: Wrapping de servicios existentes

### Configuración

Sistema flexible y jerárquico:

#### Fuentes de Configuración

- **appsettings.json**: Configuración base
- **appsettings.{Environment}.json**: Por entorno
- **Environment variables**: Variables del sistema
- **Command line**: Argumentos de línea de comandos
- **Azure Key Vault**: Secretos en la nube
- **User secrets**: Desarrollo local seguro

#### Options Pattern

Configuración fuertemente tipada:
- IOptions<T>: Snapshot en construcción
- IOptionsSnapshot<T>: Recarga por request
- IOptionsMonitor<T>: Notificación de cambios

### Autenticación y Autorización

#### Autenticación

Esquemas soportados:
- **Cookie Authentication**: Para aplicaciones web tradicionales
- **JWT Bearer**: Para APIs y SPAs
- **OAuth 2.0 / OpenID Connect**: Integración con proveedores externos
- **Certificate Authentication**: Para servicios de machine-to-machine
- **Windows Authentication**: En entornos corporativos

#### Autorización

Control granular de acceso:
- **Role-based**: Por roles de usuario
- **Claims-based**: Por claims específicos
- **Policy-based**: Requisitos complejos personalizados
- **Resource-based**: Dependiente del recurso accedido

### SignalR

Comunicación en tiempo real:

#### Características

- **WebSockets**: Cuando está disponible
- **Fallbacks**: Server-Sent Events, Long Polling
- **Hubs**: Abstracción de alto nivel
- **Groups**: Broadcasting a subconjuntos de clientes
- **Backplane**: Escalamiento con Redis, Azure Service Bus

#### Escenarios

- Chats
- Dashboards en tiempo real
- Notificaciones push
- Juegos multiplayer
- Colaboración en tiempo real

### gRPC

Framework RPC de alto rendimiento:

#### Ventajas

- **Binario**: Protocol Buffers para eficiencia
- **HTTP/2**: Multiplexing, server push
- **Streaming**: Unidireccional y bidireccional
- **Contracts**: Schema-first con .proto files
- **Cross-platform**: Clientes para múltiples lenguajes

#### Tipos de Servicios

- **Unary**: Request-response simple
- **Server streaming**: Un request, múltiples responses
- **Client streaming**: Múltiples requests, una response
- **Bidirectional streaming**: Stream completo en ambas direcciones

### Health Checks

Monitoreo de salud de aplicaciones:

#### Tipos de Checks

- **Liveness**: ¿Está viva la aplicación?
- **Readiness**: ¿Está lista para tráfico?
- **Startup**: ¿Completó la inicialización?

#### Integraciones

- Database connectivity
- External services availability
- Disk space
- Memory usage
- Custom logic

### Caching

Estrategias de cache para performance:

#### In-Memory Caching

- Cache en proceso
- Ideal para datos compartidos frecuentemente accedidos
- Configuración de expiración absoluta/sliding

#### Distributed Caching

Proveedores soportados:
- **Redis**: Popular y de alto rendimiento
- **NCache**: Enterprise-grade
- **SQL Server**: Para simplificar infraestructura

#### Response Caching

- Cache de respuestas HTTP completas
- Headers de cache HTTP
- Vary by query string, headers, etc.

### Razor Pages

Modelo simplificado para páginas web:

#### Características

- **Page-centric**: Un archivo .cshtml por página
- **PageModel**: Code-behind opcional
- **Routing**: Basado en estructura de carpetas
- **Handlers**: Métodos OnGet, OnPost, etc.

### Blazor

Aplicaciones web con C# en lugar de JavaScript:

#### Blazor Server

- Rendering en servidor
- Conexión SignalR permanente
- Estado en servidor
- Latencia de red en cada interacción

#### Blazor WebAssembly

- Ejecución en el navegador
- Descarga inicial mayor
- Sin latencia después de carga
- Puede funcionar offline

#### Blazor Hybrid

En .NET 10:
- Combinación de Server y WebAssembly
- Renderizado incremental
- Streaming rendering
- Enhanced navigation

---

## Entity Framework Core

### Introducción a EF Core

Entity Framework Core es el ORM (Object-Relational Mapper) moderno de Microsoft, reescrito desde cero para ser ligero, extensible y multiplataforma.

### Arquitectura de EF Core

#### Componentes Principales

1. **DbContext**: Sesión con la base de datos
2. **DbSet<T>**: Colección de entidades de tipo T
3. **Modelo**: Mapeo entre objetos y tablas
4. **Providers**: Adaptadores para diferentes bases de datos
5. **Migrations**: Sistema de control de versiones de esquema

### Proveedores de Bases de Datos

EF Core soporta múltiples motores:

- **SQL Server / Azure SQL**: Provider oficial de Microsoft
- **PostgreSQL**: Popular en aplicaciones open source
- **MySQL / MariaDB**: Ampliamente usado en web
- **SQLite**: Ideal para desarrollo y aplicaciones móviles
- **Oracle**: Para entornos empresariales
- **Cosmos DB**: Base de datos NoSQL de Azure
- **In-Memory**: Para testing

### Modelado

#### Code First

Definición de modelo mediante clases C#:

**Convenciones**:
- Nombres de tabla derivan del DbSet
- Primary keys detectadas automáticamente (Id, [EntityName]Id)
- Foreign keys por propiedades de navegación
- String mapeado a nvarchar(max), int a int, etc.

**Data Annotations**:
Atributos para refinar el mapeo:
- [Key]: Especificar primary key
- [Required]: Columna NOT NULL
- [MaxLength]: Longitud máxima
- [Column]: Nombre de columna personalizado
- [Table]: Nombre de tabla personalizado
- [ForeignKey]: Especificar foreign key
- [Index]: Crear índices

**Fluent API**:
Configuración programática en OnModelCreating:
- Mapeo complejo de relaciones
- Value conversions
- Owned types
- Table splitting
- Query filters
- Seed data

#### Database First

Generación de modelo desde base de datos existente:
- Scaffolding mediante dotnet ef dbcontext scaffold
- Regeneración cuando el esquema cambia
- Personalización mediante partial classes

### Consultas

#### LINQ to Entities

Consultas expresadas en C# y traducidas a SQL:

**Evaluación del Servidor**:
Expresiones traducibles a SQL se ejecutan en la BD:
- Where, Select, OrderBy, GroupBy
- Join, Include, ThenInclude
- Count, Sum, Average, Min, Max
- Skip, Take (paginación)

**Evaluación del Cliente** (evitar):
Expresiones no traducibles ejecutan en memoria:
- Funciones C# no mapeadas
- Lógica compleja personalizada

#### Loading Strategies

**Eager Loading**:
```csharp
// Include para cargar entidades relacionadas
context.Orders.Include(o => o.Customer)
               .Include(o => o.OrderItems)
               .ToList();
```

**Lazy Loading**:
- Carga automática al acceder propiedades de navegación
- Requiere proxies o inyección de ILazyLoader
- Riesgo de N+1 queries

**Explicit Loading**:
```csharp
// Carga manual bajo demanda
context.Entry(order).Collection(o => o.OrderItems).Load();
```

**Select Loading** (recomendado):
```csharp
// Proyección a DTOs
context.Orders.Select(o => new OrderDto {
    OrderId = o.Id,
    CustomerName = o.Customer.Name
}).ToList();
```

### Change Tracking

EF Core rastrea cambios en entidades:

#### Estados de Entidad

- **Added**: Nueva entidad a insertar
- **Modified**: Entidad existente con cambios
- **Deleted**: Entidad marcada para borrado
- **Unchanged**: Sin cambios desde carga
- **Detached**: No rastreada por el contexto

#### SaveChanges

Proceso al guardar:
1. DetectChanges: Identifica modificaciones
2. Genera comandos SQL apropiados
3. Abre transacción
4. Ejecuta comandos
5. Actualiza valores generados por BD
6. Commit

### Migraciones

Sistema de control de versiones para esquema:

#### Flujo de Trabajo

1. **Crear migración**: `dotnet ef migrations add MigrationName`
2. **Revisar código generado**: Up y Down methods
3. **Aplicar a BD**: `dotnet ef database update`
4. **Revertir si necesario**: `dotnet ef database update PreviousMigration`

#### Estrategias de Despliegue

- **Desarrollo**: Automático en startup
- **Staging/Producción**: Scripts SQL generados manualmente
- **CI/CD**: Integración en pipeline de deployment

### Rendimiento

#### Optimizaciones

**AsNoTracking**:
```csharp
// Para queries read-only
context.Products.AsNoTracking().ToList();
```

**Compiled Queries**:
Precompilación de queries frecuentes para evitar re-parsing.

**Batch Operations**:
- Múltiples operaciones en un solo roundtrip
- Mejor performance en inserts/updates masivos

**Raw SQL**:
```csharp
// Para queries complejas no expresables en LINQ
context.Products.FromSqlRaw("SELECT * FROM Products WHERE ...").ToList();
```

**Stored Procedures**:
Mapeo de procedimientos almacenados.

#### Connection Resiliency

Reintentos automáticos en fallas transitorias:
- Configurable por provider
- Estrategia de backoff exponencial
- Logging de reintentos

### Características Avanzadas

#### Value Conversions

Transformación entre representación de código y BD:
- Enums a strings
- Encriptación de datos sensibles
- JSON serialization de objetos complejos

#### Shadow Properties

Propiedades en modelo sin equivalente en clase:
- Útil para auditoría (CreatedDate, ModifiedDate)
- Soft deletes

#### Owned Types

Objetos de valor que forman parte de una entidad:
- Address, Money, DateRange
- Pueden mapearse a misma tabla o tabla separada

#### Table Splitting

Múltiples entidades mapeadas a la misma tabla.

#### Global Query Filters

Filtros automáticos en todas las queries:
- Tenant isolation en aplicaciones multi-tenant
- Soft deletes (IsDeleted = false)

#### Interceptors

Hooks en el pipeline de EF Core:
- Modificar comandos SQL antes de ejecución
- Logging personalizado
- Auditoría

---

## Blazor

### Introducción a Blazor

Blazor permite construir aplicaciones web interactivas usando C# en lugar de JavaScript. Comparte código entre cliente y servidor, aprovecha el ecosistema .NET completo, y ofrece excelente productividad.

### Modelos de Hosting

#### Blazor Server

**Características**:
- Rendering en servidor via SignalR
- Tamaño de descarga mínimo
- Ejecución completa en servidor
- Acceso directo a recursos del servidor

**Ventajas**:
- Inicio rápido
- Funciona en navegadores antiguos
- Código protegido en servidor
- Debugging completo

**Desventajas**:
- Requiere conexión constante
- Latencia en cada interacción
- Escalamiento de SignalR connections
- No funciona offline

#### Blazor WebAssembly

**Características**:
- Descarga .NET runtime y app al navegador
- Ejecución completamente en cliente
- Funciona offline (con service workers)
- Puede ser PWA completa

**Ventajas**:
- Sin latencia de red después de carga
- Escalamiento simple (CDN)
- Rica experiencia offline
- Reduce carga del servidor

**Desventajas**:
- Descarga inicial grande (>2MB)
- Tiempo de inicio más lento
- Sin acceso directo a recursos del servidor
- Limitaciones de WebAssembly

#### Blazor United (.NET 10)

Modelo híbrido que combina lo mejor:

**Server-Side Rendering (SSR)**:
- Primera carga renderizada en servidor
- HTML completo enviado al cliente
- SEO friendly

**Interactive Server**:
- Componentes específicos con interactividad server
- SignalR para componentes dinámicos

**Interactive WebAssembly**:
- Componentes descargados y ejecutados en cliente
- Máxima interactividad sin latencia

**Streaming Rendering**:
- Partes de la página se renderizan progresivamente
- Mejor percepción de velocidad

**Enhanced Navigation**:
- Navegación sin full page refresh
- Fetch de HTML vía JavaScript

### Componentes

#### Anatomía de un Componente

Archivo .razor combinando markup y código:

```razor
@page "/counter"
@rendermode InteractiveServer

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
```

#### Ciclo de Vida

Métodos de lifecycle hooks:

1. **SetParametersAsync**: Parámetros recibidos
2. **OnInitialized / OnInitializedAsync**: Inicialización
3. **OnParametersSet / OnParametersSetAsync**: Después de parámetros
4. **OnAfterRender / OnAfterRenderAsync**: Después de rendering
5. **Dispose / DisposeAsync**: Cleanup

#### Parámetros

Comunicación padre-hijo:

```razor
@code {
    [Parameter]
    public string Title { get; set; }
    
    [Parameter]
    public EventCallback<int> OnValueChanged { get; set; }
}
```

#### Cascading Parameters

Datos que fluyen por el árbol de componentes:

```razor
<CascadingValue Value="@theme">
    <!-- Todos los componentes hijos pueden acceder -->
</CascadingValue>
```

### Data Binding

#### One-Way Binding

```razor
<p>@message</p>
<input value="@message" />
```

#### Two-Way Binding

```razor
<input @bind="message" />
<input @bind="startDate" @bind:format="yyyy-MM-dd" />
```

#### Event Handling

```razor
<button @onclick="HandleClick">Click</button>
<input @oninput="HandleInput" />
<form @onsubmit="HandleSubmit">
```

### Formularios y Validación

#### EditForm

Componente para formularios:

```razor
<EditForm Model="@model" OnValidSubmit="HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />
    
    <InputText @bind-Value="model.Name" />
    <ValidationMessage For="@(() => model.Name)" />
    
    <button type="submit">Submit</button>
</EditForm>
```

#### Validación

- **Data Annotations**: Atributos en el modelo
- **FluentValidation**: Validación compleja
- **Custom validators**: Lógica personalizada

### JavaScript Interop

Comunicación bidireccional con JavaScript:

#### Desde C# llamar JavaScript

```csharp
await JSRuntime.InvokeVoidAsync("alert", "Hello from C#!");
var result = await JSRuntime.InvokeAsync<string>("myJsFunction", arg1, arg2);
```

#### Desde JavaScript llamar C#

```javascript
DotNet.invokeMethodAsync('MyAssembly', 'MyMethod', arg1, arg2);
```

### Estado de la Aplicación

#### State Management

Opciones para gestionar estado:

**Cascading Parameters**:
- Simple para datos compartidos por árbol

**Dependency Injection**:
- Servicios singleton/scoped
- Observable pattern con eventos

**State Container Pattern**:
- Clase dedicada para estado
- Notificación de cambios
- Subscription pattern

**Fluxor**:
- Redux-like state management
- Unidirectional data flow
- Time-travel debugging

### Autenticación y Autorización

#### AuthenticationStateProvider

Abstracción para estado de autenticación:
- JWT tokens
- Cookies
- OAuth flows

#### AuthorizeView

Componente para UI basada en autorización:

```razor
<AuthorizeView Roles="Admin">
    <Authorized>
        <p>Admin content</p>
    </Authorized>
    <NotAuthorized>
        <p>You're not authorized</p>
    </NotAuthorized>
</AuthorizeView>
```

### Rendimiento

#### Virtualization

Rendering eficiente de listas grandes:

```razor
<Virtualize Items="@items" Context="item">
    <div>@item.Name</div>
</Virtualize>
```

#### Lazy Loading

Carga de assemblies bajo demanda:
- Reduce tamaño de descarga inicial
- Assemblies cargados cuando se necesitan

#### Prerendering

Renderizado inicial en servidor para mejor UX y SEO.

---

## MAUI (.NET Multi-platform App UI)

### Introducción a MAUI

.NET MAUI es el framework de Microsoft para crear aplicaciones nativas multiplataforma desde una única base de código. Evolución de Xamarin.Forms, ahora completamente integrado en .NET 10.

### Plataformas Soportadas

- **Android**: Android 5.0 (API 21) y superiores
- **iOS**: iOS 11 y superiores
- **macOS**: macOS 10.15 y superiores (Mac Catalyst)
- **Windows**: Windows 10 1809 y superiores (WinUI 3)

### Arquitectura

#### Estructura de Proyecto Único

Un solo proyecto para todas las plataformas:

```
MyApp/
├── Platforms/
│   ├── Android/
│   ├── iOS/
│   ├── MacCatalyst/
│   └── Windows/
├── Resources/
│   ├── Images/
│   ├── Fonts/
│   └── Styles/
├── Views/
├── ViewModels/
└── Models/
```

#### Multi-targeting

El proyecto compila para todas las plataformas:
- Código compartido: 95%+ de la aplicación
- Código específico: Solo cuando es absolutamente necesario

### Controles y Layouts

#### Controles Básicos

- **Label**: Texto
- **Button**: Botones interactivos
- **Entry**: Entrada de texto de una línea
- **Editor**: Entrada de texto multilínea
- **CheckBox**: Casilla de verificación
- **Switch**: Toggle
- **Slider**: Rango numérico
- **Stepper**: Incremento/decremento
- **DatePicker / TimePicker**: Selección de fecha/hora
- **Picker**: Lista desplegable

#### Controles de Colecciones

- **CollectionView**: Lista eficiente con virtualización
- **CarouselView**: Carousel de elementos
- **ListView**: Lista tradicional (legacy)

#### Layouts

- **StackLayout**: Apilamiento vertical u horizontal
- **Grid**: Layout en cuadrícula
- **AbsoluteLayout**: Posicionamiento absoluto
- **FlexLayout**: Flexbox-like layout
- **ScrollView**: Contenido desplazable

### Navegación

#### Navigation Patterns

**Shell Navigation**:
- URI-based navigation
- Flyout menu
- Tabs
- Routes registradas

**NavigationPage**:
- Stack-based navigation
- Barra de navegación automática

**TabbedPage**:
- Tabs en la parte inferior (iOS) o superior (Android)

**FlyoutPage**:
- Menu lateral (hamburger menu)

### Data Binding

#### MVVM Pattern

Patrón arquitectónico recomendado:

- **Model**: Datos y lógica de negocio
- **View**: XAML UI
- **ViewModel**: Lógica de presentación y estado

#### Binding Context

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             x:Class="MyApp.MainPage">
    <StackLayout>
        <Label Text="{Binding Title}" />
        <Button Command="{Binding SaveCommand}" />
    </StackLayout>
</ContentPage>
```

#### INotifyPropertyChanged

Notificación de cambios en propiedades:
- Binding automático se actualiza
- CommunityToolkit.Mvvm simplifica implementación

### Recursos y Estilos

#### Recursos

Definición centralizada:
- Colores
- Fuentes
- Strings
- Estilos

#### Estilos

XAML styling similar a CSS:
- Implicit styles: Aplicados automáticamente por tipo
- Explicit styles: Requieren referencia explícita
- Style inheritance: Reutilización vía BasedOn

### Plataform Specifics

#### Características Específicas

Acceso a características nativas:

**APIs Abstractas**:
- Geolocation
- Camera
- File system
- Connectivity
- Battery
- Device info
- Permissions

**Conditional Compilation**:
```csharp
#if ANDROID
    // Código específico de Android
#elif IOS
    // Código específico de iOS
#endif
```

**Platform Handlers**:
Personalización profunda de controles por plataforma.

### Gráficos

#### Microsoft.Maui.Graphics

Abstracción de gráficos 2D multiplataforma:
- Drawing API consistente
- Renderizado nativo en cada plataforma
- Canvas para dibujo personalizado

### Acceso a Datos

#### Opciones de Persistencia

**SQLite.NET**:
- Base de datos local
- Cross-platform
- ORM ligero

**Preferences**:
- Key-value storage
- Configuración simple

**Secure Storage**:
- Almacenamiento encriptado
- Credenciales y secretos

**File System**:
- Acceso a archivos locales
- App sandbox

### Integración con Backend

#### HttpClient

Consumo de APIs REST:
- Serialización JSON
- Autenticación
- Headers personalizados

#### SignalR

Comunicación en tiempo real con servidor.

#### gRPC

APIs de alto rendimiento.

### Pruebas

#### Unit Testing

Testing de ViewModels y lógica:
- xUnit, NUnit, MSTest
- Mocking con Moq

#### UI Testing

Pruebas de interfaz:
- Appium para multiplataforma
- Xamarin.UITest (legacy)

### Publicación

#### Android

- **Google Play Store**: Publicación a millones de usuarios
- **APK / AAB**: Formatos de distribución

#### iOS

- **App Store**: Revisión de Apple
- **TestFlight**: Beta testing

#### macOS

- **Mac App Store**: Distribución a usuarios Mac
- **Notarización**: Requerida para apps fuera del store

#### Windows

- **Microsoft Store**: Distribución en Windows
- **MSIX**: Instalador moderno

---

## Servicios en la Nube con Azure

### Introducción a Azure

Microsoft Azure es la plataforma en la nube que se integra perfectamente con .NET 10, ofreciendo servicios PaaS, IaaS y SaaS para hospedar, escalar y administrar aplicaciones.

### Compute Services

#### Azure App Service

PaaS para hospedar aplicaciones web:

**Características**:
- Escalamiento automático
- Deployment slots para staging
- CI/CD integrado
- Logging y monitoring
- Custom domains y SSL gratuito

**Planes**:
- Free/Shared: Para desarrollo y pruebas
- Basic: Apps de producción pequeñas
- Standard: Escalamiento y features avanzados
- Premium: Alto rendimiento y isolation
- Isolated: Dedicado en VNET

#### Azure Functions

Serverless compute para funciones:

**Triggers Soportados**:
- HTTP
- Timer
- Queue/Service Bus
- Blob Storage
- Event Hub
- Cosmos DB
- Event Grid

**Planes de Hosting**:
- Consumption: Pay-per-execution
- Premium: Always-on con VNet
- Dedicated: App Service Plan compartido

**Escenarios**:
- Microservicios
- Background processing
- Event-driven workflows
- APIs ligeras

#### Azure Container Instances (ACI)

Ejecución de contenedores sin orquestación:
- Inicio rápido
- Facturación por segundo
- Ideal para cargas batch

#### Azure Kubernetes Service (AKS)

Kubernetes administrado:
- Orquestación de contenedores a escala
- Control plane gratuito
- Integración con Azure services
- Auto-scaling de pods y nodos

### Storage Services

#### Azure Blob Storage

Almacenamiento de objetos:

**Tipos de Blobs**:
- Block blobs: Archivos generales
- Append blobs: Logs
- Page blobs: VHDs de VMs

**Tiers**:
- Hot: Acceso frecuente
- Cool: Acceso poco frecuente
- Archive: Almacenamiento a largo plazo

#### Azure Files

File shares SMB/NFS en la nube:
- Montables en Windows, Linux, macOS
- Replacement para file servers
- Azure File Sync para híbrido

#### Azure Queue Storage

Cola de mensajes simple:
- At-least-once delivery
- Hasta 500TB de mensajes
- Ideal para desacoplamiento

#### Azure Table Storage

NoSQL key-value store:
- Estructura flexible
- Bajo costo
- Alta disponibilidad

### Database Services

#### Azure SQL Database

Base de datos relacional como servicio:

**Modelos de Compra**:
- DTU: Recursos agrupados
- vCore: Control granular de CPU/memoria

**Tiers**:
- Basic: Desarrollo y pequeñas DBs
- Standard: Cargas de trabajo típicas
- Premium: Alto rendimiento
- Hyperscale: Hasta 100TB

**Características**:
- Backups automáticos
- Point-in-time restore
- Geo-replication
- Transparent Data Encryption
- Advanced Threat Protection

#### Azure Cosmos DB

Base de datos NoSQL distribuida globalmente:

**APIs**:
- SQL API: Documentos JSON con SQL queries
- MongoDB API: Compatibilidad con MongoDB
- Cassandra API: Compatibilidad con Cassandra
- Gremlin API: Grafos
- Table API: Key-value

**Características**:
- Replicación multi-región
- Latencia <10ms en P99
- Múltiples modelos de consistencia
- Escalamiento elástico
- SLAs líderes en la industria

#### Azure Database for PostgreSQL / MySQL

Bases de datos open source administradas:
- Versiones recientes siempre disponibles
- Alta disponibilidad incorporada
- Backups automáticos
- Escalamiento flexible

### Messaging Services

#### Azure Service Bus

Enterprise message broker:

**Características**:
- Queues: Point-to-point
- Topics: Pub/sub con filtros
- Sessions: Mensajes ordenados
- Dead-letter queues
- Duplicate detection
- Transactions

**Escenarios**:
- Integración enterprise
- Desacoplamiento de servicios
- Load leveling

#### Azure Event Hubs

Plataforma de streaming de Big Data:
- Millones de eventos por segundo
- Captura automática a storage
- Compatible con Apache Kafka
- Event sourcing a escala

#### Azure Event Grid

Routing de eventos:
- Reacción a eventos de Azure services
- Webhooks para notificaciones
- Filtrado y routing avanzado

### Networking

#### Azure Virtual Network (VNet)

Red privada en Azure:
- Subnets
- Network Security Groups
- VPN Gateway
- ExpressRoute
- Peering entre VNets

#### Azure Application Gateway

Load balancer de capa 7:
- SSL termination
- URL-based routing
- Web Application Firewall
- Autoscaling

#### Azure Front Door

CDN global y load balancing:
- Aceleración de aplicaciones web
- Failover automático
- SSL offload
- WAF integrado

### Identity and Security

#### Azure Active Directory (Entra ID)

Servicio de identidad:
- Single Sign-On
- Multi-Factor Authentication
- Conditional Access
- B2B / B2C scenarios
- OAuth 2.0 / OpenID Connect

#### Azure Key Vault

Gestión de secretos:
- Secrets: Strings, connection strings, passwords
- Keys: Claves criptográficas
- Certificates: Certificados SSL/TLS
- Hardware Security Modules (HSM)

### Monitoring and Management

#### Azure Monitor

Observabilidad completa:

**Application Insights**:
- APM para aplicaciones
- Distributed tracing
- Performance profiling
- Usage analytics
- Availability tests

**Log Analytics**:
- Logs centralizados
- Kusto Query Language (KQL)
- Alertas basadas en queries
- Dashboards personalizados

#### Azure DevOps

CI/CD y gestión de proyectos:

**Services**:
- Azure Repos: Git repositories
- Azure Pipelines: CI/CD
- Azure Boards: Work item tracking
- Azure Artifacts: Package management
- Azure Test Plans: Testing tools

### Integración con .NET 10

#### Azure SDKs para .NET

Bibliotecas modernas:
- Async/await first
- Dependency injection friendly
- Logging integrado
- Retry policies
- Distributed tracing

#### Configuration

Integración con App Configuration:
- Configuración centralizada
- Feature flags
- Key-value pairs dinámicos

#### Deployment

Opciones para .NET apps:
- Visual Studio publish
- Azure CLI
- GitHub Actions
- Azure Pipelines
- Docker containers

---

## Herramientas de Desarrollo

### Visual Studio 2022+

IDE completo de Microsoft:

#### Características Principales

**Productividad**:
- IntelliSense avanzado
- Code refactoring
- Code snippets
- Live Share para colaboración
- CodeLens para insights de código

**Debugging**:
- Breakpoints condicionales
- Edit and Continue
- Time Travel Debugging
- Remote debugging
- Performance profiling

**Testing**:
- Test Explorer
- Code Coverage
- Live Unit Testing
- IntelliTest para generación automática

**Extensiones**:
- Marketplace con miles de extensiones
- ReSharper para análisis avanzado
- GitLens para Git
- GitHub Copilot para AI assistance

### Visual Studio Code

Editor ligero y extensible:

#### Ventajas

- Multiplataforma (Windows, Linux, macOS)
- Inicio rápido
- Altamente personalizable
- Integrated terminal
- Git integrado

#### Extensiones para .NET

- **C# Dev Kit**: Soporte completo de C#
- **C#**: Syntax highlighting y IntelliSense
- **.NET Core Test Explorer**: Testing
- **NuGet Package Manager**: Gestión de paquetes
- **REST Client**: Testing de APIs

### .NET CLI

Herramienta de línea de comandos:

#### Comandos Principales

```bash
# Crear nuevo proyecto
dotnet new console|web|webapi|classlib|...

# Restaurar paquetes
dotnet restore

# Compilar
dotnet build

# Ejecutar
dotnet run

# Testing
dotnet test

# Publicar
dotnet publish -c Release

# Añadir paquete NuGet
dotnet add package PackageName

# Entity Framework
dotnet ef migrations add MigrationName
dotnet ef database update
```

#### Ventajas

- Cross-platform
- CI/CD friendly
- Scripting y automatización
- Consistente entre proyectos

### NuGet Package Manager

Repositorio de paquetes de .NET:

#### Uso

**Visual Studio**:
- UI gráfica para búsqueda e instalación
- Gestión visual de dependencias

**CLI**:
```bash
dotnet add package Newtonsoft.Json
dotnet remove package Newtonsoft.Json
dotnet list package
dotnet restore
```

**PackageReference**:
Formato moderno en .csproj:
```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
</ItemGroup>
```

#### Versionado Semántico

- Major.Minor.Patch (1.2.3)
- Breaking changes incrementan Major
- New features incrementan Minor
- Bug fixes incrementan Patch

### Git y GitHub

Control de versiones:

#### Git Flow

Estrategia de branching:
- main/master: Producción
- develop: Desarrollo
- feature/*: Nuevas características
- release/*: Preparación de release
- hotfix/*: Correcciones urgentes

#### GitHub Actions

CI/CD integrado:
- Workflows en YAML
- Triggers en push, PR, schedule
- Matrix builds para múltiples plataformas
- Marketplace de acciones reutilizables

### Docker

Contenedorización de aplicaciones:

#### Dockerfile para .NET

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY ["MyApp.csproj", "./"]
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

#### Docker Compose

Orquestación local:
- Múltiples servicios (app, database, cache)
- Networking automático
- Volumes para persistencia

### Debugging Tools

#### Visual Studio Debugger

Capacidades avanzadas:
- Breakpoints con condiciones y acciones
- DataTips para inspección rápida
- Watch windows
- Call Stack
- Immediate window para evaluar expresiones

#### dotnet-trace

Recolección de traces de rendimiento:
```bash
dotnet trace collect --process-id <PID>
```

#### dotnet-dump

Captura y análisis de dumps:
```bash
dotnet dump collect --process-id <PID>
dotnet dump analyze dump.dmp
```

#### dotnet-counters

Monitoreo en tiempo real:
```bash
dotnet counters monitor --process-id <PID>
```

### Code Analyzers

Análisis estático de código:

#### Roslyn Analyzers

- Detección de problemas en tiempo de escritura
- Sugerencias de refactoring
- Aplicación de convenciones de código
- Custom analyzers para reglas específicas

#### StyleCop

Enforcement de estilo de código.

#### SonarAnalyzer

Análisis de calidad y seguridad.

---

## Patrones y Mejores Prácticas

### Principios SOLID

#### Single Responsibility Principle (SRP)

Una clase debe tener una sola razón para cambiar:
- Cohesión alta
- Clases pequeñas y focalizadas
- Facilita testing y mantenimiento

#### Open/Closed Principle (OCP)

Abierto para extensión, cerrado para modificación:
- Extensibilidad sin modificar código existente
- Uso de abstracciones
- Polimorfismo y herencia

#### Liskov Substitution Principle (LSP)

Los subtipos deben ser sustituibles por sus tipos base:
- Contratos consistentes
- Sin sorpresas en herencia
- Precondiciones no más fuertes, postcondiciones no más débiles

#### Interface Segregation Principle (ISP)

Los clientes no deben depender de interfaces que no usan:
- Interfaces pequeñas y específicas
- Evitar "fat interfaces"
- Composición de interfaces

#### Dependency Inversion Principle (DIP)

Depender de abstracciones, no de concreciones:
- Inyección de dependencias
- Inversión de control
- Facilita testing con mocks

### Patrones de Diseño

#### Creacionales

**Singleton**:
- Instancia única en toda la aplicación
- Acceso global controlado
- Cuidado con multi-threading

**Factory Method**:
- Creación de objetos sin especificar clase exacta
- Delegación de instanciación a subclases

**Abstract Factory**:
- Familias de objetos relacionados
- Sin especificar clases concretas

**Builder**:
- Construcción paso a paso
- Diferentes representaciones del mismo objeto

**Prototype**:
- Clonación de objetos
- Evitar construcción costosa

#### Estructurales

**Adapter**:
- Compatibilidad entre interfaces incompatibles
- Wrapping de clases existentes

**Decorator**:
- Añadir responsabilidades dinámicamente
- Alternativa flexible a herencia

**Facade**:
- Interface simplificada a sistema complejo
- Reducción de acoplamiento

**Proxy**:
- Control de acceso a objeto
- Lazy initialization, caching, logging

**Composite**:
- Tratar objetos individuales y composiciones uniformemente
- Estructuras de árbol

#### Comportamiento

**Strategy**:
- Familia de algoritmos intercambiables
- Selección en runtime

**Observer**:
- Notificación de cambios
- Pub/sub pattern

**Command**:
- Encapsulación de requests como objetos
- Undo/redo, queueing

**Template Method**:
- Estructura de algoritmo con steps personalizables
- Hook methods

**Chain of Responsibility**:
- Cadena de handlers
- Desacoplamiento de sender y receiver

### Patrones Arquitectónicos

#### Layered Architecture

Organización en capas:
- Presentation Layer
- Business Logic Layer
- Data Access Layer
- Database Layer

Ventajas:
- Separación de concerns
- Testing por capas
- Mantenibilidad

#### Clean Architecture

Independencia de frameworks y tecnología:

**Capas**:
1. **Entities**: Lógica de negocio core
2. **Use Cases**: Casos de uso de la aplicación
3. **Interface Adapters**: Controladores, presenters
4. **Frameworks & Drivers**: UI, DB, web frameworks

**Principios**:
- Dependencias apuntan hacia adentro
- Core independiente de infraestructura
- Testabilidad máxima

#### Hexagonal Architecture (Ports & Adapters)

Aplicación en el centro:
- Ports: Interfaces que define la aplicación
- Adapters: Implementaciones que conectan con exterior
- Facilita cambio de tecnologías

#### Microservices

Aplicación como conjunto de servicios pequeños:

**Características**:
- Deployados independientemente
- Organizados por business capabilities
- Descentralización de datos
- Comunicación vía APIs

**Ventajas**:
- Escalamiento independiente
- Tecnologías heterogéneas
- Resiliencia
- Equipos autónomos

**Desafíos**:
- Complejidad operacional
- Consistencia de datos
- Testing end-to-end
- Debugging distribuido

#### Event-Driven Architecture

Comunicación mediante eventos:

**Patrones**:
- **Event Notification**: Notificación simple de que algo ocurrió
- **Event-Carried State Transfer**: Evento contiene datos completos
- **Event Sourcing**: Estado actual derivado de secuencia de eventos
- **CQRS**: Separación de comandos y queries

### Repository Pattern

Abstracción de acceso a datos:

**Ventajas**:
- Desacoplamiento de lógica de negocio y persistencia
- Testing con repositorios mock
- Cambio de proveedor de datos

**Implementación**:
- Interface genérica: IRepository<T>
- Implementaciones específicas por entidad
- Unit of Work para transaccionalidad

### Unit of Work Pattern

Coordinación de múltiples repositorios:
- Transacciones entre repositorios
- Tracking de cambios centralizado
- Commit único al finalizar

### Specification Pattern

Lógica de negocio encapsulada:
- Criteria reutilizables
- Composición de especificaciones
- Queries complejas legibles

### CQRS (Command Query Responsibility Segregation)

Separación de lecturas y escrituras:

**Ventajas**:
- Optimización independiente
- Escalamiento asimétrico
- Modelos diferentes para read/write

**Cuando usar**:
- Dominios complejos
- Alta carga de lecturas vs escrituras
- Necesidad de optimizaciones específicas

### Event Sourcing

Persistencia de eventos en lugar de estado:

**Ventajas**:
- Auditoría completa
- Time travel: Estado en cualquier punto del tiempo
- Event-driven integrations

**Desafíos**:
- Complejidad
- Evolución de eventos
- Proyecciones para queries

---

## Seguridad

### Autenticación

#### ASP.NET Core Identity

Sistema completo de membresía:

**Características**:
- Gestión de usuarios y roles
- Password hashing con PBKDF2
- Two-Factor Authentication
- Account lockout
- Email confirmation
- Password recovery
- External login providers (Google, Facebook, Microsoft, etc.)

**Personalización**:
- Custom user properties
- Custom stores
- UI totalmente customizable

#### JWT (JSON Web Tokens)

Tokens para APIs:

**Estructura**:
- Header: Algoritmo y tipo
- Payload: Claims
- Signature: Verificación de integridad

**Ventajas**:
- Stateless
- Escalabilidad
- Cross-domain

**Seguridad**:
- HTTPS obligatorio
- Expiración corta
- Refresh tokens para renovación
- Validación de issuer y audience

#### OAuth 2.0 y OpenID Connect

Protocolos estándar:

**OAuth 2.0**:
- Authorization framework
- Delegación de acceso
- Flujos: Authorization Code, Implicit, Client Credentials, Resource Owner Password

**OpenID Connect**:
- Capa de identidad sobre OAuth 2.0
- ID Token con claims de usuario
- UserInfo endpoint

**IdentityServer**:
Framework para implementar OAuth 2.0 y OIDC en .NET.

### Autorización

#### Claims-Based Authorization

Autorización basada en atributos de usuario:
- Claims: Key-value pairs de información
- Flexible y extensible
- Claims transformation

#### Policy-Based Authorization

Policies con requisitos complejos:

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("AtLeast21", policy =>
        policy.Requirements.Add(new MinimumAgeRequirement(21)));
});
```

#### Resource-Based Authorization

Autorización que depende del recurso:
- Validación en runtime
- Acceso a datos específicos del recurso
- IAuthorizationService para evaluación

### Seguridad de Datos

#### Encriptación

**Data at Rest**:
- Transparent Data Encryption en SQL Server
- Azure Storage Service Encryption
- Field-level encryption con DataProtection API

**Data in Transit**:
- HTTPS obligatorio
- TLS 1.2+
- Certificate pinning en móviles

#### Data Protection API

Sistema de protección de datos de ASP.NET Core:
- Key management automático
- Protección de cookies, tokens
- Rotación de keys
- Persistencia en Azure Key Vault, Redis, filesystem

### Protección Contra Ataques

#### Cross-Site Scripting (XSS)

**Prevención**:
- Output encoding automático en Razor
- Content Security Policy headers
- HttpOnly cookies
- Validación de input

#### Cross-Site Request Forgery (CSRF)

**Prevención**:
- Anti-forgery tokens automáticos
- SameSite cookies
- Verificación de origin header

#### SQL Injection

**Prevención**:
- Parametrized queries (siempre)
- ORM (Entity Framework Core)
- Input validation
- Principio de least privilege en DB

#### Open Redirect

**Prevención**:
- Validación de URLs de redirect
- Whitelist de destinos permitidos

### Secrets Management

#### User Secrets

Para desarrollo local:
- Secretos fuera del código fuente
- Por proyecto
- No commitear a control de versiones

#### Environment Variables

Para diferentes entornos:
- Configuración específica de ambiente
- Sobrescritura de appsettings

#### Azure Key Vault

Para producción:
- Gestión centralizada de secretos
- Rotación automática
- Auditoría de accesos
- HSM-backed keys

### HTTPS y Certificados

#### Enforcement

- HTTPS Redirection middleware
- HSTS (HTTP Strict Transport Security)
- Certificate pinning

#### Let's Encrypt

Certificados SSL/TLS gratuitos:
- Renovación automática
- Wildcard certificates

### Logging y Auditoría

#### Security Logging

Eventos a registrar:
- Intentos de login (exitosos y fallidos)
- Cambios de permisos
- Acceso a recursos sensibles
- Cambios en configuración de seguridad

#### Compliance

Estándares y regulaciones:
- GDPR: Privacidad de datos en EU
- HIPAA: Información de salud en US
- PCI DSS: Datos de tarjetas de crédito
- SOC 2: Controles de seguridad

### Security Headers

Headers HTTP de seguridad:

- **Content-Security-Policy**: Control de recursos cargados
- **X-Frame-Options**: Prevención de clickjacking
- **X-Content-Type-Options**: Prevención de MIME sniffing
- **Strict-Transport-Security**: Forzar HTTPS
- **Referrer-Policy**: Control de información de referrer

### Dependencias Seguras

#### Actualización de Paquetes

- Monitoreo de vulnerabilidades
- GitHub Dependabot
- Snyk
- OWASP Dependency Check

#### Supply Chain Security

- Firma de paquetes NuGet
- Verificación de integridad
- Repositorios privados para paquetes internos

---

## Rendimiento y Optimización

### Profiling y Diagnóstico

#### Herramientas

**Visual Studio Profiler**:
- CPU profiling
- Memory profiling
- Database profiling
- Performance insights

**dotnet-trace**:
- Recolección de eventos de performance
- Análisis en PerfView o Visual Studio

**BenchmarkDotNet**:
- Microbenchmarking preciso
- Comparación de implementaciones
- Detección de regresiones

### Optimización de Memoria

#### Reducción de Allocations

**Span<T> y Memory<T>**:
- Zero-allocation string processing
- Slicing sin copiar
- StackAlloc para buffers temporales

**Object Pooling**:
- Reutilización de objetos costosos
- ArrayPool<T> para arrays
- ObjectPool<T> para objetos personalizados

**Struct vs Class**:
- Structs para objetos pequeños (<16 bytes)
- Evitar boxing/unboxing
- Readonly structs

#### Gestión del GC

**Configuración**:
- Server GC para throughput
- Workstation GC para latencia
- Latency modes para control fino

**Generaciones**:
- Mantener objetos de vida larga en Gen2
- Evitar objetos de tamaño mediano (LOH threshold)

### Optimización de CPU

#### Algoritmos Eficientes

- Complejidad temporal apropiada
- Estructuras de datos óptimas
- Caching de resultados costosos

#### Paralelización

**Cuando usar**:
- Operaciones CPU-bound
- Datos independientes
- Overhead de paralelización justificado

**TPL**:
- Parallel.For/ForEach
- PLINQ
- Task.WhenAll para operaciones independientes

#### SIMD

Operaciones vectorizadas:
- System.Numerics.Vectors
- Hardware intrinsics
- Hasta 8x speedup en operaciones matemáticas

### Optimización de I/O

#### Async/Await

- Libera threads durante I/O
- Mejor escalabilidad
- Evitar async void
- ConfigureAwait(false) en libraries

#### Buffering

- BufferedStream para archivos
- Pipeline API para streaming eficiente
- Tamaño de buffer apropiado

#### Caching

**In-Memory Cache**:
- Datos frecuentemente accedidos
- Expiración configurable
- Eviction policies

**Distributed Cache**:
- Redis para múltiples instancias
- Consistencia entre servidores
- Session state distribuido

### Optimización de Base de Datos

#### Queries Eficientes

**EF Core**:
- AsNoTracking para read-only
- Select projections vs full entities
- Eager loading vs lazy loading
- Compiled queries
- Bulk operations

**Indexes**:
- Columnas frecuentemente filtradas
- Foreign keys
- Covering indexes
- Fill factor apropiado

**Query Optimization**:
- Evitar N+1 queries
- Batching de queries
- Paginación eficiente
- Desnormalización cuando apropiado

### Compilación AOT (Ahead-of-Time)

#### Native AOT

Compilación a código nativo:

**Ventajas**:
- Startup instantáneo
- Menor memoria
- Self-contained sin runtime
- Mejor para containers y serverless

**Limitaciones**:
- No soporta reflection dinámica
- Trimming agresivo
- Tamaño de binario mayor

#### Ready to Run (R2R)

Híbrido entre IL y nativo:
- Startup más rápido que JIT puro
- Mantiene flexibilidad de IL
- Tamaño mayor que IL puro

### HTTP Performance

#### HTTP/2

Ventajas sobre HTTP/1.1:
- Multiplexing: Múltiples requests en una conexión
- Server push
- Header compression
- Stream prioritization

#### gRPC

Alternativa de alto rendimiento:
- Protocol Buffers binarios
- HTTP/2 nativo
- Streaming eficiente

### CDN y Caching

#### Content Delivery Network

- Distribución geográfica
- Reducción de latencia
- Cache de assets estáticos
- DDoS protection

#### HTTP Caching

Headers apropiados:
- Cache-Control
- ETag
- Last-Modified
- Expires

### Connection Pooling

#### Database Connections

- Reuso de conexiones
- Configuración de pool size
- Connection lifetime

#### HTTP Connections

HttpClient reusable:
- Connection pooling automático
- DNS resolution caching
- Socket reuse

### Compression

#### Response Compression

- Gzip para compatibilidad
- Brotli para mejor ratio
- Dynamic vs static compression

#### Request Compression

Para upload de datos grandes.

---

## Testing y Calidad de Código

### Tipos de Pruebas

#### Unit Testing

Pruebas de unidades individuales:

**Frameworks**:
- **xUnit**: Recomendado por Microsoft
- **NUnit**: Popular y maduro
- **MSTest**: Integrado con Visual Studio

**Características**:
- Aislamiento mediante mocks
- Rápidas y deterministas
- Cobertura de código
- Test-driven development (TDD)

#### Integration Testing

Pruebas de componentes integrados:

**WebApplicationFactory**:
- Testing de APIs completas
- In-memory test server
- Database en memoria o contenedor

**Escenarios**:
- Database access
- External services
- Authentication/authorization

#### End-to-End Testing

Pruebas de flujos completos:

**Herramientas**:
- **Playwright**: Automatización de navegador
- **Selenium**: Estándar de industria
- **Cypress**: Enfocado en frontend

### Mocking

#### Moq

Framework de mocking popular:

**Capacidades**:
- Setup de métodos
- Verificación de llamadas
- Callback actions
- Sequences de comportamiento

**Ejemplo**:
```csharp
var mock = new Mock<IRepository>();
mock.Setup(r => r.GetById(It.IsAny<int>()))
    .Returns(new Entity());
```

#### NSubstitute

Sintaxis más fluida:
- Menos ceremonia
- Natural language-like

### Cobertura de Código

#### Herramientas

- **Coverlet**: Cross-platform
- **Visual Studio Code Coverage**: Enterprise edition
- **ReportGenerator**: Reportes visuales

#### Métricas

- Line coverage: % de líneas ejecutadas
- Branch coverage: % de ramas ejecutadas
- Objetivo típico: 80%+

### Test-Driven Development (TDD)

#### Ciclo Red-Green-Refactor

1. **Red**: Escribir test que falla
2. **Green**: Implementar mínimo para pasar
3. **Refactor**: Mejorar código manteniendo tests verdes

**Ventajas**:
- Diseño testable
- Especificación viviente
- Confianza en refactoring

### Behavior-Driven Development (BDD)

#### SpecFlow

Given-When-Then scenarios:

```gherkin
Given I am a logged in user
When I add an item to the cart
Then the cart should contain 1 item
```

Vinculación con código mediante step definitions.

### Property-Based Testing

#### FsCheck

Testing con generación automática de datos:
- Invariantes que deben cumplirse
- Cientos de casos generados automáticamente
- Shrinking para casos mínimos de falla

### Performance Testing

#### Benchmarking

BenchmarkDotNet para microbenchmarks:
- Comparación de implementaciones
- Detección de regresiones
- Estadísticas robustas

#### Load Testing

Herramientas:
- **k6**: Scripting en JavaScript
- **JMeter**: Java-based
- **Azure Load Testing**: Cloud-based

### Mutation Testing

#### Stryker.NET

Testing de calidad de tests:
- Muta el código intencionalmente
- Verifica que los tests detecten mutaciones
- Identifica tests débiles

### Code Quality

#### Static Analysis

**Roslyn Analyzers**:
- Análisis en tiempo de compilación
- Enforcement de convenciones
- Detección de code smells

**SonarQube**:
- Análisis exhaustivo
- Deuda técnica
- Security vulnerabilities
- Code duplications

#### Code Reviews

Mejores prácticas:
- Pull requests pequeños
- Descripción clara de cambios
- Automated checks antes de review
- Constructive feedback

#### Technical Debt

Gestión de deuda:
- Identificación sistemática
- Priorización
- Refactoring incremental
- Balance con features

### Continuous Integration

#### Pipeline de CI

Pasos típicos:
1. Checkout code
2. Restore dependencies
3. Build
4. Run tests
5. Code analysis
6. Package artifacts

#### GitHub Actions

Ejemplo de workflow:
```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-dotnet@v1
        with:
          dotnet-version: '10.0.x'
      - run: dotnet restore
      - run: dotnet build
      - run: dotnet test
```

### Continuous Deployment

#### Estrategias

**Blue-Green Deployment**:
- Dos entornos idénticos
- Switch instantáneo
- Rollback rápido

**Canary Deployment**:
- Despliegue gradual
- Monitoreo de errores
- Rollout o rollback

**Feature Flags**:
- Deployment vs release
- A/B testing
- Kill switches

---

## Conclusiones

### El Ecosistema .NET 10

.NET 10 representa la madurez de más de dos décadas de evolución en el desarrollo de software. Como versión LTS, ofrece estabilidad a largo plazo mientras incorpora las últimas innovaciones en rendimiento, seguridad y productividad.

### Fortalezas Clave

1. **Rendimiento de Clase Mundial**: Entre las plataformas más rápidas disponibles, con optimizaciones continuas en cada release

2. **Multiplataforma Real**: Verdadera portabilidad entre Windows, Linux, macOS, y dispositivos móviles

3. **Ecosistema Completo**: De microservicios a aplicaciones empresariales, de web a móvil, .NET lo abarca todo

4. **Herramientas Excepcionales**: Visual Studio, VS Code, y el CLI proporcionan experiencia de desarrollo de primer nivel

5. **Integración Cloud-Native**: Diseñado para la nube con soporte excepcional para containers, Kubernetes y Azure

6. **Comunidad y Soporte**: Open source con respaldo de Microsoft y comunidad global activa

### Casos de Uso Ideales

- **APIs y Microservicios**: ASP.NET Core con rendimiento excepcional
- **Aplicaciones Web Modernas**: Blazor para SPAs con C#
- **Aplicaciones Móviles**: MAUI para iOS y Android
- **Aplicaciones Empresariales**: WPF/WinForms para desktop tradicional
- **Gaming**: Unity con .NET para scripts
- **IoT**: .NET Nano Framework para dispositivos embebidos
- **Machine Learning**: ML.NET para integrar AI

### Evolución Futura

.NET continúa evolucionando con releases anuales. La hoja de ruta incluye:

- **Mayor rendimiento**: Optimizaciones continuas en JIT, GC y bibliotecas base
- **Native AOT mejorado**: Más escenarios soportados con compilación nativa
- **Cloud-native**: Mejor integración con patrones modernos
- **AI/ML**: Capacidades de inteligencia artificial más profundas
- **Simplificación**: APIs más intuitivas y menos boilerplate

### Adopción Recomendada

Para nuevos proyectos:
- Comenzar con .NET 10 (LTS) para estabilidad
- Usar ASP.NET Core para web
- Considerar Blazor para SPAs
- MAUI para móvil cross-platform
- EF Core para acceso a datos

Para migración:
- .NET Framework → .NET 10 con asistentes de migración
- Xamarin → MAUI progresivamente
- ASP.NET MVC → ASP.NET Core MVC

### Recursos de Aprendizaje

- **Documentación Oficial**: https://docs.microsoft.com/dotnet
- **.NET Blog**: https://devblogs.microsoft.com/dotnet
- **GitHub**: https://github.com/dotnet
- **Microsoft Learn**: Paths de aprendizaje gratuitos
- **Pluralsight / LinkedIn Learning**: Cursos en profundidad
- **Conferencias**: .NET Conf anual

### Comunidad

- **Stack Overflow**: Tag .net y relacionados
- **Reddit**: r/dotnet
- **Discord**: Servidores oficiales y de comunidad
- **Meetups**: Grupos locales de .NET
- **User Groups**: .NET Foundation user groups

### Conclusión Final

.NET 10 consolida a .NET como una plataforma unificada, moderna y de alto rendimiento para construir cualquier tipo de aplicación. Con su modelo open source, comunidad activa, soporte empresarial de Microsoft, y evolución continua, .NET está posicionado como una elección segura y poderosa para el desarrollo de software en la década que viene.

La inversión en aprender .NET 10 es una inversión en una tecnología con futuro garantizado, ampliamente adoptada en la industria, y con demanda sostenida de profesionales capacitados.

---

## Referencias

1. Microsoft .NET Documentation: https://docs.microsoft.com/dotnet
2. .NET Blog: https://devblogs.microsoft.com/dotnet
3. .NET Foundation: https://dotnetfoundation.org
4. GitHub - dotnet: https://github.com/dotnet
5. ASP.NET Core Documentation: https://docs.microsoft.com/aspnet/core
6. Entity Framework Core Documentation: https://docs.microsoft.com/ef/core
7. Azure Documentation: https://docs.microsoft.com/azure
8. C# Language Specification: https://docs.microsoft.com/dotnet/csharp
9. .NET Performance Blog: https://devblogs.microsoft.com/dotnet/category/performance
