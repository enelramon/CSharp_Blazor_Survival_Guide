# **GUÍA DE ARQUITECTURA DE SOFTWARE**

para Proyectos Profesionales con C\# y .NET

*Windows Forms \+ Entity Framework Core \+ Inyección de Dependencias*

Versión 1.0  •  2025

## **1\. ¿Por qué importa la arquitectura?**

Un proyecto sin arquitectura definida crece de forma caótica: los formularios tienen lógica de negocio, las consultas a base de datos están mezcladas con la interfaz, y cualquier cambio pequeño rompe funcionalidades en lugares inesperados.

Una buena arquitectura te da:

* Código mantenible: cualquier desarrollador puede entender el proyecto rápidamente.

* Testeable: puedes probar la lógica sin necesidad de abrir formularios.

* Escalable: agregar nuevas funcionalidades no requiere reescribir lo existente.

* Profesional: es lo que se espera en el mundo laboral real.

# **2\. Arquitectura en Capas (N-Layer)**

La arquitectura recomendada para proyectos de escritorio con Windows Forms y EF Core es la arquitectura en 3 capas lógicas distribuidas en proyectos separados dentro de la misma solución:

| Capa | Proyecto (.csproj) | Responsabilidad |
| :---- | :---- | :---- |
| Presentación | MiApp.Ui | Formularios Windows Forms, validación visual, navegación entre pantallas |
| Negocio | MiApp.Business | Reglas de negocio, validaciones complejas, coordinación de operaciones |
| Datos | MiApp.Data | DbContext de EF Core, modelos, repositorios, acceso a base de datos |

**Regla de oro:** Las capas superiores solo conocen a la capa inmediatamente inferior. La capa de Presentación NUNCA accede directamente al DbContext.

## **2.1 Estructura de carpetas recomendada**

Solution 'MiApp'

├── MiApp.Data

│   ├── Context/

│   │   └── MiAppContext.cs

│   ├── Models/          ← Generados por Scaffold

│   └── Repositories/

│       ├── IProductRepository.cs

│       └── ProductRepository.cs

├── MiApp.Business

│   ├── DTOs/

│   │   └── ProductDto.cs

│   ├── Interfaces/

│   │   └── IProductService.cs

│   └── Services/

│       └── ProductService.cs

└── MiApp.Ui

    ├── Forms/

    │   └── Products/

    │       ├── ProductForm.cs

    │       └── ProductForm.Designer.cs

    ├── App.config

    └── Program.cs

# **3\. Capa de Datos (MiApp.Data)**

## **3.1 Paquetes NuGet necesarios**

* Microsoft.EntityFrameworkCore

* Microsoft.EntityFrameworkCore.SqlServer

* Microsoft.EntityFrameworkCore.Tools

## **3.2 Patrón Repositorio**

El patrón Repositorio abstrae el acceso a datos detrás de una interfaz. Esto tiene dos beneficios clave: la capa de negocio no sabe si los datos vienen de SQL Server, SQLite, o un mock para pruebas; y puedes cambiar la tecnología de acceso a datos sin tocar la lógica de negocio.

**Interfaz (IProductRepository.cs):**

public interface IProductRepository

{

    Task\<IEnumerable\<Product\>\> GetAllAsync();

    Task\<Product?\> GetByIdAsync(int id);

    Task AddAsync(Product product);

    Task UpdateAsync(Product product);

    Task DeleteAsync(int id);

}

**Implementación (ProductRepository.cs):**

public class ProductRepository : IProductRepository

{

    private readonly MiAppContext \_context;

    public ProductRepository(MiAppContext context)

        \=\> \_context \= context;

    public async Task\<IEnumerable\<Product\>\> GetAllAsync()

        \=\> await \_context.Products.ToListAsync();

    public async Task AddAsync(Product product)

    {

        \_context.Products.Add(product);

        await \_context.SaveChangesAsync();

    }

}

# **4\. Capa de Negocio (MiApp.Business)**

## **4.1 ¿Para qué sirve?**

La capa de negocio es el corazón de la aplicación. Aquí van las reglas que definen cómo funciona el sistema, no cómo se ve ni cómo se almacena.

| ✅ Va en Business | ❌ NO va en Business |
| :---- | :---- |
| Validar que el precio de lista sea mayor al costo | Mostrar un MessageBox de error |
| Calcular descuentos o impuestos | Consultas directas al DbContext |
| Verificar que un producto no esté duplicado | Lógica de navegación entre formularios |
| Orquestar múltiples operaciones en secuencia | Manipulación de controles visuales |

## **4.2 DTOs (Data Transfer Objects)**

Los DTOs son clases simples que transportan solo los datos necesarios entre capas. Nunca expongas los modelos de EF Core directamente a la capa de presentación.

public class ProductDto

{

    public int ProductId { get; set; }

    public string Name { get; set; } \= string.Empty;

    public decimal ListPrice { get; set; }

    public string? CategoryName { get; set; }

}

## **4.3 Servicio de ejemplo**

public class ProductService : IProductService

{

    private readonly IProductRepository \_repo;

    public ProductService(IProductRepository repo)

        \=\> \_repo \= repo;

    public async Task\<IEnumerable\<ProductDto\>\> GetAllAsync()

    {

        var products \= await \_repo.GetAllAsync();

        return products.Select(p \=\> new ProductDto {

            ProductId \= p.ProductId,

            Name \= p.Name,

            ListPrice \= p.ListPrice

        });

    }

    public async Task CreateAsync(ProductDto dto)

    {

        // Regla de negocio

        if (dto.ListPrice \<= 0\)

            throw new BusinessException("El precio debe ser mayor a 0.");

        var product \= new Product {

            Name \= dto.Name,

            ListPrice \= dto.ListPrice,

            ModifiedDate \= DateTime.Now

        };

        await \_repo.AddAsync(product);

    }

}

# **5\. Inyección de Dependencias**

## **5.1 ¿Qué es y por qué usarla?**

La Inyección de Dependencias (DI) es un patrón donde las clases reciben sus dependencias desde afuera en lugar de crearlas internamente. Esto hace el código más flexible, testeable y desacoplado.

| Sin DI ❌ | Con DI ✅ |
| :---- | :---- |
| var svc \= new ProductService(new ProductRepository(new MiAppContext())); | ProductService se recibe en el constructor automáticamente |
| Imposible hacer pruebas unitarias | Puedes inyectar mocks para pruebas |
| Dependencias hardcodeadas en toda la app | Un solo lugar de configuración: Program.cs |

## **5.2 Configuración en Program.cs**

internal static class Program

{

    public static ServiceProvider ServiceProvider { get; private set; }

    \[STAThread\]

    static void Main()

    {

        ApplicationConfiguration.Initialize();

        var services \= new ServiceCollection();

        ConfigureServices(services);

        ServiceProvider \= services.BuildServiceProvider();

        Application.Run(ServiceProvider.GetRequiredService\<MainForm\>());

    }

    private static void ConfigureServices(ServiceCollection services)

    {

        var connStr \= ConfigurationManager

            .ConnectionStrings\["MiApp"\].ConnectionString;

        // Datos

        services.AddDbContext\<MiAppContext\>(o \=\> o.UseSqlServer(connStr));

        services.AddScoped\<IProductRepository, ProductRepository\>();

        // Negocio

        services.AddScoped\<IProductService, ProductService\>();

        // Formularios

        services.AddTransient\<MainForm\>();

        services.AddTransient\<ProductForm\>();

    }

}

## **5.3 Ciclos de vida: cuándo usar cada uno**

| Ciclo de vida | Cuándo usarlo |
| :---- | :---- |
| AddSingleton | Una sola instancia en toda la app. Para configuración, logging, caché. |
| AddScoped | Una instancia por operación/alcance. Ideal para DbContext, Repositorios y Servicios. |
| AddTransient | Nueva instancia cada vez que se solicita. Ideal para Formularios Windows Forms. |

# **6\. Capa de Presentación (MiApp.Ui)**

## **6.1 Responsabilidades del formulario**

Un formulario bien diseñado solo debe:

* Mostrar datos al usuario (llenar controles con información).

* Capturar la entrada del usuario (leer controles).

* Validar el formato de entrada (campos obligatorios, formatos).

* Delegar toda la lógica al servicio correspondiente.

* Mostrar resultados o errores al usuario.

**Principio:** Si ves lógica de negocio en un formulario, es una señal de que debe moverse a la capa de Business.

## **6.2 Formulario correcto vs incorrecto**

| ❌ Formulario con lógica de negocio | ✅ Formulario delegando al servicio |
| :---- | :---- |
| if (listPrice \<= standardCost) MessageBox.Show("Error"); | try { await \_service.CreateAsync(dto); } |
| \_context.Products.Add(new Product { ... }); | catch (BusinessException ex) { MessageBox.Show(ex.Message); } |
| await \_context.SaveChangesAsync(); | MessageBox.Show("Guardado correctamente."); |

## **6.3 Patrón de carga asíncrona**

private void Form\_Load(object sender, EventArgs e)

    \=\> \_ \= LoadDataAsync();

private async Task LoadDataAsync()

{

    try

    {

        var products \= await \_service.GetAllAsync();

        dgvProducts.DataSource \= products.ToList();

    }

    catch (Exception ex)

    {

        MessageBox.Show($"Error: {ex.Message}", "Error",

            MessageBoxButtons.OK, MessageBoxIcon.Error);

    }

}

# **7\. Manejo de Errores**

## **7.1 Excepción personalizada de negocio**

Crea una excepción personalizada en la capa de negocio para distinguir errores de validación de errores técnicos inesperados:

public class BusinessException : Exception

{

    public BusinessException(string message) : base(message) { }

}

## **7.2 Estrategia de manejo por capa**

| Capa | Proyecto (.csproj) | Responsabilidad |
| :---- | :---- | :---- |
| Business | MiApp.Business | Lanza BusinessException para errores de validación esperados. |
| Data | MiApp.Data | Deja que las excepciones de EF Core suban sin atraparlas. |
| Presentación | MiApp.Ui | Captura BusinessException para mensajes amigables, Exception para errores inesperados. |

private async void btnSave\_Click(object sender, EventArgs e)

{

    try

    {

        await \_service.CreateAsync(BuildDto());

        MessageBox.Show("Guardado correctamente.");

        this.Close();

    }

    catch (BusinessException ex)

    {

        // Error esperado: mostrar mensaje amigable

        MessageBox.Show(ex.Message, "Validación",

            MessageBoxButtons.OK, MessageBoxIcon.Warning);

    }

    catch (Exception ex)

    {

        // Error inesperado: loggear y mostrar mensaje genérico

        MessageBox.Show("Ocurrió un error inesperado.", "Error",

            MessageBoxButtons.OK, MessageBoxIcon.Error);

    }

}

# **8\. Checklist de Proyecto Profesional**

Antes de entregar tu proyecto, verifica que cumple con todos estos puntos:

## **Estructura**

* La solución tiene al menos 2 proyectos: Data y Ui (idealmente 3 con Business).

* Cada proyecto referencia solo al proyecto de la capa inferior.

* Hay una carpeta por entidad en cada capa (Products/, Customers/, etc.).

## **Datos**

* El DbContext vive en MiApp.Data, nunca en Ui.

* Existe al menos una interfaz de repositorio con su implementación.

* La cadena de conexión está en App.config, no hardcodeada en el código.

## **Negocio**

* Las reglas de negocio están en servicios, no en formularios.

* Los formularios reciben DTOs, no modelos de EF Core.

* Existe una BusinessException para errores esperados.

## **Presentación**

* Los formularios se registran con AddTransient en Program.cs.

* Los formularios nuevos se abren con ServiceProvider.GetRequiredService\<T\>().

* Toda carga de datos usa async/await correctamente.

* Hay validación visual con ErrorProvider antes de llamar al servicio.

* Los errores se muestran con MessageBox diferenciando tipo de error.

## **Calidad general**

* No hay código comentado ni métodos vacíos sin uso.

* Los nombres de variables, métodos y clases son descriptivos en español o inglés (consistente).

* No hay números mágicos: se usan constantes o configuración.

* El proyecto compila sin advertencias (warnings).

# **9\. Resumen Visual**

| Flujo | Presentación (Ui) | Negocio (Business) | Datos (Data) |
| ----- | ----- | ----- | ----- |
| Leer datos | Llama a IService.GetAllAsync() | Llama a IRepository.GetAllAsync() | Consulta EF Core → SQL Server |
| Guardar | Llama a IService.CreateAsync(dto) | Valida reglas, llama a IRepository.AddAsync() | Add \+ SaveChangesAsync() |
| Error negocio | Muestra MessageBox warning | Lanza BusinessException | — |
| Error técnico | Muestra MessageBox error | No captura, deja subir | Excepción de EF Core sube |

# **10\. Estilo Funcional: Patron Result**

El patron Result es una alternativa al uso de excepciones para el control de flujo. En lugar de lanzar un throw, los metodos devuelven un objeto que representa exito o fallo. Esto hace que el codigo sea mas predecible, mas facil de leer y honesto en su firma.

| Antes (excepciones) | Ahora (Result) |
| :---- | :---- |
| throw new BusinessException(...) | return Result.Failure(...) |
| try/catch en el formulario | .OnSuccess() / .OnFailure() |
| La firma no dice si puede fallar | Task\<Result\> es explicito |
| Control de flujo con excepciones | Control de flujo con valores |

## **10.1 Clase Result**

public class Result

{

    public bool IsSuccess { get; }

    public bool IsFailure \=\> \!IsSuccess;

    public string Error { get; }

    protected Result(bool isSuccess, string error)

    {

        IsSuccess \= isSuccess;

        Error \= error;

    }

    public static Result Success() \=\> new(true, string.Empty);

    public static Result Failure(string error) \=\> new(false, error);

    public static Result\<T\> Success\<T\>(T value) \=\> new(value, true, string.Empty);

    public static Result\<T\> Failure\<T\>(string error) \=\> new(default\!, false, error);

}

public class Result\<T\> : Result

{

    public T Value { get; }

    protected internal Result(T value, bool isSuccess, string error)

        : base(isSuccess, error) \=\> Value \= value;

}

## **10.2 Extensiones funcionales**

Estas extensiones permiten encadenar operaciones de forma fluida sin anidar if/else ni try/catch:

public static class ResultExtensions

{

    public static Result\<TOut\> Map\<TIn, TOut\>(

        this Result\<TIn\> result, Func\<TIn, TOut\> map)

        \=\> result.IsSuccess

            ? Result.Success(map(result.Value))

            : Result.Failure\<TOut\>(result.Error);

    public static async Task\<Result\<TOut\>\> BindAsync\<TIn, TOut\>(

        this Result\<TIn\> result,

        Func\<TIn, Task\<Result\<TOut\>\>\> bind)

        \=\> result.IsSuccess

            ? await bind(result.Value)

            : Result.Failure\<TOut\>(result.Error);

    public static Result\<T\> OnSuccess\<T\>(

        this Result\<T\> result, Action\<T\> action)

    {

        if (result.IsSuccess) action(result.Value);

        return result;

    }

    public static Result\<T\> OnFailure\<T\>(

        this Result\<T\> result, Action\<string\> action)

    {

        if (result.IsFailure) action(result.Error);

        return result;

    }

}

## **10.3 Servicio con Result**

Las validaciones ya no lanzan excepciones, devuelven Result.Failure con el mensaje de error:

public async Task\<Result\<IEnumerable\<ProductDto\>\>\> GetAllAsync()

{

    try

    {

        var products \= await \_repo.GetAllAsync();

        var dtos \= products.Select(p \=\> new ProductDto {

            ProductId \= p.ProductId,

            Name      \= p.Name,

            ListPrice \= p.ListPrice

        });

        return Result.Success(dtos);

    }

    catch (Exception ex)

        \=\> Result.Failure\<IEnumerable\<ProductDto\>\>(ex.Message);

}

public async Task\<Result\> CreateAsync(ProductDto dto)

{

    var validation \= Validate(dto);

    if (validation.IsFailure) return validation;

    try

    {

        await \_repo.AddAsync(new Product {

            Name          \= dto.Name,

            ListPrice     \= dto.ListPrice,

            StandardCost  \= dto.StandardCost,

            ModifiedDate  \= DateTime.Now,

            Rowguid       \= Guid.NewGuid(),

            SellStartDate \= DateTime.Now

        });

        return Result.Success();

    }

    catch (Exception ex) { return Result.Failure(ex.Message); }

}

private static Result Validate(ProductDto dto)

{

    if (string.IsNullOrWhiteSpace(dto.Name))

        return Result.Failure("El nombre es obligatorio.");

    if (dto.ListPrice \<= 0\)

        return Result.Failure("El precio debe ser mayor a 0.");

    if (dto.ListPrice \< dto.StandardCost)

        return Result.Failure("El precio no puede ser menor al costo.");

    return Result.Success();

}

## **10.4 Formulario consumiendo Result**

El formulario ya no necesita try/catch. El manejo de exito y error queda separado y legible:

private async Task LoadDataAsync()

{

    var result \= await \_service.GetAllAsync();

    result

        .OnSuccess(p \=\> dgvProducts.DataSource \= p.ToList())

        .OnFailure(e \=\> MessageBox.Show(e, "Error",

            MessageBoxButtons.OK, MessageBoxIcon.Error));

}

private async void btnSave\_Click(object sender, EventArgs e)

{

    if (\!ValidateForm()) return;

    btnSave.Enabled \= false;

    var result \= await \_service.CreateAsync(BuildDto());

    result

        .OnSuccess(\_ \=\> { MessageBox.Show("Guardado."); this.Close(); })

        .OnFailure(e \=\> MessageBox.Show(e, "Validacion",

            MessageBoxButtons.OK, MessageBoxIcon.Warning));

    btnSave.Enabled \= true;

}

## **10.5 Encadenamiento con Bind (nivel avanzado)**

Para operaciones que dependen unas de otras se pueden encadenar con BindAsync evitando if anidados:

public async Task\<Result\<ProductDto\>\> GetAndValidateAsync(int id)

{

    var result \= await \_repo.GetByIdAsync(id);

    return await result

        .BindAsync(ValidateActive)

        .Map(p \=\> new ProductDto {

            ProductId \= p.ProductId,

            Name      \= p.Name

        });

}

private Result\<Product\> ValidateActive(Product p)

    \=\> p.SellEndDate is null || p.SellEndDate \> DateTime.Now

        ? Result.Success(p)

        : Result.Failure\<Product\>("El producto ya no esta activo.");

**Consejo:** Coloca Result.cs y ResultExtensions.cs en una carpeta Common dentro de MiApp.Business. Al ser clases genericas y reutilizables no pertenecen a ninguna entidad especifica.

*"El codigo limpio no es el codigo que funciona. Es el codigo que cualquier desarrollador puede entender."*