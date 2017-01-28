---
title: "dotnet-build 命令 | .NET Core SDK"
description: "dotnet-build 命令可生成项目及其所有依赖项。"
keywords: "dotnet-build, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 70285a83-4103-4617-be8b-d0e1e9a4a91d
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 04c4d77b31bf4a1bdb425d837c490440e7312e57

---

#<a name="dotnet-build"></a>dotnet-build

## <a name="name"></a>名称 
dotnet-build - 生成项目及其所有依赖项 

## <a name="synopsis"></a>摘要

`dotnet build [--help] [--output]  [--framework]  
    [--configuration]  [--runtime] [--version-suffix]
    [--build-profile]  [--no-incremental] [--no-dependencies]
    [<project>]`

## <a name="description"></a>描述

`dotnet build` 命令可将源项目及其依赖项的多个源文件生成为二进制文件。 默认情况下，生成的二进制文件为中间语言 (IL) 并具有 DLL 扩展名。 
`dotnet build` 还删除了 `\*.deps` 文件，该文件概述了主机运行应用程序所需的条件。  

生成需要资产文件（列出了应用程序的所有依赖项的文件），这意味着生成代码前需运行 [`dotnet restore`](dotnet-restore.md)。

开始编译前，`build` 谓词会分析项目及其依赖项，以便进行增量安全检查。
如果通过所有检查，生成将继续执行项目及其依赖项的增量编译；否则，它将退回到非增量编译。 通过配置文件标志，用户可以选择接收有关如何缩短生成时间的附加信息。

若要生成可执行的应用程序而不是库，则需要设置 `<OutputType>` 属性：

```xml
<PropertyGroup>
    <OutputType>Exe</OutputType>
</PropertyGroup>
```

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-o|--output <OUTPUT_DIRECTORY>`

放置生成二进制文件的目录。 指定此选项时还需要定义 `--framework`。

`-f|--framework <FRAMEWORK>`

编译特定框架。 需要在[项目文件](csproj.md)中定义该框架。

`-c|--configuration [Debug|Release]`

定义一个配置，根据该配置进行生成。  如果省略，则默认为 `Debug`。

`-r|--runtime [RUNTIME_IDENTIFIER]`

要生成的目标运行时。 有关可以使用的运行时标识符 (RID) 列表，请参阅 [RID 目录](../../rid-catalog.md)。 

`--version-suffix [VERSION_SUFFIX]`

定义在项目文件的版本字段中应替换的 `*` 对象。 格式遵循 NuGet 的版本准则。 

`--build-profile`

打印出用户需要处理的增量安全检查，以便自动打开增量编译。

`--no-incremental`

将生成标记为对增量生成不安全。 这将关闭增量编译并强制完全重新生成项目依赖项关系图。

`--no-dependencies`

忽略项目间引用，并仅生成指定要生成的根项目。

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet build`

使用“发布”配置生成项目及其依赖项：

`dotnet build --configuration Release`

针对特定运行时（本例中为 Ubuntu 16.04）生成项目及其依赖项：

`dotnet build --runtime ubuntu.16.04-x64`



<!--HONumber=Nov16_HO3-->


