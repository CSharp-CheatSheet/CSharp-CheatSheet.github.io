---
# permalink: /about/
layout: single
title: "Collections"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---

# Static and Dynamic Data Structure

## Array (Static at Runtime)

```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            Cat[] catArray = new Cat[3];
            List<Cat> catList = new List<Cat>();

            // Initialize an array
            catArray[0] = new Cat("Nana");
            catArray[1] = new Cat("Coffee");
            catArray[2] = new Cat("Kiwi");

            // Iterate the array to create cats
            catList.Add(new Cat("Nana"));
            catList.Add(new Cat("Coffee"));
            catList.Add(new Cat("Kiwi"));
        }
    }
}
```

```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Cat
    {
        public string Name{ get; set; }

        public Cat()
        {
            this.Name = "unknown";
        }
        public Cat( string name )
        {
            this.Name = name;
        }
    }
}
```

# Collections

If you need to store multiple values in a variable, then you can use a collection. A **collection** is a data structure in memory that can manage multiple items in different ways. In comparison to an **array**, collections enable dynamic changes.

# System.Collections.Generic Namespace [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic?view=net-6.0)

* System.Collections: Interfaces and base classes used by collections.
* System.Collections.Generic: Introduced in C# 2.0 with .NET Framework 2.0. These collections allow you to specify the type you want to store using a generic type parameter (which is safer, faster, and more efficient).
* System.Collections.Concurrent
* System.Collections.Immutable

# Common Features of All Collections

All collections implement the **ICollection** interface; this means that they must have a Count property to tell you how many objects are in them.

```csharp
int listCount = catList.Count;
Console.WriteLine($"The total elements in the list is {listCount}.");
```

All collections implement the IEnumerable interface, which means that they must have a
GetEnumerator method that returns an object that implements IEnumerator; this means that
the returned object must have a MoveNext method and a Current property so that they can be
iterated using the foreach statement.

```csharp
// The foreach statement
foreach (Cat cat in catList)
{
    // do something with each cat
    Console.WriteLine($"The name of the cat is {cat.Name}.");
}
```

## List<T> - std::vector<T>

* Lists are a good choice when you want to manually control the order of items in a collection.

|Index   |Item    |
|--------|--------|
|0       |Austria |
|1       |Taiwan  |
|2       |Austria |
|3       |Germany |

```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            List<string> countryList = new List<string>();
            countryList.Add("Austria");
            countryList.Add("Taiwan");
            countryList.Add("Austria");
            countryList.Add("Germany");

            foreach (string item in countryList)
            {
                Console.WriteLine(item);
            }
        }
    }
}
```
```bash
$ Austria
$ Taiwan
$ Austria
$ Germany
```

## Dictionary<TKey, TValue> - unordered_map<Key, Data>

```csharp
```

## HashSet<T> - unordered_set<Key>

```csharp
```

## SortedDictionary<TKey, TValue> - std::map<Key, Data>

```csharp
```

## SortedList<TKey, TValue> - equivalent to a std::vector<T> but keeping it ordered by using binary search + insert when adding elements.

```csharp
```

## SortedSet<T> - std::set<Key>

```csharp
```

## Queue<T> - std::queue<T>

```csharp
```

## Stack<T> - std::stack<T>

```csharp
```

## LinkedList<T> - std::list<T>

```csharp
```


---
# Selected Theory
