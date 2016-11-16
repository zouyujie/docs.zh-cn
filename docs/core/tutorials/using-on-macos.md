---
title: "在 macOS 上入门 .NET Core"
description: "使用 Visual Studio Code 在 macOS 上入门 .NET Core"
keywords: .NET, .NET Core
author: bleroy
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8ad82148-dac8-4b31-9128-b0e9610f4d9b
translationtype: Human Translation
ms.sourcegitcommit: 2339be6aef7e2ff942f1f1999a12f48ee4a77ee8
ms.openlocfilehash: 12b7bed380db53aad04f0615c6efa6152b3035b7

---

# <a name="getting-started-with-net-core-on-macos-using-visual-studio-code"></a>使用 Visual Studio Code 在 macOS 上入门 .NET Core

作者：[Bertrand Le Roy](https://github.com/bleroy)、[Phillip Carter](https://github.com/cartermp)、[Bill Wagner](https://github.com/billwagner)

供稿人： [Toni Solarin-Sodara](https://github.com/tsolarin)

本文档提供使用 [Visual Studio Code](http://code.visualstudio.com) 创建 .NET Core 解决方案的步骤和工作流概述。
将了解到如何通过 [NuGet](http://nuget.org) 创建项目、创建单元测试、使用调试工具和合并第三方库。

本文在 Mac OS 上使用 Visual Studio Code。 不同之处在于，本文指出了与 Windows 平台的区别。

## <a name="prerequisites"></a>先决条件

在开始之前，需要安装当前以预览版提供的 [.NET Core SDK](https://www.microsoft.com/net/core)。 .NET Core SDK 包括最新版本的 .NET Core 框架和运行时。

还需要安装 [Visual Studio Code](http://code.visualstudio.com)。
在本文进行的过程中，也会安装改进 .NET Core 开发体验的扩展。

可在 [.NET 主页](http://dot.net)找到所有这些内容的链接。

## <a name="getting-started"></a>入门

[GitHub](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/golden) 上提供此教程的源。

启动 Visual Studio Code。 按 Ctrl+“\`”（反引号字符），打开 VS Code 中嵌入的终端。 （或者，如果需要，可以使用单独的终端窗口）。

完成后，将创建三个项目：库项目、对该库项目的测试和使用该库的控制台应用程序。 对于这三个项目，遵循标准文件夹结构。 遵循此标准文件夹结构意味着 .NET Core SDK 工具了解生产代码项目和测试代码项目之间的关系。 这可提高开发体验的工作效率。

首先，创建这些文件夹。 在终端中，创建“golden”目录。 在该目录下创建 `src` 和 `test` 目录。 在 `src` 下创建 `app` 和 `library` 目录。 在 `test` 中创建 `test-library` 目录。 可使用 VS Code 中的终端或通过单击 VS Code 中的父文件夹并选择“新建文件夹”图标，来执行此操作。

在 VS Code 中，打开“golden”目录。 此目录是解决方案的根目录。

接下来，在根目录中为解决方案创建 `global.json` 文件。
`global.json` 的内容是：

```json
{
    "projects": [
        "src",
        "test"
    ]
}
```

此时，目录树应如下所示：


```
/golden
|__global.json
|__/src
   |__/app
   |__/library
|__/test
   |__/test-library
```

### <a name="writing-the-library"></a>编写库

下一个任务是创建库。 在终端窗口（VS Code 中嵌入的终端或其他终端）中，使用 cd 命令定位到 `golden/src/library` 并键入命令 `dotnet new -t lib`。
这将创建库项目，包含两个文件：`project.json` 和 `Library.cs`。

`project.json` 包含下列信息：

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable"
  },
  "dependencies": {},
  "frameworks": {
    "netstandard1.6": {
      "dependencies": {
        "NETStandard.Library": "1.6.0"
      }
    }
  }
}
```


此库项目将使用对象的 JSON 表示形式，因此需要添加对 `Newtonsoft.Json` NuGet 包的引用。 在 `project.json` 中，添加包的最新预发布版本作为依赖项：

```json
"dependencies": {
    "Newtonsoft.Json": "9.0.1-beta1"
},
```

添加这些依赖项后，需要将这些包安装到工作区。 运行 `dotnet restore` 命令以更新所有依赖项，并在项目目录中编写 `project.lock.json` 文件。 此文件包含项目中所有依赖项的完整依赖关系树。 无需读取此文件，它由 .NET Core SDK 中的工具使用。

现在，让我们更新 C# 代码。 让我们创建包含一个公共方法的 `Thing` 类。 此方法将返回两个数字之和，但会通过将数字转换为 JSON 字符串，再将其反序列化来执行此操作。 将文件 `Library.cs` 重命名为 `Thing.cs`。 然后，使用以下代码替换现有代码（对于模板生成的 Class1）：

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

现在， `golden/src/library/bin/Debug/netstandard1.6` 下有了一个生成的 `library.dll` 文件。

### <a name="writing-the-test-project"></a>编写测试项目

让我们为已生成的库生成测试项目。 使用 Cd 命令定位到 `test/test-library` 目录。 运行 `dotnet new -t xunittest` 创建新测试项目。 

将需要为上述步骤中编写的库添加依赖项节点。 打开 `project.json` 并将依赖项部分更新为以下代码（包括以下最后一个 `library` 节点）：

```json
"dependencies": {
  "System.Runtime.Serialization.Primitives": "4.1.1",
  "xunit": "2.1.0",
  "dotnet-test-xunit": "1.0.0-rc2-192208-24",
  "library": {
    "target": "project"
  }
}
```

`library` 节点指定此依赖项应解析到当前工作区中的项目。 在未对此显式指定的情况下，测试项目可能会针对相同名称的 NuGet 包进行生成。

现已正确配置依赖项，可以开始创建库的测试。 打开 `Tests.cs`，用以下代码替代其内容：

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

现在，运行 `dotnet restore`、`dotnet build` 和 `dotnet test`。
xUnit 控制台测试运行程序将运行一个测试并报告其正在传递。 

### <a name="writing-the-console-app"></a>编写控制台应用

在终端中，使用 cd 命令定位到 `golden/src/app` 目录。 运行 `dotnet new` 新建控制台应用程序。

控制台应用程序取决于在前面的步骤中生成和测试的库。 需要编辑 `project.json` 添加此依赖项来进行指示。  在 `dependencies` 节点中，添加 `library` 节点，如下所示：

```json
"dependencies": {
  "library": {
    "target": "project"
  }
}
```

`project` 节点在此处很重要，因为它处于测试库中。 它指示这是当前解决方案中的项目，而不是 NuGet 包。

运行 `dotnet restore` 恢复所有依赖项。 打开 `program.cs` 并使用此行替换 `Main` 方法中的内容：

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

需要将两条 `using` 指令添加到文件顶部：

```csharp
using static System.Console;
using Library;
```

然后，运行 `dotnet build`。 这将创建程序集，可键入 `dotnet run` 运行可执行文件。

### <a name="debugging-your-application"></a>调试应用程序

可使用 C# 扩展在 VS Code 中调试代码。
通过按 `F1` 打开 VS Code 面板来安装此扩展。 键入 `ext install` 查看扩展列表。 选择 C# 扩展。 （[Visual Studio Code C# 扩展文档](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md) 页面提供详细信息。）

安装扩展后，VS Code 将请求重启应用程序以加载新扩展。 安装扩展后，可打开调试器选项卡（见图）。

![VS Code 调试器](./media/using-on-macos/vscodedebugger.png)


启动调试器时，VS Code 将指导你配置调试器。 执行此操作时，将创建 `.vscode` 目录，包含两个文件：`tasks.json` 和 `launch.json`。 这两个文件可控制调试器配置。 在大多数项目中，此目录不包含在源控件中。
它包含在与此演练关联的示例中，所以可查看需要进行的编辑。

解决方案包含多个项目，因此需要修改每个文件以执行正确命令。 首先，打开 `tasks.json`。 默认生成任务在工作区源目录中运行 `dotnet build`。 但需要在 `src/app` 目录中运行它。 因此需要添加 `options` 节点，将当前工作目录设置为上述目录：

```json
"options": {
    "cwd": "${workspaceRoot}/src/app"
}
```

接下来，需要打开 `launch.json` 并更新程序路径。 将在描述程序的“配置”下看到一个节点。 将看到：

```json
"program": "${workspaceRoot}/bin/Debug/<target-framework>/<project-name.dll>",
```

将它更改为：

```json
"program": "${workspaceRoot}/src/app/bin/Debug/netcoreapp1.0/app.dll",
```

如果在 Windows 上运行，需要更新应用程序的 `project.json`（位于 `src/app` 目录中），以生成可移植 PDB 文件（在 Mac OSX 和 Linux 上，默认发生此情况）。
在 `buildOptions` 内添加 `debugType` 节点。 需要在 `project.json` 中，为 `src/app` 和 `src/library` 文件夹添加 `debugType` 节点。

```json
  "buildOptions": {
    "debugType": "portable"
  },
```

在 `Main` 中的 `WriteLine` 语句处设置一个断点。 通过按 `F9` 键或在需要断点的行的左边距中单击鼠标，来执行此操作。 通过按 VS Code 屏幕左侧的“调试”图标打开调试器（见图）。 然后，按“开始”按钮，在调试器下启动应用程序。

应命中断点。 单步执行 `Get` 方法，确保已传入正确的参数。 确保答案的确为 42。



<!--HONumber=Nov16_HO1-->


