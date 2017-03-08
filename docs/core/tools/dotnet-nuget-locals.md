---
title: "dotnet-nuget-locals 命令 | Microsoft Docs"
description: "dotnet-nuget-locals 命令清除或列出本地 NuGet 资源，例如 http 请求缓存、临时缓存或计算机范围的全局包文件夹。"
keywords: "dotnet-nuget-locals, CLI, CLI 命令, .NET Core"
author: karann-msft
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8440229e-317e-4dc1-9463-cba5fdb12c3b
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 3d8ca57c3c9c25a59b98552784b057182c9100a3
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-nuget-locals"></a>dotnet-nuget-locals

## <a name="name"></a>名称

`dotnet-nuget-locals` - 清除或列出本地 NuGet 资源，例如 http 请求缓存、临时缓存或计算机范围的全局包文件夹。 

## <a name="synopsis"></a>摘要

```
dotnet nuget locals <cache_location> [(-c|--clear)|(-l|--list)] [--force-english-output]
dotnet nuget locals [-h|--help]
```

其中 `<cache_location>` 是以下值之一：`all`、`http-cache`、`packages-cache`、`global-packages` 或 `temp`。

## <a name="description"></a>描述

`dotnet nuget locals` 命令清除或列出本地 NuGet 资源，例如 http 请求缓存、临时缓存或计算机范围的全局包文件夹。

## <a name="arguments"></a>参数

`all`

表示指定的操作应该被应用于所有缓存类型，即 http 请求缓存、全局包缓存和临时缓存。

`http-cache`

表示指定的操作应仅应用于 http 请求缓存。 其他缓存位置不受影响。

`global-packages`

表示指定的操作应仅应用于全局包缓存。 其他缓存位置不受影响。

`temp`

表示指定的操作应仅应用于临时缓存。 其他缓存位置不受影响。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-c|--clear`

清除选项用于对指定的缓存类型执行清除操作。 缓存目录的内容被以递归方式删除。 为了使操作成功，正在执行的用户/组应该具有对缓存目录中的文件的权限。 反之，则显示错误，指示未被清除的文件/文件夹。

`-l|--list`

列表选项用于显示指定缓存类型的位置。 

`--force-english-output`

强制命令行输出以英语显示。

## <a name="examples"></a>示例

显示所有本地缓存目录的路径，即 http-cache 目录、global-packages 缓存目录和临时缓存目录。

`dotnet nuget locals –l all`

显示本地 http 缓存录的路径：

`dotnet nuget locals --list http-cache`

清除所有本地缓存目录中的所有文件，即 http 缓存目录、全局包缓存目录和临时缓存目录。

`dotnet nuget locals --clear all`

清除本地全局包缓存目录中的所有文件：

`dotnet nuget locals -c global-packages`

清除本地临时缓存目录中的所有文件：

`dotnet nuget locals -c temp`

## <a name="troubleshooting"></a>疑难解答

有关使用 `dotnet-nuget-locals` 命令时最常遇到的问题和错误的详细信息，请参阅 [Managing the NuGet cache](https://docs.microsoft.com/nuget/consume-packages/managing-the-nuget-cache)（管理 NuGet 缓存）。

