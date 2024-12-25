# Colecciones en C#: Listas, Diccionarios y Conjuntos

## Índice
1. [Listas en C#: Colecciones Ordenadas](#listas-en-c-colecciones-ordenadas)
2. [Diccionarios en C#: Pares Clave-Valor](#diccionarios-en-c-pares-clave-valor)
3. [Conjuntos en C#: Colecciones Únicas](#conjuntos-en-c-colecciones-únicas)
4. [Funciones de Colecciones en C#: Más Allá de lo Básico](#funciones-de-colecciones-en-c-más-allá-de-lo-básico)
5. [Mejores Prácticas para Colecciones en C#](#mejores-prácticas-para-colecciones-en-c)

Las colecciones juegan un papel fundamental en la programación, facilitando el almacenamiento, recuperación y transformación de datos. En este capítulo, profundizaremos en tres tipos fundamentales de colecciones en C#: Listas, Diccionarios y Conjuntos. Estas estructuras ofrecen capacidades únicas para adaptarse a diversos escenarios en tu viaje de codificación.

## Listas en C#: Colecciones Ordenadas

Las listas son uno de los tipos de colección más comunes y versátiles en C#. Una lista es una colección ordenada de elementos, que permite un fácil acceso basado en el índice de cada elemento. Vamos a explorar la creación, manipulación y utilización de listas con ejemplos prácticos.

### Ejemplo 1: Creando una Lista
```csharp
// Creando una lista de enteros
List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };
```
En este ejemplo, se crea una lista llamada `numeros` con elementos enteros.

### Ejemplo 2: Accediendo a Elementos de la Lista
```csharp
// Accediendo a elementos de la lista
int primerElemento = numeros[0]; // 1
int ultimoElemento = numeros[numeros.Count - 1]; // 5
```
Los elementos de la lista se pueden acceder usando su índice. Aquí, `primerElemento` recupera el elemento en el índice 0, y `ultimoElemento` obtiene el último elemento.

### Ejemplo 3: Modificando una Lista
```csharp
// Modificando la lista
numeros.Add(6);
numeros.RemoveAt(1);
```
Para modificar una lista, usa métodos como `Add` y `RemoveAt`. En este caso, se añade un elemento y se elimina otro.

### Ejemplo 4: Iterando a Través de una Lista
```csharp
// Iterando a través de la lista
foreach (int numero in numeros) {
    Console.WriteLine($"Número Actual: {numero}");
}
```
Iterar a través de una lista es simple con un bucle `foreach`. Este ejemplo imprime cada elemento en la lista.

## Diccionarios en C#: Pares Clave-Valor

Los diccionarios, también conocidos como mapas en algunos lenguajes, son colecciones que almacenan pares clave-valor. Cada clave en un diccionario es única y está asociada con un valor específico. Esto hace que los diccionarios sean ideales para escenarios donde los datos necesitan ser organizados y recuperados basados en identificadores distintos.

### Ejemplo 5: Creando un Diccionario
```csharp
// Creando un diccionario de países y sus capitales
Dictionary<string, string> capitales = new Dictionary<string, string> {
    { "EE.UU.", "Washington, D.C." },
    { "Francia", "París" },
    { "Japón", "Tokio" }
};
```
En este ejemplo, se crea un diccionario llamado `capitales`, asociando países con sus respectivas capitales.

### Ejemplo 6: Accediendo a Valores del Diccionario
```csharp
// Accediendo a valores en el diccionario
string capitalEEUU = capitales["EE.UU."]; // Washington, D.C.
capitales.TryGetValue("Italia", out string capitalDesconocida); // null
```
Los valores en un diccionario se acceden usando sus claves correspondientes. `capitalEEUU` recupera la capital de EE.UU., y `capitalDesconocida` obtiene la capital de Italia (que es `null`).

### Ejemplo 7: Modificando un Diccionario
```csharp
// Modificando el diccionario
capitales["Alemania"] = "Berlín";
capitales.Remove("Francia");
```
Para modificar un diccionario, usa métodos como `Add` y `Remove`. Aquí, se añade Alemania y se elimina Francia.

### Ejemplo 8: Iterando a Través de un Diccionario
```csharp
// Iterando a través del diccionario
foreach (var kvp in capitales) {
    Console.WriteLine($"País: {kvp.Key}, Capital: {kvp.Value}");
}
```
Los diccionarios se pueden iterar usando un bucle `foreach`, con desestructuración para acceder tanto a las claves como a los valores. Este ejemplo imprime cada par país-capital.

## Conjuntos en C#: Colecciones Únicas

Los conjuntos son colecciones que almacenan elementos únicos. Aseguran que cada elemento aparezca solo una vez en la colección, haciéndolos adecuados para escenarios donde la unicidad es crucial.

### Ejemplo 9: Creando un Conjunto
```csharp
// Creando un conjunto de colores
HashSet<string> coloresUnicos = new HashSet<string> { "Rojo", "Verde", "Azul", "Rojo" };
```
En este ejemplo, se crea un conjunto llamado `coloresUnicos`. Ten en cuenta que los elementos duplicados (como "Rojo") se eliminan automáticamente.

### Ejemplo 10: Comprobando la Pertenencia al Conjunto
```csharp
// Comprobando la pertenencia al conjunto
bool tieneVerde = coloresUnicos.Contains("Verde"); // true
bool tieneAmarillo = coloresUnicos.Contains("Amarillo"); // false
```
La pertenencia al conjunto se puede comprobar usando el método `Contains`. Aquí, `tieneVerde` comprueba si "Verde" está en el conjunto, y `tieneAmarillo` comprueba si "Amarillo" está en el conjunto.

### Ejemplo 11: Modificando un Conjunto
```csharp
// Modificando el conjunto
coloresUnicos.Add("Amarillo");
coloresUnicos.Remove("Rojo");
```
Para modificar un conjunto, usa métodos como `Add` y `Remove`. En este caso, se añade "Amarillo" y se elimina "Rojo".

### Ejemplo 12: Iterando a Través de un Conjunto
```csharp
// Iterando a través del conjunto
foreach (string color in coloresUnicos) {
    Console.WriteLine($"Color Actual: {color}");
}
```
Los conjuntos se pueden iterar usando un bucle `foreach`. Este ejemplo imprime cada elemento en el conjunto.

## Funciones de Colecciones en C#: Más Allá de lo Básico

C# proporciona un conjunto rico de funciones para trabajar con colecciones, haciendo que operaciones como filtrar, mapear y transformar datos sean convenientes y expresivas.

### Ejemplo 13: Filtrando una Lista
```csharp
// Filtrando elementos en una lista
List<int> numerosPares = numeros.Where(n => n % 2 == 0).ToList();
```
La función `Where` se puede usar para crear una nueva lista que contenga elementos que satisfacen una condición dada. Aquí, `numerosPares` contiene solo los elementos pares de la lista `numeros`.

### Ejemplo 14: Mapeando una Lista
```csharp
// Mapeando elementos en una lista
List<int> numerosCuadrados = numeros.Select(n => n * n).ToList();
```
La función `Select` aplica una transformación a cada elemento en una lista, creando una nueva lista con los valores transformados. En este ejemplo, `numerosCuadrados` contiene los cuadrados de los elementos en la lista `numeros`.

### Ejemplo 15: Combinando Operaciones
```csharp
// Combinando operaciones de filtro y mapa
List<int> filtradosYCuadrados = numeros.Where(n => n % 2 == 0).Select(n => n * n).ToList();
```
Operaciones como `Where` y `Select` se pueden combinar para crear transformaciones más complejas. Aquí, `filtradosYCuadrados` contiene los cuadrados de los números pares de la lista `numeros`.

## Mejores Prácticas para Colecciones en C#

A medida que aprovechas el poder de las colecciones en C#, considera estas mejores prácticas para asegurar un código eficiente, legible y mantenible:
1. **Inmutabilidad por Defecto:** Prefiere usar colecciones inmutables (`ReadOnlyCollection`, `ImmutableList`, etc.) a menos que se requiera explícitamente la mutabilidad. La inmutabilidad simplifica el razonamiento sobre el código y previene modificaciones no deseadas.
2. **Usa Tipos de Colección Específicos:** Elige el tipo de colección apropiado según tus requisitos. Las listas son ideales para colecciones ordenadas, los diccionarios para pares clave-valor y los conjuntos para elementos únicos.
3. **Aprovecha las Funciones de Colección:** Explora y usa el conjunto rico de funciones de colección proporcionadas por LINQ (`Where`, `Select`, `Aggregate`, etc.) para realizar operaciones complejas de manera concisa y expresiva.
4. **Considera las Implicaciones de Rendimiento:** Ten en cuenta las implicaciones de rendimiento de las operaciones de colección, especialmente en escenarios que involucran grandes conjuntos de datos. Evalúa la complejidad temporal y espacial de tu código.
5. **Seguridad Nula en Diccionarios:** Al tratar con valores nulos en diccionarios, considera usar el método `TryGetValue` para manejar escenarios donde una clave podría estar ausente.
6. **Paradigma de Programación Funcional:** Adopta el paradigma de programación funcional ofrecido por LINQ. Funciones como `Where` y `Select` se alinean con los principios de programación funcional, permitiendo un estilo de codificación más declarativo y expresivo.
7. **Encapsula Operaciones Complejas:** Para transformaciones u operaciones complejas que involucren colecciones, encapsúlalas en funciones bien nombradas. Esto promueve la legibilidad y reutilización del código.
8. **Colecciones Inmutables en Firmas de Función:** Al diseñar funciones que aceptan colecciones como parámetros, considera usar tipos de colección inmutables en la firma de la función. Esto asegura que la función no pueda modificar la colección original.
