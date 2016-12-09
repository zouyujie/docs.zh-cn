---
title: ".NET Core 系统必备组件（预览版 3 工具）"
description: ".NET Core 系统必备组件（预览版 3 工具）"
keywords: .NET, .NET Core
author: billwagner
ms.author: wiwagn
ms.date: 09/15/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: 07b62bd7163193eff8dc8f61fda7a45a924bba2b
ms.openlocfilehash: ee4ccba7c06f0a7f67e3fe59c885febf895235fd

---

# <a name="prerequisites-for-windows-development-preview-3-tooling"></a>Windows 开发的先决条件（预览版 3 工具）

使用 Visual Studio 在 Windows 上进行 .NET Core 开发需要：

* Windows 客户端或操作系统的受支持版本。
* Visual Studio 2017 RC 或更高版本
* .NET Core 工具预览版 3

## <a name="supported-windows-versions"></a>受支持的 Windows 版本

以下 Windows 版本均支持 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10
* Windows Server 2008 R2 SP1（完全服务器或服务器核心）
* Windows Server 2012 SP1（完全服务器或服务器核心）
* Windows Server 2012 R2 SP1（完全服务器或服务器核心）
* Windows Server 2016（完全服务器、服务器核心或 Nano Server）

可以在 [.NET Core 发行说明](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md)中查看完整的 [受支持的操作系统](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md#rtm-platform-support)集。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

在 Windows 上运行时，.NET Core 需要 VC++ Redistributable。 该组件可通过 .NET Core 安装程序安装。 如果要使用安装程序脚本 (`dotnet-install.ps1`) 安装 .NET Core，需要手动安装 Visual C++ Redistributable。 

Visual C++ Redistributable 版本因 Windows 版本而异。

* Windows 10
    * [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
* Windows 7+（不是 Windows 10）
    * 请确保 Windows 安装为最新版本，并且包括通过 Windows 更新安装的修补程序 [KB2533623](https://support.microsoft.com/en-us/kb/2533623)。
    * [通用 CRT 更新](https://www.microsoft.com/en-us/download/details.aspx?id=48234)（可在 [此博客文章](https://blogs.msdn.microsoft.com/vcblog/2015/03/03/introducing-the-universal-crt/)的“什么是通用 CRT”中了解详细信息）

## <a name="visual-studio"></a>Visual Studio

通过 .NET Core 命令行工具可以使用任何编辑器开发 .NET Core 应用，但如果想要使用 Visual Studio 和 .NET Core 工具预览版 3，则需要 Visual Studio 2017 RC 或更高版本。 [Visual Studio Community 2017 RC](https://www.visualstudio.com/vs/visual-studio-2017-rc/)可免费下载。 

验证是否正在运行 Visual Studio 2017 RC：

* 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
* 在“关于 Microsoft Visual Studio”对话框中，版本号应该是 15.0.25831.1 或更高版本。

在[发行说明](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes)中可以了解关于 Visual Studio 2017 RC 中更改的详细信息。

请确保在安装过程中已安装“.NET Core and Docker（预览版）”工作负荷。 如果没有执行此操作，可再次运行安装程序，然后选择它。



<!--HONumber=Nov16_HO3-->


