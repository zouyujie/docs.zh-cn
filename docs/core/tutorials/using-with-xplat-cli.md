---
title: "使用命令行在 Windows/Linux/macOS 上入门 .NET Core"
description: "使用命令行接口 (CLI) 在 Windows、Linux 或 macOS 上入门 .NET Core"
keywords: .NET, .NET Core
author: cartermp
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: be988f09-7349-43b0-97fb-3a703d4587ce
translationtype: Human Translation
ms.sourcegitcommit: 37e14d5cdf1593f6a8b1ecee9d9828647b023548
ms.openlocfilehash: 5493ccb77e62d20d5101728ef8ab1744ea697fb8

---

# <a name="getting-started-with-net-core-on-windowslinuxmacos-using-the-command-line"></a>使用命令行在 Windows/Linux/macOS 上入门 .NET Core

本指南介绍如何使用 .NET Core CLI 工具生成基本的跨平台控制台应用。

如果熟悉 .NET Core CLI 工具集，请阅读 [.NET Core SDK 概述](../sdk.md)。

## <a name="prerequisites"></a>先决条件

开始前，请确保拥有[最新的 .NET Core CLI 工具](https://www.microsoft.com/net/core)。 还需要一个文本编辑器。

## <a name="hello-console-app"></a>Hello，控制台应用！

导航到一个文件夹或使用喜欢的名称新建一个文件夹。 “Hello”是为示例代码选择的名称，可在[此处](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/Hello)找到它。

打开命令提示符，键入下列命令：

```
$ dotnet new
$ dotnet restore
$ dotnet run
```

让我们进行快速演练：

1. `$ dotnet new`

   [`dotnet new`](../tools/dotnet-new.md) 会创建一个最新的 `project.json` 文件，其中包含生成控制台应用所必需的 NuGet 依赖项。  它还将创建 `Program.cs`，这是包含应用程序的入口点的基本文件。
   
   `project.json`：
   ```json
   {
        "version": "1.0.0-*",
        "buildOptions": {
            "emitEntryPoint": true
        },
        "dependencies": {
            "Microsoft.NETCore.App": {
                "type": "platform",
                "version": "1.0.0"
            }
        },   
       "frameworks": {
            "netcoreapp1.0": {
                "imports": "dnxcore50"
            }
        }
   }
   ```
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

2. `$ dotnet restore`

   [`dotnet restore`](../tools/dotnet-restore.md) 调用到 NuGet 以恢复依赖项树。 NuGet 分析 `project.json` 文件、下载文件中所述的依赖项（或从计算机缓存中获取）并编写 `project.lock.json` 文件。  需要 `project.lock.json` 文件才可进行编译和运行。
   
   `project.lock.json` 文件是 NuGet 依赖项和其他描述应用的信息的持久化完整图片集。  此文件由其他工具（如 `dotnet build` 和 `dotnet run`）读取，让它们可以使用正确的 NuGet 依赖项和绑定解决方法集处理源代码。
   
3. `$ dotnet run`

   [`dotnet run`](../tools/dotnet-run.md) 调用 `dotnet build` 来确保已生成要生成的目标，然后调用 `dotnet <assembly.dll>` 运行目标应用程序。
   
```
$ dotnet run
Hello, World!
```

还可以执行 [`dotnet build`](../tools/dotnet-build.md) 来编译代码，无需运行已生成的控制台应用程序。

### <a name="building-a-self-contained-application"></a>生成自包含应用程序

让我们尝试编译自包含应用程序，而不是可移植应用程序。 可阅读更多有关 [.NET Core 中可移植性的类型](../deploying/index.md)的信息，了解不同的应用程序类型及其部署方式。

需要对 `project.json` 文件进行一些更改，指导工具构建自包含应用程序。 可在示例目录中的 [HelloNative](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/HelloNative) 项目中查看这些内容。

第一个更改是从所有依赖项中删除 `"type": "platform"` 元素。 目前为止，此项目唯一的依赖项是 `"Microsoft.NETCore.App"`。 `dependencies` 部分应如下所示：

```json
"dependencies": {
    "Microsoft.NETCore.App": {
        "version": "1.0.0"
    }
},
```

接下来，需要添加 `runtimes` 节点，指定所有目标执行环境。 例如，以下 `runtimes` 节点指示生成系统为 64 位版本的 Windows 10 和 64 位版本的 Mac OS X 版本 10.11 创建可执行文件。
生成系统将生成用于当前环境的本机可执行文件。 如果是在 Windows 计算机上执行以下这些步骤，将生成 Windows 可执行文件。 如果是在 Mac 上执行以下这些步骤，将生成 OS X 可执行文件。

```json 
"runtimes": {
  "win10-x64": {},
  "osx.10.11-x64": {}
}
```

请在 [RID 目录](../rid-catalog.md)中参阅完整的受支持运行时列表。 
 
执行这两个更改后，执行 `dotnet restore`，然后执行 `dotnet build` 以创建本机可执行文件。 然后，可以运行生成的本机可执行文件。 

以下示例显示了用于 Windows 的命令。 此示例显示了生成本机可执行文件的位置，并假定项目目录名为 HelloNative。

```
$ dotnet restore 
$ dotnet build 
$ .\bin\Debug\netcoreapp1.0\win10-x64\HelloNative.exe
Hello World!
```

你可能会注意到，生成本机应用程序的速度较慢，但执行速度却较快。 随着应用程序的发展，此行为会变得更明显。

`project.json` 创建本机生成时，该生成过程会生成其他若干文件。 这些文件在 `bin\Debug\netcoreapp1.0\<platform>` 中中创建，其中 `<platform>` 是所选的 RID。 除项目的 `HelloNative.dll` 外，还有一个加载运行时和启动应用程序的 `HelloNative.exe`。
请注意，所生成的应用程序名称发生了更改，因为项目目录名称已更改。  

你可能会想要打包此应用程序，以在不包括 .NET 运行时的计算机上执行它。
使用 `dotnet publish` 命令执行此操作。 `dotnet publish` 命令会在名为 `publish` 的 `./bin/Debug/netcoreapp1.0/<platform>` 目录下新建一个子目录。 它将可执行文件、所有依赖 DLL 和框架复制到此子目录。 可将该目录打包到其他计算机（或容器）并在那里执行应用程序。 

让我们将其与第一个 Hello World 示例中的 `dotnet publish` 行为进行比较。 该应用程序是可移植应用程序，是 .NET Core 的默认应用程序类型。 可移植应用程序需要在目标计算机上安装 .NET Core。 可移植应用程序可在一台计算机上生成并在任意位置执行。 本机应用程序必须针对每台目标计算机单独进行生成。 `dotnet publish` 创建一个目录，此目录含有应用程序的 DLL 和任何不属于平台安装的依赖 DLL。

### <a name="augmenting-the-program"></a>扩充程序

让我们对此文件进行些微更改。  Fibonacci 数字很有意思，我们来尝试一下（使用本机版本）：

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
$ .\bin\Debug\netcoreapp1.0\win10-x64\Fibonacci.exe
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
using static System.Console;
using NumberFun;
```

最后，可生成它：

`$ dotnet build`

现在才是有趣的部分：让新文件执行一些操作！

### <a name="example-a-fibonacci-sequence-generator"></a>示例：Fibonacci 序列生成器

假设希望通过缓存一些 Fibonacci 值，基于之前的 [Fibonacci 示例](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/Fibonacci)进行生成，并添加一些递归特性。  [较好的 Fibonacci 示例](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/FibonacciBetter)代码如下所示：

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

请注意，使用 `Dictionary<int, int>` 和 `IEnumerable<int>` 意味着合并 `System.Collections` 命名空间。
`Microsoft.NetCore.App` 包是一个包含 .NET Framework 中的许多核心程序集的元包。 将此元包包含在内即表明已将 `System.Collections.dll` 程序集纳入项目中。 可通过运行 `dotnet publish` 并检查已安装包中的文件来对此进行验证。 将在列表中看到 `System.Collections.dll`。 

```json
{ 
  "version": "1.0.0-*", 
  "buildOptions": { 
    "debugType": "portable", 
    "emitEntryPoint": true 
  }, 
  "dependencies": {}, 
  "frameworks": { 
    "netcoreapp1.0": { 
      "dependencies": { 
        "Microsoft.NETCore.App": { 
          "version": "1.0.0" 
        } 
      }, 
      "imports": "dnxcore50" 
    } 
  },
  "runtimes": {
    "win10-x64": {},
    "osx.10.11-x64": {}
  }
}
```

现在，只需如下所示调整 `Program.cs` 文件中的 `Main()` 方法。 该示例假定 `Program.cs` 具有 `using System;` 语句。 如果有 `using static System.Console;` 语句，则从 `Console.WriteLine` 中删除`Console.`。  

```csharp
public static void Main(string[] args)
{
    var generator = new FibonacciGenerator();
    foreach (var digit in generator.Generate(15))
    {
        WriteLine(digit);
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

## <a name="using-folders-to-organize-code"></a>使用文件夹组织代码

假设希望引入一些新类型来执行工作。  为此，可添加更多文件并确保向其提供可包含在 `Program.cs` 文件中的命名空间。

```
/MyProject
|__Program.cs
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__project.json
```

项目规模相对较小时，这非常有用。  但是，如果应用较大，具有许多不同的数据类型并且可能有多层，则你可能会想要进行逻辑组织。  这时就该文件夹发挥作用了。  可按照本指南介绍的 [NewTypes 示例项目](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypes)执行操作，或创建自己的文件和文件夹。

首先，在项目的根下创建一个新的文件夹。  此处选择 `/Model`。

```
/NewTypes
|__/Model
|__Program.cs
|__project.json
```

现在，将一些新类型添加到该文件夹：

```
/NewTypes
|__/Model
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__Program.cs
|__project.json
```

现在，就像它们是同一目录中的文件一样，为其提供相同的命名空间，以便可以将其包含在 `Program.cs` 中。

### <a name="example-pet-types"></a>示例：宠物类型

此示例将创建两个新类型，`Dog` 和 `Cat`，并使它们实现接口 `IPet`。

文件夹结构：

```
/NewTypes
|__/Pets
   |__Dog.cs
   |__Cat.cs
   |__IPet.cs
|__Program.cs
|__project.json
```

`IPet.cs`：
```csharp
using System;

namespace Pets
{
    public interface IPet
    {
        string TalkToOwner();
    }
}
```

`Dog.cs`：
```csharp
using System;

namespace Pets
{
    public class Dog : IPet
    {
        public string TalkToOwner() => "Woof!";
    }
}
```

`Cat.cs`：
```csharp
using System;

namespace Pets
{
    public class Cat : IPet
    {
        public string TalkToOwner() => "Meow!";
    }
}
```

`Program.cs`：
```csharp
using System;
using Pets;
using System.Collections.Generic;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            List<IPet> pets = new List<IPet>
            {
                new Dog(),
                new Cat()  
            };
            
            foreach (var pet in pets)
            {
                Console.WriteLine(pet.TalkToOwner());
            }
        }
    }
}
```

`project.json`：
```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "emitEntryPoint": true
  },
  "dependencies": {
    "Microsoft.NETCore.App": {
      "type": "platform",
      "version": "1.0.0"
    }
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": "dnxcore50"
    }
  }
}
```

如果运行，将出现以下结果：

```
$ dotnet restore
$ dotnet run
Woof!
Meow!
```

现在可以添加新宠物类型（例如 `Bird`），扩展此项目。

## <a name="testing-your-console-app"></a>测试控制台应用

可能需要在某些时候测试项目。  下面是一种执行此操作的好办法：

1. 将现有项目的任何源移动到新的 `src` 文件夹。

   ```
   /Project
   |__/src
   ```

2. 创建 `/test` 目录。

   ```
   /Project
   |__/src
   |__/test
   ```

3. 新建 `global.json` 文件：

   ```
   /Project
   |__/src
   |__/test
   |__global.json
   ```

   `global.json`：
   ```json
   {
      "projects": [
         "src", "test"
      ]
   }
   ```

   此文件会告知生成系统这是多项目系统，这允许它查看的依赖项远不止当前刚好在其中执行的文件夹中那么多。  这很重要，因为它允许在测试项目中测试下的代码上放置依赖项。
   
### <a name="example-extending-the-newtypes-project"></a>示例：扩展 NewTypes 项目

现在项目系统已就绪，可创建测试项目并开始编写测试！  从现在开始，本指南将使用并扩展[示例 Types 项目](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypes)。  此外，还将使用 [Xunit](https://xunit.github.io/) 测试框架。  可按照指南操作或创建自己的、含测试的多项目系统。


整个项目结构应如下所示：

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__project.json
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__project.json
|__global.json
```

请确保测试项目中具有以下两项新内容：

1. 含以下项的正确 `project.json`：

   * 对 `xunit` 的引用
   * 对 `dotnet-test-xunit` 的引用
   * 引用对应于测试下的代码的命名空间

2. Xunit 测试类。

`NewTypesTests/project.json`：
```json
{
  "version": "1.0.0-*",
  "testRunner": "xunit",

  "dependencies": {
    "Microsoft.NETCore.App": {
      "type":"platform",
      "version": "1.0.0"
    },
    "xunit":"2.2.0-beta2-build3300",
    "dotnet-test-xunit": "2.2.0-preview2-build1029",
    "NewTypes": "1.0.0"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "portable-net45+win8" 
      ]
    }
  }
}
```

`PetTests.cs`： 
```csharp
using System;
using Xunit;
using Pets;
public class PetTests
{
    [Fact]
    public void DogTalkToOwnerTest()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();
        
        Assert.Equal(expected, actual);
    }
    
    [Fact]
    public void CatTalkToOwnerTest()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();
        
        Assert.Equal(expected, actual);
    }
}
```
   
现在可以运行测试！  [`dotnet test`](../tools/dotnet-test.md) 命令运行在项目中指定的测试运行程序。 确保从顶级目录开始。
 
```
$ dotnet restore
$ cd test/NewTypesTests
$ dotnet test
```
 
输出应如下所示：
 
```
xUnit.net .NET CLI test runner (64-bit win10-x64)
  Discovering: NewTypesTests
  Discovered:  NewTypesTests
  Starting:    NewTypesTests
  Finished:    NewTypesTests
=== TEST EXECUTION SUMMARY ===
   NewTypesTests  Total: 2, Errors: 0, Failed: 0, Skipped: 0, Time: 0.144s
SUMMARY: Total: 1 targets, Passed: 1, Failed: 0.
```
 
## <a name="conclusion"></a>结束语
 
希望本指南可帮助你了解如何创建 .NET Core 控制台应用（从基本知识一直到含单元测试的多项目系统）。  下一步就是创建属于自己的出色控制台应用！
 
如果对控制台应用的更高级示例感兴趣，请查看下一个教程：[使用 CLI 工具编写控制台应用：高级分步指南](cli-console-app-tutorial-advanced.md)。



<!--HONumber=Nov16_HO3-->


