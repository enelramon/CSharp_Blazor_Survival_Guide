# Programación Orientada a Objetos en C# y .NET 9

## Índice
1. [Clases y Objetos: Los Bloques de Construcción de la POO](#clases-y-objetos-los-bloques-de-construcción-de-la-poo)
2. [Constructores: Inicializando Objetos con Facilidad](#constructores-inicializando-objetos-con-facilidad)
3. [Herencia: Construyendo Jerarquías de Clases](#herencia-construyendo-jerarquías-de-clases)
4. [Polimorfismo: Abrazando la Diversidad en Tipos](#polimorfismo-abrazando-la-diversidad-en-tipos)
5. [Encapsulamiento: Protegiendo el Mundo Interior](#encapsulamiento-protegiendo-el-mundo-interior)
6. [Clases Abstractas e Interfaces: Plano para Tipos](#clases-abstractas-e-interfaces-plano-para-tipos)

# Programación Orientada a Objetos en C# y .NET 9
La Programación Orientada a Objetos gira en torno al concepto de objetos, que son instancias de clases, y C# integra estos conceptos perfectamente en su sintaxis. Exploraremos clases, objetos, herencia, polimorfismo, encapsulamiento y más. Vamos a sumergirnos en los fundamentos de la POO y cómo se manifiestan en C#.

## Clases y Objetos: Los Bloques de Construcción de la POO
En el núcleo de la Programación Orientada a Objetos están las clases y los objetos. Una clase es un plano o plantilla que define la estructura y el comportamiento de los objetos. Los objetos, por otro lado, son instancias de clases, que representan entidades del mundo real. C# simplifica la creación de clases y objetos, lo que lo convierte en un lenguaje ideal para la POO.

### Ejemplo 1: Creando una Clase Simple
```csharp
// Definición de la clase Carro
public class Carro {
    public string Marca { get; set; } = "";
    public string Modelo { get; set; } = "";
    public int Anio { get; set; } = 0;

    public void MostrarInfo() {
        Console.WriteLine($"Carro: {Marca} {Modelo}, Año: {Anio}");
    }
}
```

En este ejemplo, definimos una clase `Carro` con propiedades (`Marca`, `Modelo`, `Anio`) y un método (`MostrarInfo`) para mostrar información sobre el carro.

### Ejemplo 2: Creando Objetos a partir de una Clase
```csharp
// Creando objetos de la clase Carro
var carro1 = new Carro { Marca = "Toyota", Modelo = "Camry", Anio = 2022 };
var carro2 = new Carro { Marca = "Honda", Modelo = "Civic", Anio = 2021 };

// Llamando al método MostrarInfo en cada objeto carro
carro1.MostrarInfo();
carro2.MostrarInfo();
```

Aquí, creamos dos objetos (`carro1` y `carro2`) de la clase `Carro` y establecemos sus propiedades. Luego se llama al método `MostrarInfo` en cada objeto para mostrar su información.

## Constructores: Inicializando Objetos con Facilidad
Los constructores son métodos especiales en una clase que son responsables de inicializar las propiedades de un objeto cuando se crea. C# ofrece formas concisas y flexibles para definir constructores.

### Ejemplo 3: Constructor Primario
```csharp
// Clase con un constructor primario
public class Libro {
    public string Titulo { get; }
    public string Autor { get; }
    public int Anio { get; }

    public Libro(string titulo, string autor, int anio) {
        Titulo = titulo;
        Autor = autor;
        Anio = anio;
    }

    // Método para mostrar información sobre el libro
    public void MostrarInfo() {
        Console.WriteLine($"Libro: {Titulo} por {Autor}, Año: {Anio}");
    }
}
```

En este ejemplo, definimos una clase `Libro` con un constructor primario. Las propiedades (`Titulo`, `Autor`, `Anio`) se inicializan en el constructor.

### Ejemplo 4: Creando Objetos con Constructor Primario
```csharp
// Creando objetos usando el constructor primario
var libro1 = new Libro("El Alquimista", "Paulo Coelho", 1988);
var libro2 = new Libro("Matar a un ruiseñor", "Harper Lee", 1960);

// Llamando al método MostrarInfo en cada objeto libro
libro1.MostrarInfo();
libro2.MostrarInfo();
```

Se crean objetos (`libro1` y `libro2`) usando el constructor primario, proporcionando valores para las propiedades. Luego se llama al método `MostrarInfo` para mostrar información sobre cada libro.

### Ejemplo 5: Constructor Secundario
```csharp
public class Pelicula {
    public string Titulo { get; set; } = "";
    public string Director { get; set; } = "";
    public int Anio { get; set; } = 0;

    // Constructor secundario con parámetros adicionales
    public Pelicula(string titulo, string director, int anio) {
        Titulo = titulo;
        Director = director;
        Anio = anio;
    }

    // Método para mostrar información sobre la película
    public void MostrarInfo() {
        Console.WriteLine($"Pelicula: {Titulo} dirigida por {Director}, Año: {Anio}");
    }
}
```

Aquí, definimos una clase `Pelicula` con un constructor secundario que permite pasar parámetros adicionales al crear un objeto.

### Ejemplo 6: Creando Objetos con Constructor Secundario
```csharp
// Creando objetos usando el constructor secundario
var pelicula1 = new Pelicula("Inception", "Christopher Nolan", 2010);
var pelicula2 = new Pelicula("Sueño de fuga", "Frank Darabont", 1994);

// Llamando al método MostrarInfo en cada objeto película
pelicula1.MostrarInfo();
pelicula2.MostrarInfo();
```

Se crean objetos (`pelicula1` y `pelicula2`) usando el constructor secundario, proporcionando valores para los parámetros adicionales. El método `MostrarInfo` muestra información sobre cada película.

## Herencia: Construyendo Jerarquías de Clases
La herencia es un concepto fundamental en la POO que permite que una clase herede propiedades y comportamientos de otra clase. C# soporta la herencia de una sola clase, proporcionando una forma limpia y estructurada de construir jerarquías de clases.

### Ejemplo 7: Heredando de una Clase Base
```csharp
// Clase base
public class Animal {
    public string Nombre { get; }

    public Animal(string nombre) {
        Nombre = nombre;
    }

    public virtual void HacerSonido() {
        Console.WriteLine($"Animal {Nombre} hace un sonido genérico");
    }
}

// Clase derivada que hereda de Animal
public class Perro : Animal {
    public Perro(string nombre) : base(nombre) { }

    // Sobrescribiendo el método HacerSonido
    public override void HacerSonido() {
        Console.WriteLine($"Perro {Nombre} ladra fuerte");
    }
}
```

En este ejemplo, definimos una clase base (`Animal`) con una propiedad (`Nombre`) y un método (`HacerSonido`). La clase `Perro` hereda de `Animal` y sobrescribe el método `HacerSonido`.

### Ejemplo 8: Usando Clases Heredadas
```csharp
// Creando objetos de las clases base y derivada
var animalGenerico = new Animal("Genérico");
var perroPeludo = new Perro("Peludo");

// Llamando al método HacerSonido en cada objeto
animalGenerico.HacerSonido();
perroPeludo.HacerSonido();
```

Se crean objetos (`animalGenerico` y `perroPeludo`) de las clases base y derivada. Se llama al método `HacerSonido` en cada objeto, demostrando polimorfismo.

## Polimorfismo: Abrazando la Diversidad en Tipos
El polimorfismo permite que objetos de diferentes tipos sean tratados como objetos de un tipo base común. C# soporta el polimorfismo a través de la herencia de clases y la implementación de interfaces.

### Ejemplo 9: Usando Polimorfismo con Interfaces
```csharp
// Interfaz que define el comportamiento de sonido
public interface IHacedorDeSonido {
    void HacerSonido();
}

// Clase que implementa la interfaz IHacedorDeSonido
public class Gato : IHacedorDeSonido {
    public string Nombre { get; }

    public Gato(string nombre) {
        Nombre = nombre;
    }

    // Implementando el método HacerSonido
    public void HacerSonido() {
        Console.WriteLine($"Gato {Nombre} ronronea suavemente");
    }
}
```

Aquí, definimos una interfaz `IHacedorDeSonido` con un método `HacerSonido`. La clase `Gato` implementa esta interfaz.

### Ejemplo 10: Usando Polimorfismo con Objetos de Interfaz
```csharp
// Creando objetos de la interfaz y la clase que la implementa
IHacedorDeSonido hacedorDeSonido = new Gato("Bigotes");

// Llamando al método HacerSonido en el objeto de la interfaz
hacedorDeSonido.HacerSonido();
```

Se crea un objeto (`hacedorDeSonido`) de la interfaz `IHacedorDeSonido`, apuntando a una instancia de `Gato`. Se llama al método `HacerSonido` en el objeto de la interfaz, mostrando polimorfismo.

## Encapsulamiento: Protegiendo el Mundo Interior
El encapsulamiento es la práctica de agrupar los datos (propiedades) y los métodos que operan sobre los datos dentro de una sola unidad, conocida como clase. C# proporciona modificadores de visibilidad para controlar la accesibilidad de las propiedades y métodos.

### Ejemplo 11: Usando Modificadores de Visibilidad
```csharp
// Clase con propiedades privadas y públicas
public class CuentaBancaria {
    private double saldo = 0.0;

    // Método público para depositar dinero
    public void Depositar(double monto) {
        if (monto > 0) {
            saldo += monto;
            Console.WriteLine($"Depósito exitoso. Nuevo saldo: {saldo}");
        } else {
            Console.WriteLine("Monto de depósito inválido");
        }
    }

    // Método público para verificar el saldo
    public void VerificarSaldo() {
        Console.WriteLine($"Saldo actual: {saldo}");
    }
}
```

En este ejemplo, la clase `CuentaBancaria` tiene una propiedad privada (`saldo`) y métodos públicos (`Depositar`, `VerificarSaldo`). El `saldo` está encapsulado y su acceso está restringido a los métodos dentro de la clase.

### Ejemplo 12: Interactuando con la Clase Encapsulada
```csharp
// Creando un objeto de la clase CuentaBancaria
var cuenta = new CuentaBancaria();

// Realizando operaciones en el objeto
cuenta.Depositar(1000.0);
cuenta.Depositar(-500.0); // Monto de depósito inválido
cuenta.VerificarSaldo();
```

Se crea un objeto (`cuenta`) de la clase `CuentaBancaria`, y se realizan operaciones como depositar dinero y verificar el saldo. El encapsulamiento asegura que la propiedad `saldo` sea accedida y modificada solo a través de los métodos de la clase.

## Clases Abstractas e Interfaces: Plano para Tipos
Las clases abstractas y las interfaces proporcionan planos para que otras clases los sigan. Las clases abstractas pueden tener métodos abstractos y concretos, mientras que las interfaces solo declaran métodos abstractos.

### Ejemplo 13: Clase Abstracta
```csharp
// Clase abstracta con métodos abstractos y concretos
public abstract class Forma {
    public string Nombre { get; }

    protected Forma(string nombre) {
        Nombre = nombre;
    }

    // Método abstracto para calcular el área
    public abstract double CalcularArea();

    // Método concreto
    public void MostrarInfo() {
        Console.WriteLine($"{Nombre} - Área: {CalcularArea()}");
    }
}
```

Aquí, definimos una clase abstracta (`Forma`) con un método abstracto (`CalcularArea`) y un método concreto (`MostrarInfo`).

### Ejemplo 14: Clase Concreta que Extiende la Clase Abstracta
```csharp
// Clase concreta que extiende la clase abstracta
public class Circulo : Forma {
    public double Radio { get; }

    public Circulo(double radio) : base("Círculo") {
        Radio = radio;
    }

    // Sobrescribiendo el método abstracto para calcular el área
    public override double CalcularArea() {
        return 3.14 * Radio * Radio;
    }
}
```

La clase `Circulo` extiende la clase abstracta `Forma` y proporciona una implementación para el método abstracto.

### Ejemplo 15: Usando Clase Abstracta y Clase Concreta
```csharp
// Creando un objeto de la clase concreta
var circulo = new Circulo(5.0);

// Llamando a los métodos concretos y abstractos
circulo.MostrarInfo();
```

Se crea un objeto (`circulo`) de la clase `Circulo`, y se llama al método `MostrarInfo`, mostrando el uso de métodos abstractos y concretos.

### Ejemplo 16: Interfaz
```csharp
// Interfaz que define el comportamiento de una impresora
public interface IImpresora {
    void Imprimir(string documento);
}
```

Aquí, definimos una interfaz `IImpresora` con un solo método abstracto (`Imprimir`).

### Ejemplo 17: Clase que Implementa una Interfaz
```csharp
// Clase que implementa la interfaz IImpresora
public class ImpresoraLaser : IImpresora {
    // Implementando el método Imprimir
    public void Imprimir(string documento) {
        Console.WriteLine($"Imprimiendo documento: {documento} (Impresora Láser)");
    }
}
```

La clase `ImpresoraLaser` implementa la interfaz `IImpresora` y proporciona una implementación para el método `Imprimir`.

### Ejemplo 18: Usando Interfaz y Clase que la Implementa
```csharp
// Creando un objeto de la clase que implementa la interfaz
var impresoraLaser = new ImpresoraLaser();

// Llamando al método de la interfaz a través de la clase que la implementa
impresoraLaser.Imprimir("Informe de Ventas");
```

Se crea un objeto (`impresoraLaser`) de la clase `ImpresoraLaser`, y se llama al método `Imprimir`, demostrando el uso de interfaces.

## Clases de Datos: Simplificando la Creación de Clases de Datos
Las clases de datos en C# son clases diseñadas para almacenar datos. Proporcionan una forma concisa de crear clases con propiedades, y automáticamente generan métodos como `Equals`, `GetHashCode`, y `ToString`.

### Ejemplo 19: Definiendo una Clase de Datos
```csharp
// Definición de una clase de datos
public record Persona(string Nombre, int Edad);
```

En este ejemplo, definimos una clase de datos `Persona` con propiedades `Nombre` y `Edad`.

### Ejemplo 20: Usando una Clase de Datos
```csharp
// Creando objetos de la clase de datos
var persona1 = new Persona("Juan", 30);
var persona2 = new Persona("Ana", 25);

// Usando los métodos generados automáticamente
Console.WriteLine(persona1);
Console.WriteLine(persona2);
Console.WriteLine(persona1 == persona2);
```

Se crean objetos (`persona1` y `persona2`) de la clase de datos `Persona`, y se utilizan los métodos generados automáticamente como `ToString` y `Equals`.

