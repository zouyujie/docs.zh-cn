---
title: "dotnet-sln 命令 - .NET Core CLI | Microsoft Docs"
description: "使用 dotnet-sln 命令，可以便捷地在解决方案文件中添加、删除和列出项目。"
keywords: "dotnet-sln, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e5a72d3e-c14b-4b0a-a978-c5e54a0988c6
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 2cdfd02f7735b106fde910b8906ba4dfae860952
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-sln"></a>dotnet-sln

## <a name="name"></a>名称

`dotnet-sln` - 修改 .NET Core 解决方案文件。

## <a name="synopsis"></a>摘要

```
dotnet sln [<SOLUTION_NAME>] add <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] add **/**
dotnet sln [<SOLUTION_NAME>] remove <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] remove **/**
dotnet sln [<SOLUTION_NAME>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet sln` 命令，可以便捷地在解决方案文件中添加、删除和列出项目。

## <a name="commands"></a>命令

`add <PROJECT> ...`

`add **/*`

将一个或多个项目添加到解决方案文件中。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`remove <PROJECT> ...`

`remove **/*`

从解决方案文件中删除一个或多个项目。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`list`

在解决方案文件中列出所有项目。

## <a name="arguments"></a>参数

`SOLUTION_NAME`

要使用的解决方案文件。 如果未指定，此命令会搜索当前目录来获取一个项目文件。 如果目录中有多个解决方案文件，必须指定一个。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

将一个项目添加到解决方案中：

`dotnet sln todo.sln add todo-app/todo-app.csproj`

将一个项目添加到当前目录中的解决方案：

`dotnet sln add todo-app.csproj`

从解决方案中删除一个项目：

`dotnet sln todo.sln remove todo-app/todo-app.csproj`

使用通配模式将多个项目添加到解决方案中：

`dotnet sln add **/**/*.fsproj`

