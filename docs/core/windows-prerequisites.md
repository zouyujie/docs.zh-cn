---
title: ".NET Core 系统必备组件"
description: ".NET Core 系统必备组件"
keywords: .NET, .NET Core
author: billwagner
manager: wpickett
ms.date: 09/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: 130b94a745b0e3222e205d8af26194239130ec9c
ms.openlocfilehash: 04018ec65272745ef98a2a96eb30009bcf44cb2e

---

# <a name="prerequisites-for-windows-development"></a>Windows 开发的先决条件

使用 Visual Studio 在 Windows 上进行 .NET Core 开发需要：

* Windows 客户端或操作系统的受支持版本。
* Visual Studio 2015 Update 3.3 或更高版本
* 适用于 Visual Studio 的 NuGet Manager 扩展
* .NET Core Tooling Preview 2

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

需要使用 Visual Studio 2015 开发 .NET Core 应用。 可以免费下载 [Visual Studio Community 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs)。 

验证是否可以运行 [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx)：

* 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
* 在“关于 Microsoft Visual Studio”对话框中，版本号应该是 14.0.25424.00 或更高版本，且包括“Update 3”。
* 如果没有 Update 3，首先需要下载并安装 [Visual Studio 2015 Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)。
* 如果具有 Update 3，但版本数小于 14.0.25424.00，则需要下载并安装 [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx)。

可以在[发行说明](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)中了解关于 Update 3 中更改的详细信息。

## <a name="nuget-manager-extension-for-visual-studio"></a>适用于 Visual Studio 的 NuGet Manager 扩展

NuGet 是适用于 Microsoft 开发平台（包括 .NET Core）的包管理器。 需要 [NuGet 3.5.0](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) 或更高版本来生成 .NET Core 应用。

## <a name="net-core-tools-for-visual-studio-2015"></a>适用于 Visual Studio 2015 的 .NET Core 工具

下载并安装 [.NET Core 1.0.1 - VS 2015 Tooling Preview 2] [SDK]。 

.NET Core Tooling 包将安装适用于 Visual Studio 2015 的 .NET Core、项目模板和其他工具。

> [!NOTE]
目前，无法下载 [.NET Core 1.0.1 - VS 2015 Tooling Preview 2] [SDK] 的脱机安装程序。 而必须下载[常规引导程序] [SDK] 并通过命令行选项（如，`/layout c:\path`）运行它，以获取脱机布局。 之后，它可用作脱机安装程序：只需从本地路径运行可执行文件即可。 请注意，因为它是一个完整布局，此过程将下载所有支持语言的所有包，大小约为 1 GB。

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546



<!--HONumber=Nov16_HO1-->


