---
title: "dotnet-publish 命令 | Microsoft Docs"
description: "dotnet-publish 命令可将 .NET Core 项目发布到目录。"
keywords: "dotnet-publish, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 0d222382640fc239760f8f51c69f1f306674d7ca

---

#<a name="dotnet-publish-net-core-tools-rc4"></a>dotnet-publish（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅 [dotnet-publish](../../tools/dotnet-publish.md) 主题。

## <a name="name"></a>名称

`dotnet-publish` - 将应用程序及其所有依赖项打包到文件夹，准备进行发布。

## <a name="synopsis"></a>摘要

`dotnet publish [project] 
    [--help] [--framework]  
    [--runtime] [--output]  
    [--version-suffix] [--configuration]`

## <a name="description"></a>描述

`dotnet publish` 编译应用程序、读取 project 文件中指定的所有依赖项并将生成的文件集发布到目录。 

根据可移植应用的类型，生成的目录包含以下内容：

1. 依赖框架的部署 - 应用程序的中间语言 (IL) 代码和应用程序的所有托管依赖项。
2. 独立部署 - 除上述内容外，还包括目标平台的完整运行时。

有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)主题。

## <a name="options"></a>选项

`[project]` 

要发布的项目，如果未指定 `[project]`，默认为当前目录。 

`-h|--help`

打印出有关命令的简短帮助。  

`-f|--framework <FRAMEWORK>`

发布针对给定框架标识符 (FID) 的应用程序。 

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 有关可以使用的运行时标识符 (RID) 列表，请参阅 [RID 目录](../../rid-catalog.md)。

`-o|--output <OUTPUT_PATH>`

指定放置目录的路径。 如未指定，对于可移植应用程序，将默认为 *_./bin/[configuration]/[framework]/_* 或对于独立部署，将默认为 *_./bin/[configuration]/[framework]/[runtime]_*。

`--version-suffix [VERSION_SUFFIX]`

定义在项目文件的版本字段中应替换的 `*` 对象。

`-c|--configuration [Debug|Release]`

发布时要使用的配置。 默认值为 `Debug`。

## <a name="examples"></a>示例

发布应用程序。

`dotnet publish`

使用指定的项目文件发布应用程序

`dotnet publish ~/projects/app1/app1.csproj`
    
使用 `netcoreapp1.0` 框架发布当前应用程序：

`dotnet publish --framework netcoreapp1.0`
    
使用 `netcoreapp1.0` 框架和 `OS X 10.10` 的运行时发布当前应用程序（此 RID 必须存在于项目文件中）。

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

## <a name="see-also"></a>另请参阅
* [框架](../../../standard/frameworks.md)
* [运行时标识符 (RID) 目录](../../rid-catalog.md)



<!--HONumber=Feb17_HO2-->


