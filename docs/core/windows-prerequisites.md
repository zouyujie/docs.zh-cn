---
title: "Windows 上 .NET Core 的先决条件 | Microsoft Docs"
description: "了解在 Windows 计算机上开发和运行 .NET Core 应用程序所需的依赖项。"
keywords: ".NET Core、Windows、先决条件、依赖项、Visual Studio"
author: mairaw
ms.author: mairaw
ms.date: 01/05/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: e374b924bf78d62227cb9607641130dfd9128186
ms.openlocfilehash: 6383a0ce253f6f7000ed8a81b29b9e1d58914acc
ms.lasthandoff: 03/06/2017

---

# <a name="prerequisites-for-net-core-on-windows"></a>Windows 上 .NET Core 的先决条件

本文展示了在 Windows 计算机上部署和运行 .NET Core 应用程序并使用 Visual Studio 进行开发时所需的依赖项。

## <a name="supported-windows-versions"></a>受支持的 Windows 版本

以下 Windows 版本均支持 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10
* Windows Server 2008 R2 SP1（完全服务器或服务器核心）
* Windows Server 2012 SP1（完全服务器或服务器核心）
* Windows Server 2012 R2 SP1（完全服务器或服务器核心）
* Windows Server 2016（完全服务器、服务器核心或 Nano Server）

可以在 [.NET Core 1.0.0 发行说明](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md)中查看完整的[受支持的操作系统](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md#rtm-platform-support)集。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

在早于 Windows 10 和 Windows Server 2016 的 Windows 版本上运行 .NET Core 时，需要 Visual C++ Redistributable。 若使用 .NET Core 安装程序，将自动安装此依赖项。 但是，如果通过[安装程序脚本](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-install-script)安装 .NET Core 或部署自包含的 .NET Core 应用程序，则需要手动安装 [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)。

> [!NOTE]
> <em>仅适用于 Windows 7 和 Windows Server 2008 计算机：</em><br>
> 确保 Windows 安装是最新版本，并且包括通过 Windows 更新安装的修补程序 [KB2533623](https://support.microsoft.com/en-us/kb/2533623)。

## <a name="prerequisites-with-visual-studio-2017"></a>Visual Studio 2017 的先决条件

可以使用所选择的任何编辑器，使用 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要在集成的开发环境中的 Windows 上开发 .NET Core 应用程序，可以使用 [Visual Studio 2017](#visual-studio-2017)。

若要使用 Visual Studio 2017 开发 .NET Core 应用，必须选择将 **.NET Core 跨平台开发**工具集（在“其他工具集”部分中）与最新版本的 Visual Studio 一并安装。

Visual Studio 2017 有不同的版本。 可以免费下载 [Visual Studio Community 2017](https://www.visualstudio.com/vs/visual-studio-2017/#downloadvs) 并开始使用。  若要了解有关 Visual Studio 安装过程的详细信息，请参阅[安装 Visual Studo 2017](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio)。

在[发行说明](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes)中可以详细了解 Visual Studio 2017 中的更改。

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546
