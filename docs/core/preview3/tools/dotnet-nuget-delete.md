---
title: "dotnet-nuget-delete 命令 | Microsoft Docs"
description: "dotnet-nuget-delete 命令从服务器删除或取消列出包。"
keywords: "dotnet-nuget-delete, CLI, CLI 命令, .NET Core"
author: karann-msft
ms.author: mairaw
ms.date: 11/11/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 6ddffde4-c789-4e90-990e-d35f6a6565d4
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: 787b1427b1064943570cbc361042ab2f20d11088
ms.lasthandoff: 01/21/2017

---

#<a name="dotnet-nuget-delete"></a>dotnet-nuget-delete

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>名称 
`dotnet-nuget-delete` - 从服务器删除或取消列出包。 

## <a name="synopsis"></a>摘要

`dotnet nuget delete [<package_name> <package_version>] 
    [--help] [--source] [--non-interactive] 
    [--api-key] [--force-english-output] [--verbosity] [--config-file]`

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

`--verbosity <LEVEL>`

在输出中显示此数量的详细信息。 级别可以是 `normal`、`quiet` 或 `detailed`。

`--config-file <FILE>`

NuGet 配置文件专门用于此命令，它替换了由标准配置文件发现和链接过程找到的其他配置文件。 路径可以是绝对的，也可以是相对的。
有关配置文件的详细信息，请参阅 [Configuring NuGet Behavior](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)（配置 NuGet 行为）。

## <a name="examples"></a>示例

删除包 MyPackage 的 1.0 版：

`dotnet nuget delete MyPackage 1.0` 

删除包 MyPackage 的 1.0 版（不提示用户需要凭据或其他输入）：

`dotnet nuget delete MyPackage 1.0 --non-interactive`

删除包 MyPackage 的 1.0 版（指定自定义配置文件 ./config/My.Config）：

`dotnet nuget delete MyPackage 1.0 --config-file ./config/My.Config`

删除包 MyPackage 的 1.0 版（包括最大详细级别）：

`dotnet nuget delete MyPackage 1.0 --verbosity detailed`

