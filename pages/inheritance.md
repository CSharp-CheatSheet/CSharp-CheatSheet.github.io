---
# permalink: /about/
layout: single
title: "Inheritance"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---

# Other Properties of Methods
## Types of the Methods
* **Instance methods** are actions that an object does to itself.
  * A mom cat procreates a kitty by taking a dad cat as an input.
  * The mom cat cannot produce kitties from multiple dad cats.
* **Static methods** are actions the type does.
  * The owner of the cats encourages them to procreate a kitty.
  * The owner can pair many cat couples at the same time.

```csharp
using System;
using System.Collections.Generic;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    internal class Program
    {
        static void Main(string[] args)
        {
            // Create 3 cats and initialize them
            Cat nana = new Cat("Nana", new DateTime(2019, 12, 9));
            Cat coffee = new Cat("Coffee", new DateTime(2019, 6, 20));
            Cat kiwi = new Cat("Kiwi", new DateTime(2018, 11, 19));

            // Print out the present content
            nana.WriteToConsole();
            coffee.WriteToConsole();
            kiwi.WriteToConsole();

            // Call instance method
            Cat kitty1 = nana.ProduceKittyWith(coffee);
            kitty1.Name = "Naffee";
            // Call static method
            Cat kitty2 = Cat.ProduceKitty(kiwi, coffee);
            // The following statement functions as the above one
            // Cat kitty2 = kiwi * coffee;
            kitty1.Name = "Kiffee";

            // Print out the kitty name
            Console.WriteLine($"{nana.Name} has {nana.Children.Count} kitty.");
            Console.WriteLine($"{coffee.Name} has {coffee.Children.Count} kitty.");
            Console.WriteLine($"{kiwi.Name} has {kiwi.Children.Count} kitty.");
            Console.WriteLine(
            format: "{0}'s first kitty is named \"{1}\".",
            arg0: coffee.Name,
            arg1: coffee.Children[0].Name);
        }
    }
}

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
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

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

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Static method to "multiply"
        public static Cat ProduceKitty(Cat cat1, Cat cat2)
        {
            Cat kitty = new Cat
            {
                Name = $"Baby of {cat1.Name} and {cat2.Name}"
            };
            cat1.Children.Add(kitty);
            cat2.Children.Add(kitty);
            return kitty;
        }

        // Use operators instead of the above method
        public static Cat operator * (Cat cat1, Cat cat2)
        {
            return Cat.ProduceKitty(cat1, cat2);
        }

        // Instance method to "multiply"
        public Cat ProduceKittyWith(Cat partner)
        {
            return ProduceKitty(this, partner);
        }
    }
}
```
```bash
$ Nana was born on a Monday.
$ Coffee was born on a Thursday.
$ Kiwi was born on a Monday.
$ Nana has 1 kitty.
$ Coffee has 2 kitty.
$ Kiwi has 1 kitty.
$ Coffee\'s first kitty is named "Kiffee".
```

## Local (Nested/Inner) Functions

**Local functions** are private methods of a type that are nested in another member.

```csharp
public Cat ProduceKittyWith(Cat partner)
{
    // This is a local function
    bool testIfInLove(Cat partner)
    {
        return true;
    }

    // Test if the cat is in love with the partner.
    testIfInLove( partner);

    return ProduceKitty(this, partner);
}
```

---
# Splitting Files to Organize Them
```bash
// Create a folder named MyBusiness
MyBusiness> mkdir MyBusiness
// Create a folder named PetLibrary
MyBusiness> mkdir PetLibrary
// Enter the folder MyBusiness
MyBusiness> cd MyBusiness
// Set up a console application
MyBusiness/MyBusiness> $ dotnet new console
// Leave the folder MyBusiness and enter the folder PetLibrary
MyBusiness/MyBusiness> $ cd ../PetLibrary
// Set up a class library
MyBusiness/PetLibrary> $ dotnet new classlib
MyBusiness/PetLibrary> $ mv Class1.cs Animals.cs
// Go back to the folder MyBusiness and run the program
MyBusiness/PetLibrary> $ cd ../MyBusiness
MyBusiness/MyBusiness> $ dotnet run
```

In MyBusiness.csproj, you see the configuration of the program
```csharp
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  // Set environment variable
  <ItemGroup>
    <ProjectReference
      // On Windows
      Include="..\PetLibrary\PetLibrary.csproj" />
      // On MacOS, Unix
      Include="../PetLibrary/PetLibrary.csproj" />        
      // The slash and backslash presentation used to describe a path were not
      // standardized. It causes a lot of pain.
      // Some morden editors automatically convert them.
  </ItemGroup>

</Project>
```

In MyBusiness/Program.cs,
```csharp
using System;
using System.Collections.Generic;
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
            Cat nana = new Cat("Nana", new DateTime(2019, 12, 9));
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
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

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

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Static method to "multiply"
        public static Cat ProduceKitty(Cat cat1, Cat cat2)
        {
            Cat kitty = new Cat
            {
                Name = $"Baby of {cat1.Name} and {cat2.Name}"
            };
            cat1.Children.Add(kitty);
            cat2.Children.Add(kitty);
            return kitty;
        }

        // Use operators instead of the above method
        public static Cat operator *(Cat cat1, Cat cat2)
        {
            return Cat.ProduceKitty(cat1, cat2);
        }

        // Instance method to "multiply"
        public Cat ProduceKittyWith(Cat partner)
        {
            return ProduceKitty(this, partner);
        }
    }
}
```

---
# Inheriting Classes
In C#, classes are used to create custom types. Inheritance is the process by which one class inherits the members of another class.

# Self-Defined Interface [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)
An **interface** defines a contract. Any class or struct that implements that contract must provide an implementation of the members defined in the interface. Note that you cannot apply access modifiers to interface members.

In MyBusiness/Program.cs,
```csharp
using System;
using System.Collections.Generic;
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
            Cat nana = new Cat("Nana", new DateTime(2019, 12, 9));
            double speed = nana.SpeedUp(2);
            Console.WriteLine($"{nana.Name} is running at speed {speed} km/hr."); ;
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
    public class Cat : IRun
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

        /*
        Class methods, where functions should be implemented
        */

        // Constructors
        // Default constructor. It will be called by default
        public Cat()
        {
            Speed = 0.0;
            Name = "Unknown";
            DateOfBirth = DateTime.Today;
        }
        // Parameterized Constructor
        public Cat(string name, DateTime dateOfBirth)
        {
            Speed = 0.0;
            this.Name = name;
            this.DateOfBirth = dateOfBirth;
        }
        // Finalizer
        ~Cat()
        {
        }

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Static method to "multiply"
        public static Cat ProduceKitty(Cat cat1, Cat cat2)
        {
            Cat kitty = new Cat
            {
                Name = $"Baby of {cat1.Name} and {cat2.Name}"
            };
            cat1.Children.Add(kitty);
            cat2.Children.Add(kitty);
            return kitty;
        }

        // Use operators instead of the above method
        public static Cat operator *(Cat cat1, Cat cat2)
        {
            return Cat.ProduceKitty(cat1, cat2);
        }

        // Instance method to "multiply"
        public Cat ProduceKittyWith(Cat partner)
        {
            return ProduceKitty(this, partner);
        }

        // Implementation of interface IRun
        public double Speed { get; set; }
        public int Distance { get; }
        public double SpeedUp(double velocity)
        {
            Speed += velocity;
            return Speed;
        }
    }

    // IRun is an interface
    // You have variables and methods, but you don't implement them.
    interface IRun
    {
        double Speed { get; set; }
        int Distance { get; }

        double SpeedUp(double velocity);
    }
}
```
```bash
$ Nana is running at speed 2 km/hr.
```

# System-Defined Interface [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)

In MyBusiness/Program.cs,
```csharp
using System;
using System.Collections.Generic;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    internal class Program
    {
        static void Main(string[] args)
        {
            // Create a cat array
            Cat[] cats =
            {
                new Cat("Nana", new DateTime(2019, 12, 9)),
                new Cat("Coffee", new DateTime(2019, 6, 20)),
                new Cat("Kiwi", new DateTime(2018, 11, 19))
            };

            // Print the array
            for (int i = 0; i < cats.Length; i++)
            {
                Console.WriteLine($"{cats[i].Name}");
            }

            // Sort the array
            Array.Sort(cats);

            // Print the array again
            Console.WriteLine("Use Cat's IComparable implementation to sort the cat instance:");
            for (int i = 0; i < cats.Length; i++)
            {
                Console.WriteLine($"{cats[i].Name}");
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
    public class Cat : IComparable<Cat>
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

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

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Implementation of interface IComparible
        // Also check the class "public class Cat : IComparable<Cat>"
        public int CompareTo(Cat? other)
        {
            if (other != null)
                return Name.CompareTo(other.Name);
            else
                return 0;
        }
    }
}
```
```bash
$ Nana
$ Coffee
$ Kiwi
$ Use Cat\'s IComparable implementation to sort the cat instance:
$ Coffee
$ Kiwi
$ Nana
```

# Generics [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics)

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
            // Cat is currently flexible, because any type can be set for the food field and input parameter.
            // But there is no type checking, so inside the CheckFood method,
            // we cannot safely do much and the results are sometimes not what you might expect
            var t1 = new Cat();
            t1.food = 5;
            Console.WriteLine($"Cat food with an integer: {t1.CheckFood(5)}");
            var t2 = new Cat();
            t2.food = "fish";
            Console.WriteLine($"Cat food with a string: {t2.CheckFood("fish")}");

            // The type is defined at allocation
            var gt1 = new GenericCat<int>();
            gt1.food = 5;
            Console.WriteLine($"Cat food with an integer: {gt1.CheckFood(5)}");
            var gt2 = new GenericCat<string>();
            gt2.food = "fish";
            Console.WriteLine($"Cat food with a string: {gt2.CheckFood("fish")}");

            // generic methods
            string food1 = "4";
            Console.WriteLine("Double cat food {0} to {1}",
              arg0: food1,
              arg1: GenericMethodCat.DoubleMyFood<string>(food1));
            byte food2 = 3;
            Console.WriteLine("Double cat food {0} to {1}",
              arg0: food2,
              arg1: GenericMethodCat.DoubleMyFood(food2));
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
    // Working with non-generic types
    public class Cat
    {
        public object? food = default(object);
        public string CheckFood(object input)
        {
            if (food == input)
            {
                return "Expected food and input are the same.";
            }
            else
            {
                return "Expected food and input are NOT the same.";
            }
        }
    }

    // Working with generic types
    // One can consider T as a kind of template
    public class GenericCat<T> where T : IComparable
    {
        // A default() returns the default value of type parameter. Here is used for initialization.
        public T? food = default(T?);

        public string CheckFood(T input)
        {
            if (food == null)
            {
                return "Expected food is empty.";
            }
            else if (food.CompareTo(input) == 0)
            {
                return "Expected food and input are the same.";
            }
            else
            {
                return "Expected food and input are NOT the same.";
            }
        }
    }

    // Working with generic methods
    // One can consider T as a kind of template
    public class GenericMethodCat
    {
        public static double DoubleMyFood<T>(T input)
        where T : IConvertible
        {
            // convert using the current culture
            double d = input.ToDouble(
                Thread.CurrentThread.CurrentCulture);   
                // A system method to convert a string to a double, we simply use it for now.
            return 2 * d;
        }
    }
}
```
```bash
$ Cat food with an integer: Expected food and input are NOT the same.
$ Cat food with a string: Expected food and input are the same.
$ Cat food with an integer: Expected food and input are the same.
$ Cat food with a string: Expected food and input are the same.
$ Double cat food 4 to 8
$ Double cat food 3 to 6
```

# Class Inheritance [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)
**Inheritance**, together with encapsulation and polymorphism, is one of the three primary characteristics of object-oriented programming.

In PetLibrary/Animals.cs, add another class
```csharp
public class WildCat : Cat
{
    public string? CountryCode { get; set; }
    public DateTime FoundDate { get; set; }

    // overridden methods
    public override string ToString()
    {
        return $"{Name}'s code is {CountryCode}";
    }

    // hidden methods
    public new void WriteToConsole()
    {
        Console.WriteLine(format:
          "{0} was born on {1:dd/MM/yy} and found on {2:dd/MM/yy}",
          arg0: Name,
          arg1: DateOfBirth,
          arg2: FoundDate);
    }
}
```

In MyBusiness/Program.cs,
```csharp
using System;
using System.Collections.Generic;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    internal class Program
    {
        static void Main(string[] args)
        {
            // Create a cat array
            Cat[] cats =
            {
                new Cat("Nana", new DateTime(2019, 12, 9)),
                new Cat("Coffee", new DateTime(2019, 6, 20)),
                new Cat("Kiwi", new DateTime(2018, 11, 19))
            };

            // Initialize objects by using an object initializer
            // Cat: base class or parent class
            // Wild: derived class or child class
            WildCat leopard = new WildCat
            {
                Name = "Alice",
                CountryCode = "Taiwan"
            };
            Cat petCat = leopard;

            leopard.WriteToConsole();
            petCat.WriteToConsole();
            Console.WriteLine(leopard.GetName());
            Console.WriteLine(petCat.GetName());        // It is calling the method from the derived class. Strange?
                                                        // The compiler is not smart, thus casting is important!
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
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

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

        // Must should have existed from the parent class, from System.Object in this case
        public override string ToString()
        {
            return Name;
        }

        public virtual string GetName()
        {
            return Name;
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

        // overridden methods
        // based on the keyword overide
        public override string ToString()
        {
            return $"{Name}: from {CountryCode}";
        }

        public override string GetName()
        {
            return $"{Name}: from {CountryCode}";
        }

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
}
```

# Virtual Function [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/virtual)

---
# Selected Theory

## Useful Advanced C# Data Structure

* Collections [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/collections). We will introduce one-by-one later.
