---
title: "dotnet-remove reference 命令 | Microsoft Docs"
description: "使用 dotnet-remove reference 命令可方便地删除“项目到项目”引用。"
keywords: "dotnet-remove, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 889c6b7e-a313-40b1-9fd3-6a6f4c52f1d0
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 1f1a364b703c6b83a9b21ee420d62411bf9cd3ec
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-remove-reference"></a>dotnet-remove reference

## <a name="name"></a>名称

`dotnet-remove reference` - 删除“项目到项目”引用。

## <a name="synopsis"></a>摘要

```
dotnet remove [project] reference [-f|--framework] <project_references>
dotnet remove reference [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet remove reference` 命令可方便地从项目删除项目引用。

## <a name="arguments"></a>参数

`project`

要操作的项目文件。 如果未指定，此命令会搜索当前目录，以获取解决方案文件。

`project_references`

要删除的项目到项目引用。 可指定一个或多个项目。 基于 Unix/Linux 的终端支持 glob 模式。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-f|--framework <FRAMEWORK>`

仅在以特定框架为目标时删除引用。

## <a name="examples"></a>示例

从指定项目删除项目引用：

`dotnet remove app/app.csproj reference lib/lib.csproj`

从当前目录中的项目删除多个项目引用：

`dotnet remove reference lib1/lib1.csproj lib2/lib2.csproj`

使用通配模式删除多个项目引用：

`dotnet remove app/app.csproj reference **/*.csproj`
