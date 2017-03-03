---
title: "dotnet-nuget-push 命令 | Microsoft Docs"
description: "dotnet-nuget-push 命令将包推送到服务器，并将其发布。"
keywords: "dotnet-nuget-push, CLI, CLI 命令, .NET Core"
author: karann-msft
ms.author: mairaw
ms.date: 11/11/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f54d9adf-94f8-41cc-bb52-42f7ca3be6ff
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: dcc89fd24e23e624c4bcf90a8200b4e655af6dd6
ms.lasthandoff: 01/21/2017

---

#<a name="dotnet-nuget-push"></a>dotnet-nuget-push

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>名称 
`dotnet-nuget-push` - 将包推送到服务器，并将其发布。 

## <a name="synopsis"></a>摘要

`dotnet nuget push [<package>] [--help] [--source] [--symbols-source] 
    [--timeout] [--api-key] [--symbol-api-key] [--disable-buffering] [--no-symbols] 
    [--force-english-output] [--config-file] [--verbosity]`

## <a name="description"></a>描述

`dotnet nuget push` 将包推送到服务器，并将其发布。 push 命令使用在系统的 NuGet 配置文件或配置文件链中找到的服务器和凭据详细信息。 有关配置文件的详细信息，请参阅 [Configuring NuGet Behavior](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)（配置 NuGet 行为）。 通过加载 %AppData%\NuGet\NuGet.config (Windows) 或 $HOME/.local/share (Linux/macOS) 获得 NuGet 的默认配置，然后加载任意 nuget.config 或 .nuget\nuget.config，从驱动器的根目录开始，并在当前目录中结束。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-s|--source <SOURCE>`

指定服务器 URL。 除非在 NuGet 配置文件中设置了 DefaultPushSource 配置值，否则此选项是必需的。

`--symbols-source <SOURCE>`

指定符号服务器 URL。

`-t|--timeout <TIMEOUT>`

指定推送到服务器的超时（秒）。 默认值为 300 秒（5 分钟）。 指定 0 也将给出此默认值。

`-k|--api-key <API_KEY>`

服务器的 API 密钥。

`--symbol-api-key <API_KEY>`

符号服务器的 API 密钥。

`-d|--disable-buffering`

当推送到 HTTP(S) 服务器以减少内存使用率时，禁用缓冲。

`-n|--no-symbols`

不推送符号（即使存在）。

`--force-english-output`

强制所有记录的输出以英语显示。 除了在非英语计算机上生成英语输出的灵活性，此选项还提供的跨平台的一致性，对自动化工具而言它是一项有用功能，它能擦除文本的日志。

`--config-file <FILE>`

NuGet 配置文件专门用于此命令，它替换了由标准配置文件发现和链接过程找到的其他配置文件。 路径可以是绝对的，也可以是相对的。
有关配置文件的详细信息，请参阅 [Configuring NuGet Behavior](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)（配置 NuGet 行为）。 

`--verbosity <LEVEL>`

在输出中显示此数量的详细信息。 级别可以是 `normal`、`quiet` 或 `detailed`。

## <a name="examples"></a>示例

将 foo.nupkg 推送到默认推送源（提供 API 密钥）：

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a`

将 foo.nupkg 推送到自定义推送源 `http://customsource`提供 API 密钥）：

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s http://customsource/` 

将 foo.nupkg 推送到默认推送源：

`dotnet nuget push foo.nupkg` 

将 foo.symbols.nupkg 推送到默认符号源：

`dotnet nuget push foo.symbols.nupkg`

将 foo.nupkg 推送到默认推送源（指定 360 秒超时）：

`dotnet nuget push foo.nupkg --timeout 360`

将当前目录中的所有 .nupkg 文件推送到默认推送源：

`dotnet nuget push *.nupkg`

将当前目录中的所有 .nupkg 文件推送到默认推送源（指定自定义配置文件 ./config/My.Config）：

`dotnet nuget push *.nupkg --config-file ./config/My.Config`

将当前目录中的所有 .nupkg 文件推送到默认推送源（包含最大详细级别）：

`dotnet nuget push *.nupkg --verbosity detailed`

