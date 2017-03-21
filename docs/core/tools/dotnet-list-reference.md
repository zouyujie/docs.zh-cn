---
title: "dotnet-list reference 命令 | Microsoft Docs"
description: "使用 dotnet-list reference 命令可方便地列出项目到项目的引用。"
keywords: "dotnet-list, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8f954a0c-03f8-4fbc-a529-b313ab12c623
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: e95aa43bfed78d72ef1ea5f3883ae64e06ffaa99
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-list-reference"></a>dotnet-list reference

## <a name="name"></a>名称

`dotnet-list reference` - 列出项目到项目引用。

## <a name="synopsis"></a>摘要

```
dotnet list [project] reference
dotnet list reference [-h|--help]
```

## <a name="description"></a>说明

使用 `dotnet list reference` 命令可方便地列出给定项目的项目引用。

## <a name="arguments"></a>参数

`project`

要列出其引用的项目文件。 如果未指定，此命令会搜索当前目录，以获取解决方案文件。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

列出指定项目的项目引用：

`dotnet list app/app.csproj reference`

列出当前目录中的项目的项目引用：

`dotnet list reference`

