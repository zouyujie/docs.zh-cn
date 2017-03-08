---
title: "dotnet-nuget-delete 命令 | Microsoft Docs"
description: "dotnet-nuget-delete 命令从服务器删除或取消列出包。"
keywords: "dotnet-nuget-delete, CLI, CLI 命令, .NET Core"
author: karann-msft
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 6ddffde4-c789-4e90-990e-d35f6a6565d4
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 2ce157e3f32f3e899245e38bb4520b17be3e0b32
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-nuget-delete"></a>dotnet-nuget-delete

## <a name="name"></a>名称

`dotnet-nuget-delete` - 从服务器删除或取消列出包。 

## <a name="synopsis"></a>摘要

```
dotnet nuget delete [<package_name> <package_version>] [-s|--source] [--non-interactive] [-k|--api-key] [--force-english-output]
dotnet nuget delete [-h|--help]
```

## <a name="description"></a>描述

`dotnet nuget delete` 命令从服务器删除或取消列出包。 对于 NuGet.org，该操作将取消列出包。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-s|--source <SOURCE>`

指定服务器 URL。 nuget.org 的支持 URL 包括：`http://www.nuget.org`、`http://www.nuget.org/api/v3` 和 `http://www.nuget.org/api/v2/package`。 对于专用源，请替换主机名（例如，`%hostname%/api/v3`）。

`--non-interactive`

不提示用户输入或确认。

`-k|--api-key <API_KEY>`

服务器的 API 密钥。

`--force-english-output`

强制命令行输出以英语显示。

## <a name="examples"></a>示例

删除包 MyPackage 的 1.0 版：

`dotnet nuget delete MyPackage 1.0` 

删除包 MyPackage 的 1.0 版（不提示用户需要凭据或其他输入）：

`dotnet nuget delete MyPackage 1.0 --non-interactive`

