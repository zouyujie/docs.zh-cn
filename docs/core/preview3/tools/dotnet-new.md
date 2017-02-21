---
title: "dotnet-new 命令 | Microsoft Docs"
description: "dotnet-new 命令可在当前目录中创建新的 .NET Core 项目。"
keywords: "dotnet-new, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 02/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
translationtype: Human Translation
ms.sourcegitcommit: 96fd8ea3e55ea33e0bdd0bf3c50a10d0de6db1a1
ms.openlocfilehash: f0c62647c5817db2057c60a7a95a62f08f7889a5

---
#<a name="dotnet-new-net-core-tools-rc4"></a>dotnet-new（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅 [dotnet-new](../../tools/dotnet-new.md) 主题。

## <a name="name"></a>名称
dotnet-new - 在当前目录中新建 .NET Core 项目

## <a name="synopsis"></a>摘要
```
dotnet new [template] [-lang|--language] [-n|--name] [-o|--output] [-h|--help]
dotnet new [template] [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>描述
使用 `dotnet new` 命令，可以便捷地初始化有效的 .NET Core 项目和示例源代码，从而试用命令行接口 (CLI) 工具集。 

在目录上下文中调用此命令。 调用后，此命令会根据传递给它的模板和选项来创建资源和文件。 

此后，已准备好进一步编译和/或编辑该项目。 

## <a name="arguments"></a>参数
template - 调用命令时要实例化的模板。

此命令包含模板的默认列表；使用 `dotnet new --help`。 

## <a name="options"></a>选项

`-l|--list`         

列出包含指定名称的模板。

`-lang|--language`  

指定要创建的模板的语言

`-n|--name`         

要创建的输出的名称。 如果未指定名称，使用的是当前目录的名称。

`-o|--output`       

用于放置生成的输出的位置。

`-all|--show-all`   

显示特定类型项目的所有模板。

`-h|--help`

打印命令帮助。

## <a name="template-options"></a>模板选项
每个项目模板都可能有附加选项。 例如，核心模板有以下附加选项：

**console、xunit、mstest**

`-f|--framework` - 指定目标框架。 可取值为 netcoreapp1.0 或 netcoreapp1.1（默认值为 netcoreapp1.0）

**web、webapi**

`-f|--framework` - 指定目标框架。 可取值为 netcoreapp1.0 或 netcoreapp1.1（默认值为 netcoreapp1.0）
 
**mvc**

`-f|--framework` - 指定目标框架。 可取值为 netcoreapp1.0 或 netcoreapp1.1（默认值为 netcoreapp1.0）

`-au|--authentication` - 要使用的身份验证类型。 可取值为 None 或 Individual（默认值为 None）

`-uld|--use-local-db` - 指示是否使用 LocalDB，而不是 SQLite。 可取值为 true 或 false（默认值为 false）

**classlib**

`-f|--framework` - 指定目标框架。 可取值为 netcoreapp1.0、netcoreapp1.1 和 netstandard1.0 - 1.6（默认值为 netstandard1.4）。

## <a name="examples"></a>示例

在当前目录中创建 F# 控制台应用程序项目：

`dotnet new console -lang f#` 
   
在当前目录中新建定位 .NET Core 1.0 且没有设置身份验证的 ASP.NET Core C# MVC 应用程序项目：  

`dotnet new mvc -au None -f netcoreapp1.0`
 
新建定位 .NET Core 1.1 的 XUnit 应用程序：

`dotnet new xunit --Framework netcoreapp1.1`

列出适用于 MVC 的所有模板：

`dotnet new mvc -l`


<!--HONumber=Feb17_HO3-->


