---
title: ".NET Core CLI 扩展性模型 | Microsoft Docs"
description: ".NET Core CLI 扩展性模型"
keywords: "CLI, 扩展性, 自定义命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 1bebd25a-120f-48d3-8c25-c89965afcbcd
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 0a136e69e103994a69084b09f481489880d5df42

---

# <a name="net-core-cli-extensibility-model"></a>.NET Core CLI 扩展性模型 

> [!WARNING]
> 本主题适用于 .NET Core 工具预览版 2。 对于 .NET Core 工具 RC4 版本，请参阅 [.NET Core CLI 扩展性模型（.NET Core 工具 RC4）](../preview3/tools/extensibility.md)主题。

## <a name="overview"></a>概述
本文将介绍如何扩展 CLI 工具的主要方式，并解释驱动每个工具的方案。 本文档将概述如何使用这些工具并简短说明如何生成两种工具。 

## <a name="how-to-extend-cli-tools"></a>如何扩展 CLI 工具
可以通过以下两种主要方式扩展 CLI 工具：

1. 通过基于每个项目的 NuGet 包
2. 通过系统路径

上方列出的两种扩展性机制并不相互排斥；可以同时使用或单独使用。 选择何种机制很大程度上取决于希望通过扩展实现的目标。

## <a name="per-project-based-extensibility"></a>基于每个项目的扩展性
基于项目的工具是作为 NuGet 包分布的[可移植控制台应用程序](../deploying/index.md)。 工具仅在项目的上下文中可用，这些工具被该项目引用或为该项目还原；项目上下文外（例如，包含该项目的目录外）的调用将因无法找到命令而失败。

此外，这些工具非常适合生成服务器，因为 `project.json` 外不需要任何条件。 生成过程会对所生成的项目运行还原操作，并且工具可用。 语言项目（如 F#）也属于此类别；毕竟只能采用某种特定语言编写每个项目。 

最后，此扩展性模型支持创建需要访问项目生成输出的工具。 例如，[ASP.NET](https://www.asp.net/) MVC 应用程序中的多种 Razor 视图工具均属于此类别。 

### <a name="consuming-per-project-tools"></a>使用基于项目的工具
使用这些工具需要将 `tools` 节点添加到 `project.json`。 在 `tools` 节点内，引用该工具所在的包。 运行 `dotnet restore` 后，将还原该工具及其依赖项。 

对于需要加载用于执行的项目生成输出的工具，通常还有一个依赖项，它位于项目文件中的常规依赖项下。 这意味着加载项目代码的工具有两个组件： 

1. “工具”主要调用程序
2. 包含要使用的逻辑的任何数目的其他工具 

为什么需要两个组件？ 需要加载项目生成输出的工具需具备所处理项目的统一依赖项关系图。 通过添加依赖项位，可以使 NuGet 能够将这些依赖项解析为统一关系图。 调用程序存在的原因在于它需要推断出依赖项工具的位置及框架。 调用程序可以接受用户指定和查找依赖项工具所用的所有重定向参数（`-c`、`-o`、`-b`）；还可以在多个框架中存在多个依赖项工具情况下实现各种策略（即运行所有工具或仅一个工具等）通常，可采用所需的任何方式在这两种工具之间共享逻辑。 

我们来看看将简单的工具专用工具添加到简单项目的示例。 假定示例命令称为 `dotnet-api-search`，它可使你搜索指定 API 的所有 NuGet 包，以下是使用该工具的控制台应用程序 `project.json` 文件：

```json
{
    "version": "1.0.0",
    "compilationOptions": {
        "emitEntryPoint": true
    },
    "dependencies": {
        "Microsoft.NETCore.App": {
            "type": "platform",
            "version": "1.0.0"
        }
    },
    "tools": {
        "dotnet-api-search": {
            "version": "1.0.0",
            "imports": ["dnxcore50"]
        }
    },
    "frameworks": {
        "netcoreapp1.0": {}
    }
}
```

`tools` 节点采用与 `dependencies` 节点相同的方式进行结构化。 它需要至少包含该工具及其版本的包的包 ID。 在上述示例中，我们可以看到另一语句，即 `imports`。 这会影响该工具的还原过程，并指定除工具本身所含任何目标框架外，它还与 `dnxcore50` 目标兼容。 有关详细信息，可以参阅 [project.json 引用](project-json.md)。

### <a name="building-tools"></a>生成工具
如前所述，工具仅仅是可移植控制台应用程序。 可以采用与生成控制台应用程序类似的方式生成此工具。 生成后，使用 [`dotnet pack`](dotnet-pack.md) 命令创建 NuGet 包 (nupkg)，其中包含代码和依赖项等相关信息。 作者可以随意命名包，但内部应用程序（即实际的工具二进制文件）必须遵循 `dotnet-<command>` 的约定以便 `dotnet` 能够调用它。 

由于工具是可移植应用程序，使用该工具的用户必须拥有生成该工具时所针对的 .NET Core 库版本，以便运行此工具。 工具使用的以及 .NET Core 库未包含的其他任何依赖项均被还原并放置在 NuGet 缓存中。 因此，使用 .NET Core 库和 NuGet 缓存中的程序集可以运行整个工具。 

这些类型的工具含有依赖项关系图，它完全独立于使用这些工具的项目的依赖项关系图。 还原过程将首先还原项目依赖项，然后还原每个工具及其依赖项。 

可在 [.NET Core CLI 存储库](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestProjects)中找到有关此过程的更多示例和不同组合。 还可以在相同存储库中查看[所用工具的实现](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages)。 

加载用于执行的项目生成输出的生成工具略有不同。 如上所述，这些类型的工具有两个组件：

1. 一个是用户调用的调度程序工具
2. 另一个是特定于框架的依赖项，其中包含有关如何找到并处理生成输出的逻辑

这方面的典型示例是[实体框架 (EF)](https://github.com/aspnet/EntityFramework) 命令以及 [`dotnet test`](dotnet-test.md) 命令。 无论哪种情况都有一个在 `project.json` 的 `tools` 节点中引用的工具，即主调度程序。 用户可在命令行调用此工具。 拼图的第二块是项目主依赖项（根依赖项或特定于框架的依赖项）中提供的依赖项。 此包含有工具的实际逻辑。 包属于普通依赖项，因此会将其作为项目还原过程的一部分进行还原。 

不同于前面几种工具，这些工具实际上属于使用它们的项目的关系图。 这是因为它们需要访问项目代码并且可能访问所有依赖项。 例如，EF 工具需要此项的原因在于它们需要扫描程序集以查找所需代码，如迁移。  

存在此双管齐下的解决方案的另一个原因是可实现更简洁的调用模型。 将某些项目放置在磁盘上的大多数 CLI 命令（例如，`dotnet build`、`dotnet publish`）都允许用户使用 `--output` 参数、`--build-base-path` 参数或 `--configuration` 参数将输出重定向到不同路径。 例如，若要使 EF 工具能够找到项目的生成输出，必须同时向 `dotnet` 驱动程序以及 `ef` 命令提供具有相同值的相同参数。 使用调用模型，用户可以将任何参数传递到调度程序工具，此工具可以在之后使用该模型查找所需的包含输出目录中的逻辑的二进制文件。 

可在 [.NET Core CLI 存储库](https://github.com/dotnet/cli)中找到此方法的良好示例：

* [示例 project.json 文件](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/TestAssets/DesktopTestProjects/AppWithDirectDependencyDesktopAndPortable/project.json)
* [调度程序的实现](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages/dotnet-dependency-tool-invoker)
* [特定于框架的依赖项的实现](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages/dotnet-desktop-and-portable)


### <a name="path-based-extensibility"></a>基于路径的扩展
基于路径的扩展常用于开发计算机，此计算机需要在概念上涵盖多个项目的工具。 此扩展机制的主要缺点在于必须将其关联到工具所在的计算机。 如果其他计算机上需要该机制，则必须对其进行部署。

此 CLI 工具集扩展的模式就非常简单。 正如 [.NET Core CLI 概述](index.md)中所述，`dotnet` 驱动程序可以运行以 `dotnet-<command>` 约定命名的任何命令。 默认的解析逻辑将首先探测多个位置，最后探测系统路径。 如果请求的命令存在于系统路径中并且属于可调用的二进制文件，则 `dotnet` 驱动程序将调用它。 

该二进制文件几乎可以是操作系统可以执行的任何内容。 在 Unix 系统上，这表示通过 `chmod +x` 设置了执行位的任何内容。 在 Windows 上，这表示 Windows 知道如何运行的任何内容。 

例如，我们来看看非常简单的 `dotnet clean` 命令的实现。 我们将使用 `bash` 来实现此命令。 该命令仅删除当前目录中的 `bin/` 和 `obj/`。 如果将 `--lock` 参数传递给它，也会删除 `project.lock.json` 文件。 下方给出了整个命令。 

```bash
#!/bin/bash

# Delete the bin and obj dirs
rm -rf bin/ obj/

LOCK_FILE=$1
if [[ "$LOCK_FILE" = "--lock" ]]; then
    rm project.lock.json
fi


echo "Cleaning complete..."
```

在 macOS 上，可以将此脚本另存为 `dotnet-clean` 并使用 `chmod +x dotnet-clean` 设置其可执行位。 然后，可以使用命令 `ln -s dotnet-clean /usr/local/bin/` 在 `/usr/local/bin` 中创建其符号链接。 这样，就可以使用 `dotnet clean` 语法调用 clean 命令。 可以通过创建应用、在其中运行 `dotnet build`，然后运行 `dotnet clean` 来对此进行测试。 

## <a name="conclusion"></a>结束语
.NET Core CLI 工具允许两个主要扩展点。 基于项目的工具包含在项目上下文中，但允许通过还原轻松安装。 基于路径的工具非常适合可在一台计算机上使用的常规、跨项目工具。 



<!--HONumber=Feb17_HO2-->


