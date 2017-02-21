---
title: "dotnet-sln 命令 | Microsoft 文档"
description: "使用 dotnet-sln 命令，可以便捷地在解决方案文件中添加、删除和列出项目。"
keywords: "dotnet-run, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 02/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e5a72d3e-c14b-4b0a-a978-c5e54a0988c6
translationtype: Human Translation
ms.sourcegitcommit: 6c0474e2964043b6c090ecb4e68b46ff42ca670c
ms.openlocfilehash: c5ed2482222b02b8b50599b48a28afa5922e0135

---
# <a name="dotnet-sln"></a>dotnet-sln

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>名称

`dotnet-sln` - 修改 .NET Core 解决方案文件。

## <a name="synopsis"></a>摘要

```
dotnet sln [<SLN_NAME>] add <project> <project>
dotnet sln [<SLN_NAME>] add **/**
dotnet sln [<SLN_NAME>] remove <project> <project>
dotnet sln [<SLN_NAME>] remove **/**
dotnet sln [<SLN_NAME>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>描述

使用 `dotnet sln` 命令，可以便捷地在解决方案文件中添加、删除和列出项目。

## <a name="commands"></a>命令

`add <project>`

`add **/*`

将一个或多个项目添加到解决方案文件中。 基于 Unix/Linux 的终端支持 glob 模式。

`remove <project>`

`remove **/*`

从解决方案文件中删除一个或多个项目。 基于 Unix/Linux 的终端支持 glob 模式。

`list`

在解决方案文件中列出所有项目。

## <a name="arguments"></a>参数

`SLN_NAME`

要使用的解决方案文件。 如果未指定，此命令会搜索当前目录，以获取解决方案文件。 如果目录中有多个解决方案文件，必须指定一个。

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

使用 glob 模式将多个项目添加到解决方案中：

`dotnet sln add **/**/*.fsproj`



<!--HONumber=Feb17_HO2-->


