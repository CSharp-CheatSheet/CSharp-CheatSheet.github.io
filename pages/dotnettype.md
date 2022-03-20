---
# permalink: /about/
layout: single
title: ".Net Type"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---


# Lambda Expression [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions)

You use a lambda expression to create an anonymous function. Use the lambda declaration operator **=>** to separate the lambda's parameter list from its body. A lambda expression can be of any of the following two forms:

* **Expression lambda** that has an expression as its body:

```csharp
(input-parameters) => expression
```

* **Statement lambda** that has a statement block as its body:

```csharp
(input-parameters) => { <sequence-of-statements> }
```


# Type-testing Operators and Cast Expression

## Implicit Casting

```csharp
WildCat leopard = new WildCat;
Cat petCat = leopard;
WildCat wCat = petCat;  // compile error
```

## Explicit Casting

```csharp
WildCat wCat = (WildCat)petCat;
```

## Avoiding Casting Exceptions

```csharp
// WildCat wCat = (WildCat)petCat;
if (petCat is WildCat)
{
    Console.WriteLine($"{nameof(petCat)} IS an WildCat");
    WildCat wCat = (WildCat)petCat;
    // safely do something with wCat
}
```

## is Operatpr

The **is** operator will check if the run-time type of an expression is compatible with a given type. The **as** operator considers only reference, nullable, boxing, and unboxing conversions.

```csharp
if (petCat is WildCat)
{
}
```

## as Operator

The **as** operator is used to explicitly convert an expression to a given type if its run-time type is compatible with that type. The as operator returns null if the conversion is not possible.

In MyBusiness/Program.cs,
```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    internal class Program
    {
        static void Main(string[] args)
        {
            object[] myObjects = new object[4];
            myObjects[0] = new Dog();
            myObjects[1] = new Cat();
            myObjects[2] = "Dog";
            myObjects[3] = "Cat";

            for (int i = 0; i < myObjects.Length; i++)
            {
                string? s = myObjects[i] as string;
                Console.Write($"Inspecting element: {myObjects[i]}");
                if (s == null)
                {
                    Console.Write(" --> Incompatible type");
                }
                else
                {
                    Console.Write(" --> Compatible type");
                }
                Console.WriteLine(", with string!");
            }
        }
    }
}
```

In PetLibrary/Animals.cs,
```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Animal
    {
        public virtual void Speak()
        {
            Console.WriteLine("");
        }
    }

    public class Dog : Animal
    {
        public override void Speak()
        {
            Console.WriteLine("Woof!");
        }
    }

    public class Cat : Animal
    {
        public override void Speak()
        {
            Console.WriteLine("Meow!");
        }
    }
}
```

---
# Inheriting and Extending .NET Types

## try-catch [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/try-catch)

The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.

When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.

In MyBusiness/Program.cs,
```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    internal class Program
    {
        static void Main(string[] args)
        {
            // Create a cat
            Cat coffee = new Cat("Coffee", new DateTime(2019, 6, 20));

            try
            {
                coffee.TimeTravel(new DateTime(2023, 12, 31));
                coffee.TimeTravel(new DateTime(1950, 12, 25));
            }
            catch (CatException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

In PetLibrary/Animals.cs,
```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Cat
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;

        /*
        Class methods, where functions should be implemented
        */

        // Constructors
        // Default constructor. It will be called by default
        public Cat()
        {
            Name = "Unknown";
            DateOfBirth = DateTime.Today;
        }
        // Parameterized Constructor
        public Cat(string name, DateTime dateOfBirth)
        {
            this.Name = name;
            this.DateOfBirth = dateOfBirth;
        }
        // Finalizer
        ~Cat()
        {
        }

        // method
        public void TimeTravel(DateTime when)
        {
            if (when <= DateOfBirth)
            {
                // It is a handler
                throw new CatException("If you travel back in time to a date earlier than your own birth, then the universe will explode!");
            }
            else
            {
                Console.WriteLine($"Welcome to {when:yyyy}!");
            }
        }

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }
    }

    public class WildCat : Cat
    {
        public string? CountryCode { get; set; }
        public DateTime FoundDate { get; set; }

        // hidden methods
        // based on the keyword new
        public new void WriteToConsole()
        {
            Console.WriteLine(format:
              "{0} was born on {1:dd/MM/yy} and found on {2:dd/MM/yy}",
              arg0: Name,
              arg1: DateOfBirth,
              arg2: FoundDate);
        }
    }

    public class CatException : Exception
    {
        // Unlike ordinary methods, constructors are not inherited,
        // so we must explicitly declare and explicitly call the base constructor implementations in System.Exception
        public CatException() : base() { }
        public CatException(string message) : base(message) { }
        public CatException(
          string message, Exception innerException)
          : base(message, innerException) { }
    }
}
```

```bash
$ Welcome to 2023!
$ If you travel back in time to a date earlier than your own birth, then the universe will explode!
```

## Raising and handling events

# Delegates [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)

# Handling Events [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.eventhandler-1?view=net-6.0)

##  Event Handler [Doc](https://docs.microsoft.com/en-us/dotnet/standard/events/)

## as is operators

---
# Selected Theory
