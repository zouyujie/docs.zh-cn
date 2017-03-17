---
title: "在 macOS 上入门 .NET Core"
description: "使用 Visual Studio Code 在 macOS 上入门 .NET Core"
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 02/08/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 8ad82148-dac8-4b31-9128-b0e9610f4d9b
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: c4d1b7690ca87f2a1a9ced4d82e47aee2f7ecc9f
ms.lasthandoff: 03/07/2017

---

# <a name="getting-started-with-net-core-on-macos-using-visual-studio-code"></a>使用 Visual Studio Code 在 macOS 上入门 .NET Core

本文档提供使用 [Visual Studio Code](http://code.visualstudio.com) 创建 .NET Core 解决方案的步骤和工作流概述。
将了解到如何通过 [NuGet](http://nuget.org) 创建项目、创建单元测试、使用调试工具和合并第三方库。

本文在 Mac OS 上使用 Visual Studio Code。 不同之处在于，本文指出了与 Windows 平台的区别。

## <a name="prerequisites"></a>先决条件

在开始之前，需要安装 [.NET Core SDK](https://www.microsoft.com/net/core)。 .NET Core SDK 包括最新版本的 .NET Core 框架和运行时。

还需要安装 [Visual Studio Code](http://code.visualstudio.com)。
在本文进行的过程中，也会安装改进 .NET Core 开发体验的扩展。

## <a name="getting-started"></a>入门

[GitHub](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/golden) 上提供此教程的源。

启动 Visual Studio Code。 按 Ctrl+“\`”（反引号字符），打开 VS Code 中嵌入的终端。 （或者，如果需要，可以使用单独的终端窗口）。

完成后，将创建三个项目：库项目、对该库项目的测试和使用该库的控制台应用程序。 

首先，创建这些文件夹。 在终端中，创建“golden”目录。 在 VS Code 中，打开 *golden* 目录。 此目录是解决方案的根目录。 运行 [`dotnet new`](../tools/dotnet-new.md) 命令，以创建新的解决方案：

```
dotnet new sln
```

此命令创建用于整个解决方案的 *golden.sln* 文件。

下一个任务是创建库。 在终端窗口（VS Code 中嵌入的终端或其他终端）中，使用 cd 命令定位到 *golden/* 并键入命令：

```
dotnet new classlib -o library
```

这会创建一个库项目，且在 *library* 目录中包含两个文件：*library.csproj* 和 *Class1.cs*。 需将该库项目包含在解决方案中。 运行 [`dotnet sln`](../tools/dotnet-sln.md) 命令，将新创建的 *library.csproj* 添加到解决方案：

```
dotnet sln add library/library.csproj
```

现在来检查一下创建的项目。 *library.csproj* 文件包含以下信息：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard1.4</TargetFramework>
  </PropertyGroup>

</Project>
```

此库项目将使用对象的 JSON 表示形式，因此需要添加对 `Newtonsoft.Json` NuGet 包的引用。 `dotnet add` 命令向项目添加新项。 若要向 NuGet 包添加引用，可使用 `package` 命令并指定包的名称。 

```
dotnet add library package Newtonsoft.Json
```

这会将 `Newtonsoft.Json` 及其依赖项添加到库项目。 或可以手动编辑 *library.csproj* 文件，并添加以下节点：

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json">
    <Version>9.0.1</Version>
  </PackageReference>
</ItemGroup>
```

添加这些依赖项后，需要将这些包安装到工作区。 运行 `dotnet restore` 命令以更新所有依赖项，并在项目目录下编写 *obj/project.assets.json* 文件。 此文件包含项目中所有依赖项的完整依赖关系树。 无需读取此文件，它由 .NET Core SDK 中的工具使用。

现在，让我们更新 C# 代码。 让我们创建包含一个公共方法的 `Thing` 类。 此方法将返回两个数字之和，但会通过将数字转换为 JSON 字符串，再将其反序列化来执行此操作。 将文件 *Class1.cs* 重命名为 *Thing.cs*。 然后，使用以下代码替换现有代码（对于模板生成的 Class1）：

```csharp
using static Newtonsoft.Json.JsonConvert;

namespace Library
{
    public class Thing
    {
        public int Get(int left, int right) =>
            DeserializeObject<int>($"{left + right}");
    }
}
```

这将使用大量现代 C# 功能，例如静态 using、表达式体成员和内插字符串。可在[了解 C#](../../csharp/index.md) 部分了解相关信息。

现已更新代码，可以使用 `dotnet build` 生成库。

现在，*golden/library/bin/Debug/netstandard1.4* 下有一个生成的 *library.dll* 文件。

### <a name="writing-the-test-project"></a>编写测试项目

让我们为已生成的库生成测试项目。 更改为 *golden* 目录。 运行 `dotnet new xunit -o test-library` 创建新测试项目。 需要通过运行 `dotnet sln add test-library/test-library.csproj`，将此项目添加到解决方案。

将需要为上述步骤中编写的库添加依赖项节点。 `dotnet add reference` 命令执行该操作：

```
dotnet add test-library/test-library.csproj reference library/library.csproj
```

或可以手动编辑 *test-library.csproj* 文件，并添加以下节点：

```xml
<ItemGroup>
  <ProjectReference Include="..\library\library.csproj" />
</ItemGroup>
```

`library` 节点指定此依赖项应解析到当前工作区中的项目。 在未对此显式指定的情况下，测试项目可能会针对相同名称的 NuGet 包进行生成。

现已正确配置依赖项，可以开始创建库的测试。 打开 *UnitTest1.cs*，用以下代码替代其内容：

```csharp
using Library;
using Xunit;

namespace TestApp
{
    public class LibraryTests
    {
        [Fact]
        public void TestThing() {
            Assert.Equal(42, new Thing().Get(19, 23));
        }
    }
}
```

现在，运行 `dotnet restore` 和 `dotnet build`。 这些命令将以递归方式查找所有项目，以还原依赖项并生成它们。
最后，运行 `dotnet test test-library/test-library.csproj` 以运行测试。
xUnit 控制台测试运行程序将运行一个测试并报告其正在传递。 

### <a name="writing-the-console-app"></a>编写控制台应用

在终端中运行 `dotnet new console -o app` 新建控制台应用程序。 此项目也是解决方案的一部分，因此运行 `dotnet sln add app/app.csproj` 将项目添加到解决方案。

控制台应用程序取决于在前面的步骤中生成和测试的库。 需要通过再次运行 `dotnet add reference` 进行指示：

```
dotnet add app/app.csproj reference library/library.csproj
```

运行 `dotnet restore` 恢复所有依赖项。 打开 *program.cs* 并使用此行替换 `Main` 方法中的内容：

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

需要将两条 `using` 指令添加到文件顶部：

```csharp
using static System.Console;
using Library;
```

然后，运行 `dotnet build`。 这将创建程序集，可键入 `dotnet run -p app/app.csproj` 运行可执行文件。
`dotnet run` 的 `-p` 参数为主应用程序指定项目。

### <a name="debugging-your-application"></a>调试应用程序

可使用 C# 扩展在 VS Code 中调试代码。
通过按 `F1` 打开 VS Code 面板来安装此扩展。 键入 `ext install` 查看扩展列表。 选择 C# 扩展。 （[Visual Studio Code C# 扩展文档](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md) 页面提供详细信息。）

安装扩展后，VS Code 将请求重启应用程序以加载新扩展。 安装扩展后，可打开调试器选项卡（见图）。

![VS Code 调试器](./media/using-on-macos/vscodedebugger.png)

在 `Main` 中的 `WriteLine` 语句处设置一个断点。 通过按 `F9` 键或在需要断点的行的左边距中单击鼠标，来执行此操作。 通过按 VS Code 屏幕左侧的“调试”图标打开调试器（见图）。 然后，按“开始”按钮，在调试器下启动应用程序。

应命中断点。 单步执行 `Get` 方法，确保已传入正确的参数。 确保答案的确为 42。

