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
ms.assetid: 8a7e1c52-5c57-4bf5-abad-727450ebeefd
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 1cf1611ab83874ad44855521d21040d102206338

---

#<a name="dotnet-publish"></a>dotnet-publish

> [!WARNING]
> 本主题适用于 .NET Core 工具预览版 2。 对于 .NET Core 工具 RC4 版本，请参阅 [dotnet-publish（.NET Core 工具 RC4）](../preview3/tools/dotnet-publish.md)主题。

## <a name="name"></a>名称

`dotnet-publish` - 将应用程序及其所有依赖项打包到文件夹，准备进行发布。

## <a name="synopsis"></a>摘要

`dotnet publish [project] 
    [--help] [--framework]  
    [--runtime] [--build-base-path] [--output]  
    [--version-suffix] [--configuration] [--native-subdirectory] [--no-build]`

## <a name="description"></a>描述

`dotnet publish` 编译应用程序、读取 [project.json](project-json.md) 文件中指定的所有依赖项并将生成的文件集发布到目录。 

根据可移植应用的类型，生成的目录包含以下内容：

1. 可移植应用程序 - 应用程序的中间语言 (IL) 代码和应用程序的所有托管依赖项。
    * 含本机依赖项的可移植应用程序 - 除上述内容外，还包括每个本机依赖项的受支持平台的子目录。 
2. 独立应用程序 - 除上述内容外，还包括目标平台的完整运行时。

有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)主题。

## <a name="options"></a>选项

`[project]` 

要发布的项目，如果未指定 `[project]`，默认为当前目录。 此值可以是 [project.json](project-json.md) 文件或包含 [project.json](project-json.md) 文件的项目目录的路径。 如果找不到 [project.json](project-json.md) 文件，`dotnet publish` 会引发错误。 

`-h|--help`

打印出有关命令的简短帮助。  

`-f|--framework <FRAMEWORK>`

发布针对给定框架标识符 (FID) 的应用程序。 如未指定，则从 [project.json](project-json.md#frameworks) 读取 FID。 如果找不到有效框架，该命令会引发错误。 如果找到多个有效框架，该命令会发布所有有效框架。 

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 有关可以使用的运行时标识符 (RID) 列表，请参阅 [RID 目录](../rid-catalog.md)。

`-b|--build-base-path <OUTPUT_DIRECTORY>`

放置临时输出的目录。

`-o|--output <OUTPUT_PATH>`

指定放置目录的路径。 如未指定，对于可移植应用程序，将默认为 *_./bin/[configuration]/[framework]/_* 或对于独立部署，将默认为 *_./bin/[configuration]/[framework]/[runtime]_*。

`--version-suffix [VERSION_SUFFIX]`

定义在 project.json 文件的版本字段中应替换 `*` 的对象。

`-c|--configuration [Debug|Release]`

发布时要使用的配置。 默认值为 `Debug`。

`[--native-subdirectory]` 依赖项包的本机资产中的子目录包括在输出中的临时机制。 

`[--no-build]` 发布前不生成项目。

## <a name="examples"></a>示例

使用在 `project.json` 中找到的框架发布应用程序。 如果 `project.json` 包含[运行时](project-json.md#runtimes)节点，则发布当前平台的 RID。

`dotnet publish`

使用指定的 [project.json](project-json.md) 发布应用程序：

`dotnet publish ~/projects/app1/project.json`
    
使用 `netcoreapp1.0` 框架发布当前应用程序：

`dotnet publish --framework netcoreapp1.0`
    
使用 `netcoreapp1.0` 框架和 `OS X 10.10` 的运行时发布当前应用程序（此 RID 必须存在于 `project.json` [运行时](project-json.md#runtimes)节点中）：

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

## <a name="see-also"></a>另请参阅
* [框架](../../standard/frameworks.md)
* [运行时标识符 (RID) 目录](../rid-catalog.md)


<!--HONumber=Feb17_HO2-->


