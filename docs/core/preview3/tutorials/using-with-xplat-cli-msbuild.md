---
title: "使用命令行在 Windows/Linux/macOS 上开始使用 .NET Core（.NET Core 工具 RC4）| Microsoft 文档"
description: "使用命令行接口 (CLI) 在 Windows、Linux 或 macOS 上入门 .NET Core"
keywords: ".NET、.NET Core"
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 41632e63-d5c6-4427-a09e-51dc1116d45f
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 4c17da61f492e17edf4d69d79be430ead3dd0cc6

---

# <a name="getting-started-with-net-core-on-windowslinuxmacos-using-the-command-line-net-core-tools-rc4"></a>使用命令行在 Windows/Linux/macOS 上开始使用 .NET Core（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅[使用命令行在 Windows/Linux/macOS 上实现 .NET Core 入门](../../tutorials/using-with-xplat-cli.md)主题。

本指南介绍如何使用 .NET Core CLI 工具生成跨平台控制台应用。  将从最基本的控制台应用开始介绍，最终涵盖包括测试在内的多个项目。 基于已经了解和生成的应用，逐步添加这些功能。

如果熟悉 .NET Core CLI 工具集，请阅读 [.NET Core SDK 概述](../tools/dotnet.md)。

## <a name="prerequisites"></a>先决条件

开始之前，请确保已安装 [.NET Core CLI 工具 RC4 或更高版本](https://github.com/dotnet/core/blob/master/release-notes/preview3-download.md)。  还需要一个文本编辑器。

## <a name="hello-console-app"></a>Hello，控制台应用！

首先，导航到一个文件夹或使用喜欢的名称新建一个文件夹。  “Hello”是为示例代码选择的名称，可在[此处](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/HelloMsBuild)找到它。

打开命令提示符，键入下列命令：

```
$ dotnet new
$ dotnet restore
$ dotnet run
```

让我们进行快速演练：

1. `$ dotnet new`

   [`dotnet new`](../tools/dotnet-new.md) 会创建一个最新的 `Hello.csproj` 项目文件，其中包含生成控制台应用所必需的依赖项。  它还将创建 `Program.cs`，这是包含应用程序的入口点的基本文件。
   
   `Hello.csproj`：
   ```xml
    <Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
        <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
        
        <PropertyGroup>
            <OutputType>Exe</OutputType>
            <TargetFramework>netcoreapp1.0</TargetFramework>
        </PropertyGroup>

        <ItemGroup>
            <Compile Include="**\*.cs" />
            <EmbeddedResource Include="**\*.resx" />
        </ItemGroup>

        <ItemGroup>
            <PackageReference Include="Microsoft.NETCore.App">
                <Version>1.0.1</Version>
            </PackageReference>
            <PackageReference Include="Microsoft.NET.Sdk">
                <Version>1.0.0-alpha-20161104-2</Version>
                <PrivateAssets>All</PrivateAssets>
            </PackageReference>
        </ItemGroup>
        
        <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
    </Project>
   ```

   项目文件指定还原依赖项和生成程序所需的一切。

   * `Import` 标记引入了一些对所有 .NET Core 项目都通用的属性。
   * `OutputType` 标记指定我们要生成的可执行文件，即控制台应用程序。
   * `TargetFramework` 标记指定我们面向的 .NET 运行时。 在高级方案中，可以指定多个目标框架，并在单个操作中生成所有目标框架。 在本教程中，我们将仅针对 .NET Core 1.0 进行生成。
   * `Compile` 标记告诉编译器生成当前目录及所有具有 `.cs` 文件扩展名的子目录（即项目中的所有 C# 文件）中的所有文件。 在高级方案中可以排除文件，但在本教程中，且在大多数简单方案中，此行可以保持不变。
   * `EmbeddedResource` 标记指示生成系统将扩展名 `.resx` 的本地化文件嵌入到编译的可执行文件。 在本教程中，我们不会使用该功能。
   * `PackageReference` 标记指定在生成应用程序时必须还原和包括哪些依赖项包。 每个包引用指定 `Include` 属性下包的名称和版本号。 在最高级方案下，你将添加多个包引用。 也可以引用磁盘上的其他项目。

   `Program.cs`：
   ```csharp
   using System;

   namespace ConsoleApplication
   {
       public class Program
       {
           public static void Main(string[] args)
           {
               Console.WriteLine("Hello World!");
           }
       }
   }
   ```

   该程序从 `using System` 开始，这意味着“将 `System` 命名空间中的所有内容都纳入此文件的作用域”。 `System` 命名空间包括基本结构，如 `string` 或数值类型。

   然后我们定义一个名为“ConsoleApplication”的命名空间。 你可以将其更改为任何你喜欢的名称。 在该命名空间中定义了一个名为“Program”的类，其中 `Main` 方法将字符串数组作为其参数。 此数组将包含在调用编译的程序时所传递的参数列表。 按照这样，不使用此数组：程序所进行的全部操作就是编写“Hello World!” “Hello World!”。 可以通过将 `Console.WriteLine` 更改为以下代码来使事情更有趣。

   ```csharp
   if (args.Length > 0)
   {
       Console.WriteLine($"Hello {args[0]}!");
   }
   else
   {
       Console.WriteLine("Hello World!");
   }
   ```

2. `$ dotnet restore`

   [`dotnet restore`](../tools/dotnet-restore.md) 调用到 [NuGet](http://nuget.org)（.NET 的包管理器）以还原依赖项树。 NuGet 分析 `Hello.csproj` 文件、下载文件中所述的依赖项（或从计算机缓存中获取）并编写 `obj/project.assets.json` 文件。  需要 `project.assets.json` 文件才可进行编译和运行。
   
   `project.assets.json` 文件是 NuGet 依赖项和其他描述应用的信息的持久化完整图片集。  此文件由其他工具（如 `dotnet build` 和 `dotnet run`）读取，让它们可以使用正确的 NuGet 依赖项和绑定解决方法集处理源代码。
   
3. `$ dotnet run`

   [`dotnet run`](../tools/dotnet-run.md) 调用 `dotnet build` 来确保已生成要生成的目标，然后调用 `dotnet <assembly.dll>` 运行目标应用程序。
   
    ```
    $ dotnet run
    Hello World!
    ```

    或者，还可以执行 [`dotnet build`](../tools/dotnet-build.md) 来编译代码，无需运行已生成的控制台应用程序。 这使得 `bin/Debug/netcoreapp1.0/Hello.dll` 编译的应用程序可以在 Windows 上使用 `dotnet bin\Debug\netcoreapp1.0\Hello.dll` 运行，在其他系统上使用 `dotnet bin/Debug/netcoreapp1.0/Hello.dll` 运行。 可以在命令行上指定一个附加参数（假设在 Windows 上）：

    ```
    $ dotnet bin\Debug\netcoreapp1.0\Hello.dll .NET
    Hello .NET!
    ```

    在高级方案中，可以将应用程序作为独立的特定于平台的文件集生成，该应用程序可以在未安装 .NET Core 的计算机上部署或运行。 请参阅 [.NET Core 应用程序部署](../deploying/index.md)了解详细信息。

### <a name="augmenting-the-program"></a>扩充程序

让我们对此文件进行些微更改。  斐波那契数字很有意思，我们来尝试一下：

`Program.cs`：

```csharp
using static System.Console;

namespace ConsoleApplication
{
    public class Program
    {
        public static int FibonacciNumber(int n)
        {
            int a = 0;
            int b = 1;
            int tmp;
            
            for (int i = 0; i < n; i++)
            {
                tmp = a;
                a = b;
                b += tmp;
            }
            
            return a;   
        }
        
        public static void Main(string[] args)
        {
            WriteLine("Hello World!");
            WriteLine("Fibonacci Numbers 1-15:");
            
            for (int i = 0; i < 15; i++)
            {
                WriteLine($"{i+1}: {FibonacciNumber(i)}");
            }
        }
    }
}
```

运行程序（假设在 Windows 上并已将项目目录名称更改为 Fibonacci）：

```
$ dotnet build
$ dotnet bin\Debug\netcoreapp1.0\win10-x64\Fibonacci.exe
1: 0
2: 1
3: 1
4: 2
5: 3
6: 5
7: 8
8: 13
9: 21
10: 34
11: 55
12: 89
13: 144
14: 233
15: 377
```

就是这么简单！  可以按任意喜欢的方式扩充 `Program.cs`。

## <a name="adding-some-new-files"></a>添加一些新文件

对于简单的一次性程序，单个文件即可，但如果要生成含有多个组件的内容，则可能需要将内容拆分为多个文件。  多个文件是一种方法。

新建一个文件，并为其提供唯一的命名空间：

```csharp
using System;

namespace NumberFun
{
    // code can go here
} 
```

接下来，将其包含在 `Program.cs` 文件中：

```csharp
using NumberFun;
```

最后，可生成它：

`$ dotnet build`

现在才是有趣的部分：让新文件执行一些操作！

### <a name="example-a-fibonacci-sequence-generator"></a>示例：Fibonacci 序列生成器

假设希望通过缓存一些斐波那契值，基于之前的斐波那契示例进行生成，并添加一些递归特性。  [更好的斐波那契示例](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/FibonacciBetterMsBuild)的代码可能会使用具有以下代码的新 `FibonacciGenerator.cs` 文件。

```csharp
using System;
using System.Collections.Generic;

namespace NumberFun
{
    public class FibonacciGenerator
    {
        private Dictionary<int, int> _cache = new Dictionary<int, int>();
        
        private int Fib(int n) => n < 2 ? n : FibValue(n - 1) + FibValue(n - 2);
        
        private int FibValue(int n)
        {
            if (!_cache.ContainsKey(n))
            {
                _cache.Add(n, Fib(n));
            }
            
            return _cache[n];
        }
        
        public IEnumerable<int> Generate(int n)
        {
            for (int i = 0; i < n; i++)
            {
                yield return FibValue(i);
            }
        }
    }
}
```

现在，只需如下所示调整 `Program.cs` 文件中的 `Main()` 方法。

```csharp
using System;
using NumberFun;

class Program
{
    static void Main(string[] args)
    {
        var generator = new FibonacciGenerator();
        foreach (var digit in generator.Generate(15))
        {
            Console.WriteLine(digit);
        }
    }
}
```

最后，运行它！

```
$ dotnet run
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

就是这么简单！

## <a name="conclusion"></a>结束语
 
希望本指南可帮助你了解如何创建 .NET Core 控制台应用（从基本知识一直到含单元测试的多项目系统）。  下一步就是创建属于自己的出色控制台应用！
 
如果对更高级的控制台应用程序示例感兴趣，请学习下一教程：[使用 .NET Core 命令行组织和测试项目（.NET Core 工具 RC4）](using-with-xplat-cli-msbuild-folders.md)。



<!--HONumber=Feb17_HO2-->


