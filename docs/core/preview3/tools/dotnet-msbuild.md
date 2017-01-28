---
title: "dotnet-msbuild 命令 | .NET Core SDK"
description: "dotnet-msmsbuild 命令提供对 MSmsbuild 命令行的访问"
keywords: "dotnet-msmsbuild, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: cde9d9577246a9025d646ce2a6d574a18512146e
ms.openlocfilehash: 51a3afdcf591b8147790d78471c6fee63ceb7f2d

---

#<a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>名称 
dotnet-msbuild - 生成项目及其所有依赖项 

## <a name="synopsis"></a>摘要

`dotnet msbuild <msbuild_arguments>`

## <a name="description"></a>描述
`dotnet msbuild` 命令允许访问完全起作用的 MSBuild 

该命令与现有的 MSBuild 命令行客户端具有完全相同的功能。 选项一致。 可以使用[现有文档](https://msdn.microsoft.com/en-us/library/ms164311.aspx)来熟悉命令参考。 

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet msbuild`

使用“发布”配置生成项目及其依赖项：

`dotnet msbuild /p:Configuration=Release`

运行发布目标并发布 `osx.10.11-x64` RID：

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`



<!--HONumber=Nov16_HO3-->


