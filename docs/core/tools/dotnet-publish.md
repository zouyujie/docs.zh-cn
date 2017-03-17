---
title: "dotnet-publish 命令 | Microsoft Docs"
description: "dotnet-publish 命令可将 .NET Core 项目发布到目录。"
keywords: "dotnet-publish, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 78487673d8fa07286605fb806f30083747b17386
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-publish"></a>dotnet-publish

## <a name="name"></a>名称

`dotnet-publish` - 将应用程序及其所有依赖项打包到文件夹，准备进行发布。

## <a name="synopsis"></a>摘要

```
dotnet publish [project] [-f|--framework] [-r|--runtime] [-o|--output] [-c|--configuration] [--version-suffix] [-v|--verbosity]
dotnet publish [-h|--help]
```

## <a name="description"></a>描述

`dotnet publish` 编译应用程序、读取 project 文件中指定的所有依赖项并将生成的文件集发布到目录。 输出将包含以下信息：

1. 扩展名为 `*.dll` 的程序集中的中间语言 (IL) 代码。
2. *deps.json* 文件，包含项目的所有依赖项。 
3. *Runtime.config.json* 文件，指定应用程序所要求的共享运行时以及该运行时的其他配置选项（例如，垃圾回收类型）。
4. 所有应用程序的依赖项。 将这些依赖项从 NuGet 缓存复制到输出文件夹。 

已准备好在远程计算机中部署 `dotnet publish` 命令的输出以用于执行，并且这是唯一正式支持的、用于准备应用程序以将其部署到另一台计算机（例如，服务器）进行执行的方式。 根据项目指定的部署类型，远程计算机上必须安装 .NET Core 共享运行时。 有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)主题。

## <a name="arguments"></a>参数

`project` 

要发布的项目，如果未指定 `project`，默认为当前目录。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-f|--framework <FRAMEWORK>`

发布用于指定的目标框架的应用程序。 目标框架必须在项目文件中进行指定。

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 这将在创建[独立部署](../deploying/index.md#self-contained-deployments-scd)时使用。 有关可以使用的运行时标识符 (RID) 列表，请参阅 [RID 目录](../rid-catalog.md)。 默认为发布[依赖于框架的应用](../deploying/index.md#framework-dependent-deployments-fdd)。

`-o|--output <OUTPUT_PATH>`

指定放置目录的路径。 如未指定，对于可移植应用程序，将默认为 *_./bin/[configuration]/[framework]/_* 或对于独立部署，将默认为 *_./bin/[configuration]/[framework]/[runtime]_*。

`-c|--configuration {Debug|Release}`

生成项目时要使用的配置。 默认值为 `Debug`。

`--version-suffix <VERSION_SUFFIX>`

定义在项目文件的版本字段中应替换的 `*` 对象。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、 `n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

发布当前目录中的项目：

`dotnet publish`

使用指定的项目文件发布应用程序：

`dotnet publish ~/projects/app1/app1.csproj`
    
使用 `netcoreapp1.1` 框架发布当前目录中的项目：

`dotnet publish --framework netcoreapp1.1`
    
使用 `netcoreapp1.1` 框架和 `OS X 10.10` 的运行时发布当前应用程序（此 RID 必须存在于项目文件中）。

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

## <a name="see-also"></a>另请参阅
* [框架](../../standard/frameworks.md)
* [运行时标识符 (RID) 目录](../rid-catalog.md)
