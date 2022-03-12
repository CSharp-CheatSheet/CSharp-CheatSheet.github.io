---
layout: single
title: "C# CheatSheet"
classes: wide
  - landing
#  - dark-theme
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"
last_modified_at: 2022-03-12
---

C# CheatSheet is a website storing teaching material for c# development.

---
# C# Environment Setup

Windows:
  * Visual Studio 2019, 2022: .Net 6, support Class Diagram
  * Visual Studio Code: .Net 5, support PUML Class Diagram

MacOS:
  * Visual Studio 2022: not yet support
  * Visual Studio 2019: .Net 5, support Class Diagram
  * Visual Studio Code: .Net 5, .Net 6, support PUML Class Diagram (tested on Mojave)

Linux:
  * Visual Studio Code: .Net 5, support PUML Class Diagram (not yet tested)

## Install IDE and .NET Framework

  * [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)
  * [Visual Studio Code](https://code.visualstudio.com), [.Net 5 or .Net 6 Runtime](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks), [Tutorial](https://www.c-sharpcorner.com/article/how-to-setup-visual-studio-code-for-c-sharp-10-and-net-6-0/)

## CSharp to PlantUML (For Visual Studio Code Users)

  * [CSharp to PlantUML](https://github.com/pierre3/PlantUmlClassDiagramGenerator)
  * Install
  ```bash
  $ dotnet tool install --global PlantUmlClassDiagramGenerator
  ```
  * Use
  ```bash
  $ puml-gen ./Program.cs -public
  ```
  * Copy the text from *.puml and visualize using [PUML Viewer](https://www.planttext.com)


## First Program

```bash
$ dotnet --info // check the version installed in your system
$ dotnet new console
```

In Program.cs
```csharp
using System
namespace MyApp
{
    class Program {         
        static void Main(string[] args) // Where the application begins
        {
            System.Console.WriteLine("Hello World!");
        }
    }
}
```

## How to Check the .Net Version

```bash
$ dotnet --version
```

## How to Build the Program

```bash
$ dotnet build
```

## How to Run the Program (Including Build)

```bash
$ dotnet run
```

---
# Selected Theory

## Naming Convention [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)

### Pascal Case
Use pascal casing ("PascalCasing") when naming a class, record, or struct. When naming public members of types, such as fields, properties, events, methods, and local functions, use pascal casing. When naming an interface, use pascal casing in addition to prefixing the name with an I. This clearly indicates to consumers that it's an interface.

### Camel Case
Use camel casing ("camelCasing") when naming private or internal fields, and prefix them with _.

---
# External Resources
