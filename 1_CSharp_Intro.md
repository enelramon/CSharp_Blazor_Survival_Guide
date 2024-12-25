# Conceptos Básicos de C#: Variables, Tipos de Datos y Operadores

## Índice
1. [Variables en C#](#variables-en-csharp)
2. [Tipos de Datos en C#](#tipos-de-datos-en-csharp)
3. [Operadores en C#](#operadores-en-csharp)

Estas son las herramientas esenciales que te permiten expresar tu lógica y crear programas dinámicos y receptivos. Así que, vamos a sumergirnos y desentrañar la simplicidad y el poder de los elementos básicos de C#.

## Variables en C#

Las variables son como contenedores que contienen información en tu programa. Dan nombres a los valores, haciendo que tu código sea legible y adaptable.

### Ejemplo 1: Declaración de Variables y Constantes
```csharp
const double pi = 3.14; // constante
int contador = 0; // variable
```
En este ejemplo, `pi` es una constante inicializada con el valor 3.14, mientras que `contador` es una variable mutable que comienza en 0. La palabra clave `const` asegura que el valor de `pi` permanezca constante, mientras que el tipo de datos `int` permite que `contador` cambie durante la ejecución del programa. Las constantes son útiles para valores que no deben cambiar, mientras que las variables son útiles para valores que pueden cambiar.

### Ejemplo 2: Inferencia de Tipos
C# también es inteligente para entender los tipos de variables sin mencionarlos explícitamente usando `var`.
```csharp
var edad = 25;
var nombre = "Alicia";
```
Aquí, C# infiere que `edad` es un entero y `nombre` es una cadena. Esta inferencia de tipos reduce la necesidad de declaraciones de tipos explícitas, haciendo que tu código sea conciso y legible.

## Tipos de Datos en C#

Los tipos de datos definen el tipo de valores que una variable puede contener. C# soporta una gama de tipos de datos, cada uno sirviendo a un propósito específico.

### Ejemplo 3: Explorando Tipos de Datos
```csharp
int edad = 25;
double altura = 175.5;
bool esEstudiante = true;
string nombre = "Alicia";
```
- `edad` es un entero (`int`).
- `altura` es un número de punto flotante de doble precisión (`double`).
- `esEstudiante` es un booleano (`bool`).
- `nombre` es una cadena (`string`).

Entender y elegir el tipo de datos correcto es crucial para un uso eficiente de la memoria y una representación precisa de la lógica de tu programa.

## Operadores en C#

Los operadores son símbolos que realizan operaciones en variables y valores. C# hereda operadores familiares de otros lenguajes pero los mejora para una sintaxis más expresiva y concisa.

### Ejemplo 4: Operadores Matemáticos
```csharp
int x = 10;
int y = 5;
int suma = x + y;
int diferencia = x - y;
int producto = x * y;
int cociente = x / y;
int resto = x % y;
```
En este fragmento, se realizan operaciones aritméticas básicas en las variables `x` y `y`. El resultado de cada operación se almacena en una nueva variable, mostrando la simplicidad y legibilidad de C#.

### Ejemplo 5: Concatenación de Cadenas
C# hace que la manipulación de cadenas sea intuitiva.
```csharp
string primerNombre = "Juan";
string apellido = "Pérez";
string nombreCompleto = primerNombre + " " + apellido;
```
Aquí, el operador `+` concatena el primer nombre, un espacio y el apellido para crear el nombre completo.

### Ejemplo 6: Operadores de Comparación
Comparar valores es una operación común en programación.
```csharp
int a = 10;
int b = 20;
bool esIgual = (a == b);
bool noEsIgual = (a != b);
bool esMayor = (a > b);
bool esMenorOIgual = (a <= b);
```
Estos operadores evalúan condiciones y devuelven un resultado booleano, ayudando en la toma de decisiones dentro de tu código.
