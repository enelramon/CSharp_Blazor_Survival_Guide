# Funciones en C#

## Índice
1. [Definiendo y Llamando](#definiendo-y-llamando)
2. [Argumentos Predeterminados y Nombrados](#argumentos-predeterminados-y-nombrados)
3. [Sobrecarga de Funciones](#sobrecarga-de-funciones)
4. [Métodos de Extensión](#métodos-de-extensión)
5. [Funciones de Orden Superior](#funciones-de-orden-superior)
6. [Expresiones Lambda](#expresiones-lambda)
7. [Métodos Inline](#métodos-inline)
8. [Funciones Recursivas](#funciones-recursivas)
9. [Funciones Recursivas de Cola](#funciones-recursivas-de-cola)
10. [Tareas Asíncronas](#tareas-asíncronas)

## Definiendo y Llamando

Las funciones sirven como bloques de construcción, permitiéndote descomponer tu código en componentes manejables y reutilizables. Exploraremos cómo definir funciones, pasar parámetros, devolver valores y llamar funciones con diferentes enfoques. Vamos a sumergirnos en el corazón de la programación modular y eficiente en C#.

## Definiendo Funciones en C#

En su núcleo, una función es un bloque de código que realiza una tarea específica. En C#, definir una función implica especificar su nombre, parámetros, tipo de retorno y el código que ejecuta.

### Ejemplo 1: Función Simple
```csharp
void Saludar() {
    Console.WriteLine("¡Hola, Desarrollador de C#!");
}
```
En este ejemplo, definimos una función simple llamada `Saludar`. El cuerpo de la función, encerrado en llaves, contiene el código para imprimir un mensaje de saludo.

### Ejemplo 2: Función con Parámetros
```csharp
void SaludarPorNombre(string nombre) {
    Console.WriteLine($"¡Hola, {nombre}!");
}
```

Aquí, la función `SaludarPorNombre` toma un parámetro `nombre` de tipo `string`. Esto permite que la función personalice el saludo según el nombre proporcionado.

### Ejemplo 3: Función con Tipo de Retorno
```csharp
int Cuadrado(int numero) {
    return numero * numero;
}
```

La función `Cuadrado` calcula el cuadrado de un número dado y devuelve el resultado. El tipo de retorno `int` especifica el tipo de valor que la función devuelve.

## Llamando Funciones en C#

Una vez que has definido una función, llamarla o invocarla es un proceso sencillo. Proporcionas los argumentos requeridos y la función ejecuta su lógica definida.

### Ejemplo 4: Llamando Función Simple
```csharp
// Llamando la función simple Saludar
Saludar();
```

Aquí, llamamos a la función `Saludar`, y esta imprime el mensaje de saludo predefinido.

### Ejemplo 5: Llamando Función con Parámetros
```csharp
// Llamando la función SaludarPorNombre con un argumento
SaludarPorNombre("Enel Almonte");
```

En este caso, llamamos a la función `SaludarPorNombre`, pasando el argumento "Enel Almonte". La función luego imprime un saludo personalizado para Enel Almonte.

### Ejemplo 6: Llamando Función con Tipo de Retorno
```csharp
// Llamando la función Cuadrado y imprimiendo el resultado
int resultado = Cuadrado(5);
Console.WriteLine($"El cuadrado de 5 es: {resultado}");
```

La función `Cuadrado` se llama con el argumento 5, y el resultado se almacena en la variable `resultado`. Luego imprimimos el cuadrado calculado.

## Argumentos Predeterminados y Nombrados

C# te permite definir valores predeterminados para los parámetros de las funciones, haciéndolas más flexibles al llamarlas. Además, puedes usar argumentos nombrados para especificar valores para parámetros específicos.

### Ejemplo 7: Función con Argumento Predeterminado
```csharp
void SaludarConPredeterminado(string nombre = "Desarrollador") {
    Console.WriteLine($"¡Hola, {nombre}!");
}
```
Aquí, la función `SaludarConPredeterminado` tiene un valor predeterminado para el parámetro `nombre`. Si no se proporciona ningún argumento, se usa el valor predeterminado "Desarrollador".

### Ejemplo 8: Llamando Función con Argumento Predeterminado
```csharp
// Llamando la función SaludarConPredeterminado sin un argumento
SaludarConPredeterminado();
```

En este ejemplo, llamar a `SaludarConPredeterminado` sin proporcionar un argumento usa el valor predeterminado, resultando en el saludo "¡Hola, Desarrollador!"

### Ejemplo 9: Función con Argumentos Nombrados
```csharp
void MostrarOrden(string articulo, int cantidad, string prioridad = "Normal") {
    Console.WriteLine($"Artículo: {articulo}, Cantidad: {cantidad}, Prioridad: {prioridad}");
}
```

Aquí, la función `MostrarOrden` tiene parámetros `articulo`, `cantidad` y un valor predeterminado para `prioridad`. Los argumentos nombrados nos permiten proporcionar valores en cualquier orden.

### Ejemplo 10: Llamando Función con Argumentos Nombrados
```csharp
// Llamando la función MostrarOrden con argumentos nombrados
MostrarOrden(cantidad: 3, prioridad: "Alta", articulo: "Portátil");
```

Usando argumentos nombrados, podemos proporcionar valores para los parámetros en cualquier orden. En este ejemplo, la llamada a la función es clara y legible a pesar del orden diferente.

## Sobrecarga de Funciones

La sobrecarga de funciones en C# te permite definir múltiples funciones con el mismo nombre pero diferentes listas de parámetros. El compilador determina qué función llamar en función de los argumentos proporcionados.

### Ejemplo 11: Sobrecarga de Funciones
```csharp
void Saludar(string persona) {
    Console.WriteLine($"¡Hola, {persona}!");
}
void Saludar(string persona, int edad) {
    Console.WriteLine($"¡Hola, {persona}! Tienes {edad} años.");
}
```

En este ejemplo, tenemos dos funciones `Saludar`: una con un solo parámetro y otra con dos parámetros. La función con la lista de parámetros adecuada se llama según el contexto.

### Ejemplo 12: Llamando Funciones Sobrecargadas
```csharp
// Llamando las funciones sobrecargadas Saludar
Saludar("Enel Almonte");
Saludar("Bob", 30);
```

Ambas funciones `Saludar` se llaman con diferentes argumentos. El compilador determina qué versión de la función invocar en función del número y tipo de argumentos.

## Métodos de Extensión

Los métodos de extensión en C# te permiten agregar nuevas funciones a clases existentes sin modificar su código fuente. Esto proporciona un mecanismo poderoso para mejorar la funcionalidad de las clases.

### Ejemplo 13: Método de Extensión
```csharp
// Extendiendo la clase string con un nuevo método
public static class StringExtensions {
    public static string AgregarExclamacion(this string str) {
        return $"{str}!";
    }
}
```

Aquí, definimos un método de extensión llamado `AgregarExclamacion` para la clase `string`. Agrega un signo de exclamación a la cadena dada.

### Ejemplo 14: Usando Método de Extensión
```csharp
// Usando el método de extensión
string saludo = "Bienvenido";
string saludoEmocionado = saludo.AgregarExclamacion();
Console.WriteLine(saludoEmocionado);
```

El método de extensión `AgregarExclamacion` se usa para modificar la cadena "Bienvenido", resultando en la salida "¡Bienvenido!"

## Funciones de Orden Superior

C# admite funciones de orden superior, lo que te permite pasar funciones como parámetros o devolverlas desde otras funciones. Esta característica de programación funcional mejora la legibilidad y reutilización del código.

### Ejemplo 15: Función de Orden Superior
```csharp
// Función de orden superior que toma una función como parámetro
int OperarEnNumeros(int a, int b, Func<int, int, int> operacion) {
    return operacion(a, b);
}

// Ejemplo de función de operación para ser pasada
int Sumar(int x, int y) {
    return x + y;
}
```
En este ejemplo, `OperarEnNumeros` es una función de orden superior que toma dos números y una función como parámetros. La función proporcionada realiza la operación deseada.

### Ejemplo 16: Usando Función de Orden Superior
```csharp
// Usando la función de orden superior con la función Sumar
int resultado = OperarEnNumeros(5, 3, Sumar);
Console.WriteLine($"Resultado de la suma: {resultado}");
```

Aquí, llamamos a `OperarEnNumeros` con la función `Sumar` como parámetro. El resultado es la suma de 5 y 3.

## Expresiones Lambda

Las expresiones lambda en C# son formas concisas de expresar funciones anónimas. Son especialmente útiles cuando se trabaja con funciones de orden superior.

### Ejemplo 17: Expresión Lambda
```csharp
// Usando una expresión lambda en una función de orden superior
Func<int, int, int> multiplicar = (x, y) => x * y;

// Usando la función de orden superior con la expresión lambda
int producto = OperarEnNumeros(4, 6, multiplicar);
Console.WriteLine($"Resultado de la multiplicación: {producto}");
```
En este ejemplo, `multiplicar` es una expresión lambda que representa una función que multiplica dos números. Luego usamos esta expresión lambda en la función de orden superior `OperarEnNumeros`.

