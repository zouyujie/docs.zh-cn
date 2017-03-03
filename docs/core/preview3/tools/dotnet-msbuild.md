---
title: "dotnet-msbuild 命令 | Microsoft Docs"
description: "dotnet-msbuild 命令提供对 MSBuild 命令行的访问。"
keywords: "dotnet-msmsbuild, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: 06d4210e5dff97d3e96efff8ae8e84efc27fb7d2
ms.lasthandoff: 01/21/2017

---

#<a name="dotnet-msbuild"></a>dotnet-msbuild

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>名称 
dotnet-msbuild - 生成项目及其所有依赖项。

## <a name="synopsis"></a>摘要

`dotnet msbuild <msbuild_arguments>`

## <a name="description"></a>描述
`dotnet msbuild` 命令允许访问完全起作用的 MSBuild 

该命令与现有的 MSBuild 命令行客户端具有完全相同的功能。 选项一致。 可以使用 [MSBuild 命令行参考](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference)来熟悉选项。 

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet msbuild`

使用“发布”配置生成项目及其依赖项：

`dotnet msbuild /p:Configuration=Release`

运行发布目标并发布 `osx.10.11-x64` RID：

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`

