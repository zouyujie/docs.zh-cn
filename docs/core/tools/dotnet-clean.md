---
title: "dotnet-clean 命令 | Microsoft Docs"
description: "dotnet-clean 命令可清除当前目录。"
keywords: "dotnet-clean, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: eff65fa1-bab4-4421-8260-d0a284b690b2
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 3c00f4616932318b5dc5d77cbdf6c645696a4226
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-clean"></a>dotnet-clean

## <a name="name"></a>名称

`dotnet-clean` - 清除项目输出。 

## <a name="synopsis"></a>摘要

```
dotnet clean [project] [-o|--output] [-f|--framework] [-c|--configuration] [-v|--verbosity]
dotnet clean [--help] 
```

## <a name="description"></a>描述

`dotnet clean` 命令将清除上一个生成的输出。 它是以 MSBuild 目标的形式实现，以便可以对项目进行评估。 只会清除在生成过程中创建的输出。 中间 (`obj`) 和最终输出 (`bin`) 文件夹都会被清除。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-o|--output <OUTPUT_DIRECTORY>`

包含已生成的二进制文件的目录。 指定此选项时还需要定义 `--framework`。 如果未在生成时指定此属性，无需为了进行清除而指定它。

`-f|--framework <FRAMEWORK>`

在生成时指定的框架。 如果未在生成时指定此属性，无需为了进行清除而指定它。 需要在[项目文件](csproj.md)中定义该框架。

`-c|--configuration [Debug|Release]`

定义一个配置，根据该配置运行生成。  如果省略，则默认为 `Debug`。 如果未在生成时指定此属性，无需为了进行清除而指定它。

`-v|--verbosity <Quiet|Minimal|Normal|Diag>`

定义用于 `dotnet clean` 命令调用的详细级别。 这是标准的 [MSBuild 详细级别](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference)。 

## <a name="examples"></a>示例

清除项目的默认生成：

`dotnet clean`

清除使用版本配置生成的项目：

`dotnet clean --configuration Release`

