---
title: "dotnet-build 命令 | Microsoft Docs"
description: "dotnet-build 命令可生成项目及其所有依赖项。"
keywords: "dotnet-build, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e1a2bc4-a919-4a86-8f33-a9b218b1fcb3
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 17c2db54f871795c370a6475c21e36736a6b46c3
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-build"></a>dotnet-build

## <a name="name"></a>名称

`dotnet-build` - 生成项目及其所有依赖项。

## <a name="synopsis"></a>摘要

```
dotnet build [project] [-o|--output] [-f|--framework] [-c|--configuration] [-r|--runtime] [--version-suffix] [--no-incremental] [--no-dependencies] [-v|--verbosity]
dotnet build [--help]
```

## <a name="description"></a>描述
`dotnet build` 命令将项目及其依赖项生成为一组二进制文件。 二进制文件是一种符号文件，用于调试（具有 `*.pdb` 扩展名）和中间语言 (IL) 形式的项目代码（具有 `*.dll` 扩展名）。 此外，将生成一个 JSON 文件，其中列出应用程序的依赖项（扩展名为 `*.deps.json`）。 最后，还将生成 `runtime.config.json` 文件。 此文件指定生成的代码将针对哪个共享运行时和版本运行。 

如果项目有第三方依赖项（如来自 NuGet 的库），将从 NuGet 缓存解析这些依赖项，并且它们不适用于项目的生成的输出。 考虑到这一点，`dotnet build` 的产品还未准备好转移到另一台计算机进行运行。 这与 .NET Framework 的行为相反，后者在构建可执行项目（一个应用程序）时，将生成可在任何已安装 .NET Framework 的计算机上运行的输出。 为了在 .NET Core 中获得相似的体验，必须使用 [dotnet publish](dotnet-publish.md) 命令。 可在 [.NET Core 应用程序部署](../deploying/index.md) 文档中找到更多相关信息。 

生成需要 *assets.json* 文件（列出了应用程序的所有依赖项的文件），这意味着生成项目前需运行 [`dotnet restore`](dotnet-restore.md)。 资产文件的缺少表现为工具无法解析引用程序集，这将导致错误。 

`dotnet build` 使用 MSBuild 来生成项目，因此支持并行生成和增量生成。 请参考 [MSBuild 文档](https://docs.microsoft.com/visualstudio/msbuild/msbuild)，获取更多有关这些主题的信息。 

除其自己的选项外，`dotnet build` 命令也接受 MSBuild 选项，如用来设置属性的 `/p` 或用来定义记录器的 `/l`。 可在 [`dotnet msbuild`](dotnet-msbuild.md) 命令文档中找到更多有关这些选项的信息。 如果想要知道何时 

项目是否可执行由项目文件中的 `<OutputType>` 属性决定。 以下示例显示会生成可执行代码的项目： 


```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

若要生成库，只需省略该属性即可。 输出方面的主要区别是库的 IL DLL 不包含任何入口点且无法执行。 

## <a name="arguments"></a>参数

`project`

要生成的项目文件。
如果未指定项目文件，则 MSBuild 会在当前工作目录中搜索以 `proj` 结尾的文件扩展名并使用该文件。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-o|--output <OUTPUT_DIRECTORY>`

放置生成二进制文件的目录。 指定此选项时还需要定义 `--framework`。

`-f|--framework <FRAMEWORK>`

编译特定框架。 需要在[项目文件](csproj.md)中定义该框架。

`-c|--configuration [Debug|Release]`

定义一个配置，根据该配置进行生成。 如果省略，则默认为 `Debug`。

`-r|--runtime [RUNTIME_IDENTIFIER]`

要生成的目标运行时。 有关可以使用的运行时标识符 (RID) 列表，请参阅 [RID 目录](../rid-catalog.md)。

`--version-suffix [VERSION_SUFFIX]`

定义在项目文件的版本字段中应替换的 `*` 对象。 格式遵循 NuGet 的版本准则。

`--no-incremental`

将生成标记为对增量生成不安全。 这将关闭增量编译并强制完全重新生成项目依赖项关系图。

`--no-dependencies`

忽略项目间引用，并仅生成指定要生成的根项目。

`-v|--verbosity`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、 `n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet build`

使用“发布”配置生成项目及其依赖项：

`dotnet build --configuration Release`

针对特定运行时（本例中为 Ubuntu 16.04）生成项目及其依赖项：

`dotnet build --runtime ubuntu.16.04-x64`
