# Testing con xUnit en C#

## Índice
1. [Introducción a xUnit](#introducción-a-xunit)
2. [Configuración del Proyecto](#configuración-del-proyecto)
3. [Escribiendo Pruebas Unitarias](#escribiendo-pruebas-unitarias)
4. [Ejecutando Pruebas](#ejecutando-pruebas)
5. [Mejores Prácticas](#mejores-prácticas)

## Introducción a xUnit

xUnit es un framework de pruebas unitarias para .NET que permite escribir y ejecutar pruebas de manera sencilla y eficiente. Es una de las herramientas más populares para realizar pruebas en aplicaciones .NET.

## Configuración del Proyecto

Para comenzar a usar xUnit, primero necesitas agregar el paquete xUnit a tu proyecto. Puedes hacerlo utilizando NuGet Package Manager o el siguiente comando en la consola del administrador de paquetes:

```bash
dotnet add package xunit
dotnet add package xunit.runner.visualstudio
```

## Escribiendo Pruebas Unitarias

Las pruebas unitarias en xUnit se escriben en clases de prueba que contienen métodos de prueba. Cada método de prueba debe estar decorado con el atributo `[Fact]`.

### Ejemplo 1: Prueba Unitaria Simple
```csharp
using Xunit;

public class CalculadoraTests
{
    [Fact]
    public void Sumar_DosNumeros_RetornaResultadoCorrecto()
    {
        // Arrange
        var calculadora = new Calculadora();
        int a = 5;
        int b = 3;

        // Act
        int resultado = calculadora.Sumar(a, b);

        // Assert
        Assert.Equal(8, resultado);
    }
}
```
En este ejemplo, se prueba el método `Sumar` de la clase `Calculadora` para verificar que retorna el resultado correcto.

## Ejecutando Pruebas

Para ejecutar las pruebas, puedes usar Visual Studio o la línea de comandos. En Visual Studio, simplemente abre el Explorador de Pruebas y ejecuta las pruebas desde allí. En la línea de comandos, usa el siguiente comando:

```bash
dotnet test
```

## Mejores Prácticas

Al escribir pruebas unitarias con xUnit, considera las siguientes mejores prácticas para asegurar un código de prueba eficiente y legible:
1. **Nombrado Claro:** Usa nombres descriptivos para las clases y métodos de prueba.
2. **AAA Pattern:** Sigue el patrón Arrange-Act-Assert para estructurar tus pruebas.
3. **Pruebas Aisladas:** Asegúrate de que cada prueba sea independiente y no dependa de otras pruebas.
4. **Cobertura de Código:** Escribe pruebas que cubran tanto casos positivos como negativos.
5. **Mantenibilidad:** Mantén el código de prueba limpio y fácil de mantener.

xUnit es una herramienta poderosa para realizar pruebas unitarias en aplicaciones .NET. Al seguir estas mejores prácticas, puedes escribir pruebas más efectivas y mantener un alto nivel de calidad en tu código.
