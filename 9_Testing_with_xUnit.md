# Guía Avanzada de Testing con xUnit en .NET
Esta guía combina los fundamentos de xUnit con la configuración práctica necesaria para probar capas de negocio (BLL) y persistencia de datos.
## Índice
 1. Introducción a xUnit
 2. Configuración del Proyecto
 3. Creación de un Proyecto de Pruebas en Visual Studio
 4. Configuración de Entity Framework para Tests
 5. Escribiendo Pruebas para BLL
 6. El uso de la clase Assert
 7. Ejecución y Resultados
 8. Mejores Prácticas
## 1. Introducción a xUnit
xUnit es un framework moderno de pruebas unitarias para .NET. A diferencia de otros frameworks, utiliza atributos más simples como [Fact] para pruebas fijas y [Theory] para pruebas con datos variables.
## 2. Configuración del Proyecto
Para proyectos manuales o vía CLI, instala los paquetes esenciales:
```bash
dotnet add package xunit
dotnet add package xunit.runner.visualstudio

```
## 3. Creación de un Proyecto de Pruebas en Visual Studio
Según el flujo de trabajo estándar en Visual Studio:
 1. **Ubicación**: En el *Solution Explorer*, identifica la clase que deseas probar (por ejemplo, en la carpeta BLL).
 2. **Generación**: Puedes hacer clic derecho sobre el nombre de la clase y seleccionar **"Create Unit Tests"**.
   * *Nota*: Asegúrate de seleccionar **xUnit** como el Test Framework en la ventana emergente.
 3. **Estructura**: Visual Studio creará un nuevo proyecto (ej. Login.BLL.Tests) con una clase de prueba vinculada.
## 4. Configuración de Entity Framework para Tests
Si tu lógica de negocio utiliza base de datos (Entity Framework), el proyecto de pruebas **también** debe estar configurado para conectarse.
### Paso A: Agregar Configuración
 1. Haz clic derecho en el proyecto de Test -> **Add** -> **New Item**.
 2. Selecciona **Application Configuration File** y asegúrate de que se llame App.config.
 3. Abre el App.config del proyecto principal, copia el <connectionStrings> y pégalo en el App.config del proyecto de Test.
### Paso B: Instalar Entity Framework
Para que el Test reconozca el contexto de datos, abre la **Package Manager Console** y ejecuta:
```powershell
Install-Package EntityFramework -ProjectName TuProyectoDeTests

```
## 5. Escribiendo Pruebas para BLL
A continuación, un ejemplo de cómo probar un método Guardar en la capa UsuariosBLL.
### Clase BLL (Código a probar)
```csharp
public class UsuariosBLL {
    public static bool Guardar(Usuarios user) {
        bool paso = false;
        try {
            Contexto db = new Contexto();
            db.Usuario.Add(user);
            paso = db.SaveChanges() > 0;
        } catch (Exception) { throw; }
        return paso;
    }
}

```
### Clase de Prueba (xUnit)
```csharp
public class UsuariosBLLTests {
    [Fact]
    public void GuardarTest() {
        // Arrange (Preparar)
        bool paso;
        Usuarios usuario = new Usuarios() {
            UsuarioId = 0,
            NombreUsuario = "Prueba",
            Clave = "1234"
        };

        // Act (Actuar)
        paso = UsuariosBLL.Guardar(usuario);

        // Assert (Afirmar)
        Assert.True(paso); // Verificamos que el resultado sea true
    }
}

```
## 6. El uso de la clase Assert
La clase Assert es fundamental para verificar resultados. Aquí las equivalencias entre frameworks:
| Propósito | MSTest (PDF) | xUnit (Recomendado) |
|---|---|---|
| Comprobar igualdad | Assert.AreEqual(a, b) | Assert.Equal(expected, actual) |
| Verificar que es falso | Assert.IsFalse(val) | Assert.False(val) |
| Verificar que es verdadero | Assert.IsTrue(val) | Assert.True(val) |
| Verificar no nulo | Assert.IsNotNull(obj) | Assert.NotNull(obj) |
## 7. Ejecución y Resultados
Para ver si tus pruebas pasan:
 1. **Ejecutar**: Clic derecho sobre el método de prueba o la clase y selecciona **Run Tests**.
 2. **Test Explorer**:
   * **Círculo Verde ✅**: La prueba pasó exitosamente.
   * **Círculo Rojo ❌**: La prueba falló (el código no se comporta como esperabas).
   * **Círculo Azul 🔵**: La prueba no se ha ejecutado.
## 8. Mejores Prácticas
 1. **Patrón AAA**: Mantén siempre el orden *Arrange* (preparación), *Act* (ejecución) y *Assert* (verificación).
 2. **Nombres Descriptivos**: El nombre del test debe decir qué hace, ej: Guardar_UsuarioNuevo_RetornaTrue.
 3. **Limpieza**: Si haces pruebas contra una base de datos real, asegúrate de limpiar los datos de prueba después de cada ejecución.
 4. **Independencia**: Un test no debe depender de que otro test haya corrido antes.
 5. 
