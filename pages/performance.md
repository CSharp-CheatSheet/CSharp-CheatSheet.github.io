---
# permalink: /about/
layout: single
title: "Performance"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---

## .NET process

Any process have three default streams:

- **Standard input (stdin)**: This is the only input stream for all terminal or console aps. When you cal Console.ReadLine or Console.Read the result is taken from this stream.
- **Standard Output (stdout)**: When you call output-related commands in the console singleton class, all data goes here. For example the WriteLine or the Write methods. The color and beeps commands send data to there too.
- **Standard error (stderr)**: This is a dedicated stream to print error-related content to the console. This is dedicated because some applications and scripting solutions want to hide these messages.

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            string name;
            Console.WriteLine("Hello, please tell me your name:");
            name = Console.ReadLine();
            Console.WriteLine("Hello {0} ", name);
        }
    }
}
```
```bash
$ Hello, please tell me your name:
$ Yun
$ Hello Yun
```

## Raising and handling events

# Handling Events [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.eventhandler-1?view=net-6.0)

##  Event Handler [Doc](https://docs.microsoft.com/en-us/dotnet/standard/events/)

```csharp
```
```bash
```

# Understanding processes, threads, and tasks

# Monitoring performance and resource usage

# Running tasks asynchronously


## Synchronizing access to shared resources

## Understanding async and await

---
# Selected Theory

## Deadlock
