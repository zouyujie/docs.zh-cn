---
title: "dotnet-restore 命令 | Microsoft Docs"
description: "了解如何使用 dotnet-restore 命令还原依赖项和特定于项目的工具。"
keywords: "dotnet-restore, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fd7a5769-afbe-4838-bbaf-3ae0cfcbb914
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: a55cd932045a59f08146dff367a87eb6fe61f6e5
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-restore"></a>dotnet-restore

## <a name="name"></a>名称

`dotnet-restore` - 恢复项目的依赖项和工具。

## <a name="synopsis"></a>摘要

```
dotnet restore [root] [-s|--source] [-r|--runtime] [--packages] [--disable-parallel] [--configfile] [--no-cache] [--ignore-failed-sources] [--no-dependencies] [-v|--verbosity]
dotnet restore [-h|--help]
```

## <a name="description"></a>描述

`dotnet restore` 命令使用 NuGet 还原依赖项以及在 project 文件中指定的特定于项目的工具。 默认情况下，并行完成对依赖项和工具的还原。

为了还原依赖项，NuGet 需要包所在的源。 常常通过 NuGet.config 配置文件提供源；安装 CLI 工具时存在一个默认源。 可以通过在项目目录中创建自己的 NuGet.config 文件来指定多个源。 此外，还可以在每次针对命令提示符进行调用时指定源。 

对于依赖项，可以使用 `--packages` 参数指定还原操作期间放置还原包的位置。 如未指定，则使用默认的 NuGet 包缓存。 可在所有操作系统上的用户主目录（例如，Linux 上的 */home/user1* 或 Windows 上的 *C:\Users\user1*）中的 `.nuget/packages` 目录找到它。

对于特定于项目的工具，`dotnet restore` 首先还原打包工具所在的包，然后继续还原 project 文件中指定的工具依赖项。

## <a name="options"></a>选项

`root` 
    
要还原的项目文件的可选路径。 

`-h|--help`

打印出有关命令的简短帮助。

`-s|--source <SOURCE>`

指定要在还原操作期间使用的 NuGet 包源。 这会替代 NuGet.config 文件中指定的所有源。 多次指定此选项可以提供多个源。

`--packages <PACKAGES_DIRECTORY]`

指定放置还原包的目录。 

`--disable-parallel`

禁用并行还原多个项目。 

`--configfile <FILE>`

用于还原操作的 NuGet 配置文件 (NuGet.config)。

`--no-cache`

指定不缓存包和 HTTP 请求。

` --ignore-failed-sources`

如果存在符合版本要求的包，则源失败时警告。

`--no-dependencies`

当使用 P2P 引用还原项目时，不要还原引用，只需还原根项目。

`--verbosity <LEVEL>`

在输出中显示此数量的详细信息。 级别可以是 `normal`、`quiet` 或 `detailed`。

## <a name="examples"></a>示例

还原当前目录中项目的依赖项和工具：

`dotnet restore` 

还原在给定路径中找到的 `app1` 项目的依赖项和工具：

`dotnet restore ~/projects/app1/app1.csproj`
    
通过将提供的文件路径用作回退源，在当前目录中还原项目的依赖项和工具：

`dotnet restore -f c:\packages\mypackages` 

通过将提供的两个文件路径用作回退源，还原当前目录中项目的依赖项和工具：

`dotnet restore -f c:\packages\mypackages -f c:\packages\myotherpackages` 

还原当前目录中项目的依赖项和工具并仅显示输出中的错误：

`dotnet restore --verbosity Error`

