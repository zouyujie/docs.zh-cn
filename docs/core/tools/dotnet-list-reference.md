---
title: "dotnet-list reference 命令 - .NET Core CLI | Microsoft Docs"
description: "使用 dotnet-list reference 命令可方便地列出项目到项目的引用。"
keywords: "dotnet-list, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8f954a0c-03f8-4fbc-a529-b313ab12c623
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: fdaf2a6f66801be68507ccabe7e0f2fea5433e65
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-list-reference"></a>dotnet-list reference

## <a name="name"></a>名称

`dotnet-list reference` - 列出项目到项目引用。

## <a name="synopsis"></a>摘要

`dotnet list [<PROJECT>] reference [-h|--help]`

## <a name="description"></a>说明

使用 `dotnet list reference` 命令可方便地列出给定项目的项目引用。

## <a name="arguments"></a>参数

`PROJECT`

指定用于列出引用的项目文件。 如果未指定，此命令会搜索当前目录，以获取项目文件。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

列出指定项目的项目引用：

`dotnet list app/app.csproj reference`

列出当前目录中的项目的项目引用：

`dotnet list reference`

