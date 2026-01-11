# Control Flow: Making Decisions and Loops

## Index
1. [Conditional Statements: Making Informed Decisions](#conditional-statements-making-informed-decisions)
2. [Loops: Repeating Tasks Efficiently](#loops-repeating-tasks-efficiently)
3. [Breaking and Continuing Loops](#breaking-and-continuing-loops)
4. [Labeling Loops](#labeling-loops)
5. [Making Decisions with Control Flow](#making-decisions-with-control-flow)
6. [Advanced Control Flow: `switch` with Ranges and Patterns](#advanced-control-flow-switch-with-ranges-and-patterns)
7. [Handling Edge Cases: `try`, `catch`, and `finally`](#handling-edge-cases-try-catch-and-finally)
8. [Practical Application: Building a Simple Calculator](#practical-application-building-a-simple-calculator)

# Control Flow: Making Decisions and Loops

We will explore the power of conditional statements, such as `if` and `else`, and learn how to create loops to iterate through code efficiently. These constructs are the backbone of dynamic and responsive programming, allowing your C# applications to adapt to changing conditions and user interactions.

## Conditional Statements: Making Informed Decisions

Conditional statements allow your program to make decisions based on certain conditions. The most common form is the `if` statement, which evaluates a condition and executes a block of code if the condition is true.

### Example 1: Basic `if` Statement

```csharp
int temperature = 25;
if (temperature > 30)
{
    Console.WriteLine("It's hot!");
}
else if (temperature >= 20 && temperature <= 30)
{
    Console.WriteLine("The weather is nice.");
}
else
{
    Console.WriteLine("It's a bit cold.");
}
```

In this example, the program evaluates the temperature and prints a message accordingly. The `else if` block allows for multiple conditions, providing a more nuanced decision-making process.

### Example 2: Expressive `switch` Statement

The `switch` statement is a versatile alternative to the traditional `switch` statement in other languages. It evaluates multiple conditions and executes the block corresponding to the first true condition.

```csharp
string dayOfWeek = "Wednesday";
switch (dayOfWeek)
{
    case "Monday":
        Console.WriteLine("It's the start of the week.");
        break;
    case "Wednesday":
    case "Thursday":
        Console.WriteLine("Midweek!");
        break;
    case "Saturday":
        Console.WriteLine("The weekend is here!");
        break;
    default:
        Console.WriteLine("Another day.");
        break;
}
```

Here, the `switch` statement checks the value of `dayOfWeek` and prints a message based on the matching condition. The `default` block serves as a fallback for any non-matching values.

## Loops: Repeating Tasks Efficiently

Loops are essential for performing repetitive tasks and iterating through collections or sequences of data. C# offers both `for` and `while` loops to suit different scenarios.

### Example 3: `for` Loop

The `for` loop is excellent for iterating through ranges, arrays, or any iterable object.

```csharp
// Printing numbers from 1 to 5
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine($"Count: {i}");
}
```

In this example, the `for` loop iterates through the range from 1 to 5, printing the count in each iteration. The `in` keyword simplifies the syntax, making it more readable.

### Example 4: `while` Loop

The `while` loop repeats a block of code while a specified condition is true.

```csharp
int countdown = 3;
while (countdown > 0)
{
    Console.WriteLine($"Countdown: {countdown}");
    countdown--;
}
```

Here, the `while` loop creates a countdown by printing the current value of `countdown` until it reaches zero. The loop continues as long as the condition `countdown > 0` is true.

### Example 5: `do-while` Loop

Similar to the `while` loop, the `do-while` loop executes the block of code first and then checks the condition. This ensures that the block is executed at least once.

```csharp
int attempts = 0;
do
{
    Console.WriteLine("Trying to connect...");
    attempts++;
} while (attempts < 3);
```

In this example, the program attempts to connect, and the loop continues until `attempts` reach a maximum of three. This guarantees that at least one connection attempt is made.

## Breaking and Continuing Loops

In some cases, you may want to exit a loop prematurely or skip to the next iteration. C# provides the `break` and `continue` statements for these scenarios.

### Example 6: `break` Statement

The `break` statement terminates the innermost loop in which it is located.

```csharp
for (int i = 1; i <= 10; i++)
{
    if (i == 5)
    {
        Console.WriteLine($"Breaking at {i}");
        break;
    }
    Console.WriteLine($"Iteration: {i}");
}
```

In this example, the loop iterates from 1 to 10, but when `i` reaches 5, the `break` statement is triggered, and the loop ends.

### Example 7: `continue` Statement

The `continue` statement skips the rest of the code in the loop for the current iteration and moves to the next one.

```csharp
for (int i = 1; i <= 5; i++)
{
    if (i == 3)
    {
        Console.WriteLine($"Skipping iteration {i}");
        continue;
    }
    Console.WriteLine($"Iteration: {i}");
}
```

Here, when `i` is equal to 3, the `continue` statement is executed, skipping the rest of the loop for that iteration.

## Labeling Loops

In nested loops, C# allows you to label them and specify which loop to break or continue.

### Example 8: Labeled `break`

```csharp
outerLoop: for (int i = 1; i <= 3; i++)
{
    for (int j = 1; j <= 3; j++)
    {
        if (i * j == 6)
        {
            Console.WriteLine($"Breaking at {i}, {j}");
            break outerLoop;
        }
        Console.WriteLine($"Iteration: {i}, {j}");
    }
}
```

In this example, the outer loop is labeled as `outerLoop`. When the condition `i * j == 6` is met, the `break outerLoop` statement terminates both loops.

### Example 9: Labeled `continue`

```csharp
outerLoop: for (int i = 1; i <= 3; i++)
{
    for (int j = 1; j <= 3; j++)
    {
        if (i == 2 && j == 2)
        {
            Console.WriteLine($"Skipping iteration {i}, {j}");
            continue outerLoop;
        }
        Console.WriteLine($"Iteration: {i}, {j}");
    }
}
```

Here, when `i` is 2 and `j` is 2, the `continue outerLoop` statement skips the rest of the inner loop for that iteration.

## Making Decisions with Control Flow

Control flow is about making decisions in your program, and combining conditional statements with loops can create powerful and responsive applications. Let's explore a more complex example that integrates these concepts.

### Example 10: Dynamic Program Flow

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
foreach (var number in numbers)
{
    if (number % 2 == 0)
    {
        Console.WriteLine($"Even number: {number}");
    }
    else
    {
        Console.WriteLine($"Odd number: {number}");
    }
}
```

In this example, the program iterates through a list of numbers. For each number, it checks if it is even or odd using the modulo operator (`%`). The result is printed dynamically, showcasing the decision-making capability of control flow.

## Advanced Control Flow: `switch` with Ranges and Patterns

The `switch` statement in C# is a powerful tool for making decisions. It is not limited to simple equality checks; you can use it with ranges and even patterns.

### Example 11: Using `switch` with Ranges

```csharp
int score = 85;
switch (score)
{
    case int n when (n >= 90 && n <= 100):
        Console.WriteLine("A");
        break;
    case int n when (n >= 80 && n < 90):
        Console.WriteLine("B");
        break;
    case int n when (n >= 70 && n < 80):
        Console.WriteLine("C");
        break;
    default:
        Console.WriteLine("Failed");
        break;
}
```

In this example, the program evaluates the `score` and prints the corresponding grade based on the defined ranges.

### Example 12: Using `switch` with Patterns

```csharp
object result = "Success";
switch (result)
{
    case string s:
        Console.WriteLine($"The result is a string: {s}");
        break;
    case int i:
        Console.WriteLine($"The result is an integer: {i}");
        break;
    case bool b:
        Console.WriteLine($"The result is a boolean: {b}");
        break;
    default:
        Console.WriteLine("Unknown result type");
        break;
}
```

Here, the `switch` statement uses patterns to check the type of the `result` variable and prints a message accordingly. The `is` keyword is used for type checking.

## Handling Edge Cases: `try`, `catch`, and `finally`

In the real world, your programs may encounter unexpected situations or errors. C# provides a robust exception handling mechanism with `try`, `catch`, and `finally` blocks.

### Example 13: Exception Handling

```csharp
int Divide(int a, int b)
{
    try
    {
        return a / b;
    }
    catch (DivideByZeroException e)
    {
        Console.WriteLine($"Error: {e.Message}");
        return -1;
    }
    finally
    {
        Console.WriteLine("Division attempt completed.");
    }
}
int result = Divide(10, 0);
Console.WriteLine($"Division result: {result}");
```

In this example, the `Divide` function attempts to perform a division. If a `DivideByZeroException` occurs (such as dividing by zero), the `catch` block handles the exception and prints an error message. The `finally` block executes regardless of whether an exception occurs, providing a cleanup or finalization step.

## Practical Application: Building a Simple Calculator

To tie everything together, let's build a simple calculator program using control flow constructs. This program will accept user input for two numbers and an operation, perform the calculation, and display the result.

### Example 14: Simple Calculator Program

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Welcome to the Simple Calculator!");
        Console.Write("Enter the first number: ");
        if (!double.TryParse(Console.ReadLine(), out double num1))
        {
            Console.WriteLine("Invalid input. Exiting.");
            return;
        }
        Console.Write("Enter the second number: ");
        if (!double.TryParse(Console.ReadLine(), out double num2))
        {
            Console.WriteLine("Invalid input. Exiting.");
            return;
        }
        Console.Write("Select the operation (+, -, *, /): ");
        string operation = Console.ReadLine();
        double? result = operation switch
        {
            "+" => num1 + num2,
            "-" => num1 - num2,
            "*" => num1 * num2,
            "/" => num2 != 0 ? num1 / num2 : (double?)null,
            _ => null
        };
        if (result.HasValue)
        {
            Console.WriteLine($"Result: {result}");
        }
        else
        {
            Console.WriteLine("Invalid operation or division by zero.");
        }
    }
}
