---
title: "dotnet-remove package 命令 | Microsoft Docs"
description: "使用 dotnet-remove package 命令可方便地删除对项目的 NuGet 包引用。"
keywords: "dotnet-remove, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2fcc8d37-16b3-4581-8038-832160e72d36
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 87c80ad193df9cc3e0feabc41bb58f1d8dda23cd
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-remove-package"></a>dotnet-remove package

## <a name="name"></a>名称

`dotnet-remove package` - 从项目文件删除包引用。

## <a name="synopsis"></a>摘要

```
dotnet remove [project] package <package_name>
dotnet remove package [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet remove package` 命令可方便地从项目删除 NuGet 包引用。

## <a name="arguments"></a>参数

`project`

要操作的项目文件。 如果未指定，此命令会搜索当前目录，以获取解决方案文件。

`package_name`

要删除的包引用。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

从当前目录中的项目删除 `Newtonsoft.Json` NuGet 包：

`dotnet remove package Newtonsoft.Json`
