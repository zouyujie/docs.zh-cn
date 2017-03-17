---
title: "dotnet-run 命令 | Microsoft Docs"
description: "dotnet-run 命令为从源代码运行应用程序提供了一个方便的选项。"
keywords: "dotnet-run, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 40d4e60f-9900-4a48-b03c-0bae06792d91
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 60bb9160e43788539b0dc6bcf1372bb925e9ba22
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-run"></a>dotnet-run

## <a name="name"></a>名称 

`dotnet-run` - 无需任何显式编译或启动命令即可“就地”运行源代码。

## <a name="synopsis"></a>摘要

```
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

## <a name="description"></a>描述

`dotnet run` 命令为从源代码使用一个命令运行应用程序提供了一个方便的选项。 这对命令行中进行快速迭代开发会有用。 该命令依赖 [`dotnet build`](dotnet-build.md) 命令来生成代码，因此任何生成要求（如必须首先还原项目）也适用于 `dotnet run`。 

输出文件会写出到默认位置，即 `bin/<configuration>/<target>`。 例如，如果具有 `netcoreapp1.0` 应用程序并且运行 `dotnet run`，输出将置于 `bin/Debug/netcoreapp1.0`。 将根据需要覆盖文件。 临时文件将置于 `obj` 目录。 

对于具有多个指定框架的项目，`dotnet run` 将显示错误，除非使用 `--framework` 选项指定要针对哪个框架运行应用程序。

必须在项目上下文，而不是生成程序集中使用 `dotnet run` 命令。 如果尝试改为运行可移植应用程序 DLL，应使用 [dotnet](dotnet.md)，切勿使用如下所示的任何命令：
 
`dotnet myapp.dll`

有关 `dotnet` 驱动程序的详细信息，请参阅 [.NET Core 命令行工具 (CLI)](index.md) 主题。

若要运行应用程序，`dotnet run` 命令需从 NuGet 缓存解析共享运行时之外的应用程序依赖项。 鉴于此，不建议使用此命令在生产中运行应用程序。 而应使用 [`dotnet publish`](dotnet-publish.md) 命令[创建部署](../deploying/index.md)，并在生产中使用该命令。 

## <a name="options"></a>选项

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此参数后的所有参数均会被传递给正在运行的应用程序。 

`-h|--help`

打印出有关命令的简短帮助。

`-c|--configuration {Debug|Release}`

用于生成项目的配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK_IDENTIFIER>`

使用指定框架生成并运行应用。 框架必须在项目文件中进行指定。

`-p|--project <PATH>`

指定要运行的项目文件的路径。 它可能是 [csproj](csproj.md) 文件的路径或包含 [csproj](csproj.md) 文件的目录路径。 如未指定，则默认为当前目录。 

## <a name="examples"></a>示例

运行当前目录中的项目：

`dotnet run` 

运行指定的项目：

`dotnet run --project /projects/proj1/proj1.csproj`

运行当前目录中的项目（在本例中，`--help` 参数被传递到正在运行的应用程序，因为使用了 `--` 参数）：

`dotnet run --configuration Release -- --help`
