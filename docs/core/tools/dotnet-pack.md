---
title: "dotnet-pack 命令 | .NET Core SDK"
description: "dotnet-pack 命令可为 .NET Core 项目创建 NuGet 包。"
keywords: "dotnet-pack, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8b4b8cef-f56c-4a10-aa01-fde8bfaae53e
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: e83c8ad302590bcd77129c3ff325e498da751e69

---

#<a name="dotnetpack"></a>dotnet-pack

## <a name="name"></a>名称

`dotnet-pack` - 将代码打包到 NuGet 包

## <a name="synopsis"></a>摘要

`dotnet pack [--help] [--output]  
    [--no-build] [--build-base-path]  
    [--configuration]  [--version-suffix]
    [project]`  

## <a name="description"></a>描述

`dotnet pack` 命令生成项目并创建 NuGet 包。 此操作将生成两个含有 `nupkg` 扩展名的包。 一个包含有代码，另一个含有调试符号。 

将被打包项目的 NuGet 依赖项添加到 nuspec 文件，以便在安装包时可以将其解析。 项目到项目的引用不会打包到项目内。 目前，如果具有项目到项目的依赖项，则每个项目均应含一个包。

`dotnet pack` 默认首先生成项目。 如果希望避免此情况，则选择 `--no-build` 选项。 这在持续集成 (CI) 生成方案中非常有用，例如，在其中你可以知道代码是刚刚生成的。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`[project]` 
    
要打包的项目。 它可能是 [project.json](project-json.md) 文件或目录的路径。 如果省略，则将默认为当前目录。 

`-o|--output <OUTPUT_DIRECTORY>`

将生成的包放置在指定目录。 

`--no-build`

打包前不生成项目。 

`--build-base-path`

将临时生成项目放置在指定目录。 默认情况下，转到当前目录中的 `obj` 目录。 

`-c|--configuration <Debug|Release>`

生成项目时要使用的配置。 如未指定，则默认为 `Debug`。

`--version-suffix`

更新了含有指定字符串的 `-*` 包版本后缀中的星形。

## <a name="examples"></a>示例

打包当前目录中的项目：

`dotnet pack`

打包 app1 项目：

`dotnet pack ~/projects/app1/project.json`
    
打包当前目录中的项目并将生成的包放置到指定文件夹：

`dotnet pack --output nupkgs`

将当前目录中的项目打包到指定文件夹并跳过生成步骤：

`dotnet pack --no-build --output nupkgs`

打包当前项目并更新生成的具有给定后缀的包版本。 例如，版本 `1.0.0-*` 将更新为 `1.0.0-ci-1234`。

`dotnet pack --version-suffix "ci-1234"`


<!--HONumber=Nov16_HO1-->


