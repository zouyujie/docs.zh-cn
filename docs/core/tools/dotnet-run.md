---
title: "dotnet-run 命令 | .NET Core SDK"
description: "dotnet-run 命令为从源代码运行应用程序提供了一个方便的选项。"
keywords: "dotnet-run, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 495ff50b-cb30-4d30-8f20-beb3d5e7c31f
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: 18731d9fcc190371d908779a69a81114e0685aba

---

#<a name="dotnetrun"></a>dotnet-run

## <a name="name"></a>名称 

dotnet-run - 无需任何显式编译或启动命令即可“就地”运行源代码

## <a name="synopsis"></a>摘要

`dotnet run [--help] [--framework] [--configuration]
    [--project] [[--] [application arguments]]`

## <a name="description"></a>描述
`dotnet run` 命令为从源代码使用一个命令运行应用程序提供了一个方便的选项。 它会编译源代码、生成输出程序，然后运行该程序。 此命令可用于快速迭代开发，还可用于运行源分布式程序（例如，网站）。

此命令依赖于 [dotnet 生成](dotnet-build.md)，以便在启动程序前生成 .NET 程序集的源输入。 此命令的要求和源输入的处理均继承自生成命令。 生成命令文档提供了有关这些要求的详细信息。

输出文件会被写入子 *bin* 文件夹，如果此文件夹不存在，则创建一个。 根据需要覆盖文件。 临时文件会被写入子 *obj* 文件夹。  

对于具有多个指定框架的项目，`dotnet run` 将首先选择 .NET Core 框架。 如果不存在，则将出错。 若要指定其他框架，请使用 `--framework` 参数。

必须在项目上下文，而不是生成程序集中使用 `dotnet run` 命令。 如果尝试改为运行可移植应用程序 DLL，应使用 [dotnet](dotnet.md)，切勿使用如下所示的任何命令：
 
`dotnet myapp.dll`

有关 `dotnet` 驱动程序的详细信息，请参阅 [.NET Core 命令行工具 (CLI)](index.md) 主题。

## <a name="options"></a>选项

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此参数后的所有参数均会被传递给正在运行的应用程序。 

`-h|--help`

打印出有关命令的简短帮助。

`-f`, `--framework <FRAMEWORK_IDENTIFIER>`

运行针对给定框架标识符 (FID) 的应用程序。 

`-c`, `--configuration <Debug|Release>`

发布时要使用的配置。 默认值为 `Debug`。

`-p`, `--project [PATH]`

指定要运行的项目。 它可能是 [project.json](project-json.md) 文件的路径或包含 [project.json](project-json.md) 文件的目录路径。 如未指定，则默认为当前目录。 

## <a name="examples"></a>示例

运行当前目录中的项目：`dotnet run` 

运行指定的项目：

`dotnet run --project /projects/proj1/project.json`

运行当前目录中的项目（在本例中，`--help` 参数被传递到正在运行的应用程序，因为使用了 `--` 参数）：

`dotnet run --configuration Release -- --help`


<!--HONumber=Nov16_HO1-->


