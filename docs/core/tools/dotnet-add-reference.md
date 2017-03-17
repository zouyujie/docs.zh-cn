---
title: "dotnet-add reference 命令 | Microsoft Docs"
description: "使用 dotnet-add reference 命令可方便地添加“项目到项目”引用。"
keywords: "dotnet-add, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e2a3efd-443c-4f23-a1b1-a662a5387879
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 7d23377244cfe60730b50bd247209de6e90bec70
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-add-reference"></a>dotnet-add reference

## <a name="name"></a>名称

`dotnet-add reference` - 添加“项目到项目”引用。

## <a name="synopsis"></a>摘要

```
dotnet add [project] reference [-f|--framework] <project_references>
dotnet add reference [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet add reference` 命令可方便地向项目添加项目引用。 运行该命令后，会将 [`<ProjectReference>`](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-items) 片段添加到项目文件。

```xml
<ItemGroup>
  <ProjectReference Include="app.csproj" />
  <ProjectReference Include="..\lib2\lib2.csproj" />
  <ProjectReference Include="..\lib1\lib1.csproj" />
</ItemGroup>
```

## <a name="arguments"></a>参数

`project`

要操作的项目文件。 如果未指定，此命令会搜索当前目录，以获取解决方案文件。

`project_references`

要添加的“项目到项目”引用。 可指定一个或多个项目。 基于 Unix/Linux 的终端支持 glob 模式。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-f|--framework <FRAMEWORK>`

仅在以特定框架为目标时添加项目引用。

## <a name="examples"></a>示例

添加项目引用：

`dotnet add app/app.csproj reference lib/lib.csproj`

添加多个项目引用：

`dotnet add reference lib1/lib1.csproj lib2/lib2.csproj`

使用通配模式在 Linux/Unix 上添加多个项目引用：

`dotnet add app/app.csproj reference **/*.csproj`
