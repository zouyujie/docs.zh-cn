---
title: "dotnet-msbuild 命令 - .NET Core CLI | Microsoft Docs"
description: "dotnet-msbuild 命令提供对 MSBuild 命令行的访问。"
keywords: "dotnet-msmsbuild, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 069909ab3890b75502602f57fc15df19bc7dd614
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>名称

`dotnet-msbuild` - 生成项目及其所有依赖项。

## <a name="synopsis"></a>摘要

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>说明

`dotnet msbuild` 命令允许访问功能完备的 MSBuild。

该命令与现有的 MSBuild 命令行客户端具有完全相同的功能。 选项一致。 使用 [MSBuild 命令行引用](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference)获取可用选项的信息。 

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet msbuild`

使用“发布”配置生成项目及其依赖项：

`dotnet msbuild /p:Configuration=Release`

运行发布目标并发布 `osx.10.11-x64` RID：

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`
