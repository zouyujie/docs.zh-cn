---
title: "dotnet-new 命令 | .NET Core"
description: "dotnet-new 命令可在当前目录中创建新的 .NET Core 项目。"
keywords: "dotnet-new, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 263c3d05-3a47-46a6-8023-3ca16b488410
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: 29ccc12ff893d316c816d22da862f90bfc9334ff

---

#<a name="dotnetnew"></a>dotnet-new

## <a name="name"></a>名称
dotnet-new -- 在当前目录中创建新的 .NET Core 项目

## <a name="synopsis"></a>摘要
`dotnet new [--help] [--type] [--lang]`

## <a name="description"></a>说明
`dotnet new` 命令可以简便地初始化有效 .NET Core 项目和示例源代码以试用命令行接口 (CLI) 工具集。 

在目录上下文中调用此命令。 调用时，该命令将导致两个主要项目被放置到当前目录： 

1. 包含示例“Hello World”程序的 `Program.cs`（或 `Program.fs`）文件。
2. 有效的 `project.json` 文件。

此后，已准备好进一步编译和/或编辑该项目。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-l|--lang <C#|F#>`

项目语言。 默认为 `C#`。 其他有效值为 `csharp`、`fsharp`、`cs` 和 `fs`。

`-t|--type`

项目类型。 C# 的有效值为 `console`、`web`、`lib` 和 `xunittest`，对于 F #，仅 `console` 有效。 

## <a name="examples"></a>示例

在当前目录中创建 C# 控制台应用程序项目：

`dotnet new` 或 `dotnet new --lang c#` 
   
在当前目录中创建 F# 控制台应用程序项目：

`dotnet new --lang f#`
  
在当前目录中创建新的 ASP.NET Core C# 应用程序项目：

`dotnet new -t web`


<!--HONumber=Nov16_HO1-->


