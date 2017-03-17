---
title: "dotnet-pack 命令 | Microsoft Docs"
description: "dotnet-pack 命令可为 .NET Core 项目创建 NuGet 包。"
keywords: "dotnet-pack, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8dbbb3f7-b817-4161-a6c8-a3489d05e051
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 88289a09a22bf20ec9089ec6a74269cd682a305b
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-pack"></a>dotnet-pack

## <a name="name"></a>名称

`dotnet-pack` - 将代码打包到 NuGet 包。

## <a name="synopsis"></a>摘要

```
dotnet pack [project] [-o|--output] [--no-build] [--include-symbols] [--include-source] [-c|--configuration] [--version-suffix] [-s|--serviceable] [-v|--verbosity]
dotnet pack [-h|--help]
```

## <a name="description"></a>描述

`dotnet pack` 命令生成项目并创建 NuGet 包。 该命令的结果是一个 NuGet 包。 如果 `--include-symbols` 选项存在，将创建包含调试符号的另一个包。 

将被打包项目的 NuGet 依赖项添加到 `nuspec` 文件，以便在安装包时可以将其解析。 项目到项目的引用不会打包到项目内。 目前，如果具有项目到项目的依赖项，则每个项目均应含一个包。

`dotnet pack` 默认首先生成项目。 如果希望避免此情况，则选择 `--no-build` 选项。 这在持续集成 (CI) 生成方案中非常有用，例如，在其中你可以知道代码是刚刚生成的。 

## <a name="arguments"></a>参数

`project` 
    
要打包的项目。 它可能是 [csproj file](csproj.md) 文件或目录的路径。 如果省略，则将默认为当前目录。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-o|--output <OUTPUT_DIRECTORY>`

将生成的包放置在指定目录。 

`--no-build`

打包前不生成项目。 

`--include-symbols`

生成符号 nupkg。 

`--include-source`

将源文件包括在 NuGet 包中。 源文件包括在 `nupkg` 内的 `src` 文件夹中。 

`-c|--configuration <Debug|Release>`

生成项目时要使用的配置。 如未指定，则默认为 `Debug`。

`--version-suffix <VERSION_SUFFIX>`

定义项目中 $(VersionSuffix) MSBuild 属性的值。

`-s|--serviceable`

设置包中可用的标志。 有关详细信息，请参阅 https://aka.ms/nupkgservicing。

`--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

打包当前目录中的项目：

`dotnet pack`

打包 app1 项目：

`dotnet pack ~/projects/app1/project.csproj`
    
打包当前目录中的项目并将生成的包放置到指定文件夹：

`dotnet pack --output nupkgs`

将当前目录中的项目打包到指定文件夹并跳过生成步骤：

`dotnet pack --no-build --output nupkgs`

打包当前项目并更新生成的具有给定后缀的包版本。 在 *.csproj* 文件中，将项目的版本后缀配置为 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`。

`dotnet pack --version-suffix "ci-1234"`
