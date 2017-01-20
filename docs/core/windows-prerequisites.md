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
ms.sourcegitcommit: c81b3b4785bff3bf8963e0ba1b917a5f797099ff
ms.openlocfilehash: b5c088da7d1155414a08995ae0d72154af891190

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

## <a name="prerequisites-with-visual-studio"></a>Visual Studio 的先决条件

可以使用所选择的任何编辑器，使用 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要使用 Visual Studio 在 Windows 上开发 .NET Core 应用程序，则可以使用这两个版本：

* [Visual Studio 2015](#visual-studio-2015)
* [Visual Studio 2017 RC](#visual-studio-2017-rc)

使用 Visual Studio 2015 创建的项目默认基于 project.json，而使用 Visual Studio 2017 RC 创建的项目则始终基于 MSBuild。 有关格式更改的详细信息，请参阅[有关更改的高级别概述](./preview3/tools/layering.md)。

### <a name="visual-studio-2015"></a>Visual Studio 2015

若要使用 Visual Studio 2015 开发 .NET Core 应用，则需要：

* Visual Studio 2015 Update 3.3 或更高版本。

   Visual Studio 2015 有不同的[版本](https://www.visualstudio.com/vs/compare)。 可以免费下载 [Visual Studio Community 2015](https://www.visualstudio.com/downloads/) 并开始使用。 

   为了验证是否可以运行 [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx)，请执行以下操作：

   * 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
   * 在“关于 Microsoft Visual Studio”对话框中，版本号应该是 14.0.25424.00 或更高版本，且包括“Update 3”。
   * 如果没有 Update 3，首先需要下载并安装 [Visual Studio 2015 Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)。
   * 如果具有 Update 3，但版本数小于 14.0.25424.00，则需要下载并安装 [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx)。

   可以在[发行说明](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs)中了解关于 Update 3 中更改的详细信息。

* 适用于 Visual Studio 的 NuGet Manager 扩展

   NuGet 是适用于 Microsoft 开发平台（包括 .NET Core）的包管理器。 需要 [NuGet 3.5.0-beta](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) 或更高版本来生成 .NET Core 应用。

* .NET Core Tooling Preview 2

   下载并安装 [.NET Core 1.0.1 - VS 2015 Tooling Preview 2][sdk]。 

   .NET Core Tooling 包将安装适用于 Visual Studio 2015 的 .NET Core、项目模板和其他工具。

   > [!NOTE]
   > 目前，无法下载 [.NET Core 1.0.1 - VS 2015 Tooling Preview 2][sdk] 的脱机安装程序。 而必须下载[常规引导程序][sdk]并通过命令行选项（如，`/layout c:\path`）运行它，以获取脱机布局。 之后，它可用作脱机安装程序：只需从本地路径运行可执行文件即可。 请注意，因为它是一个完整布局，此过程将下载所有支持语言的所有包，大小约为 1 GB。

### <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

若要使用 Visual Studio 2017 RC 开发 .NET Core 应用，则需要安装最新版本的 Visual Studio RC，并选择“.NET Core 和 Docker (预览)”工作负荷。 

Visual Studio 2017 RC 有不同的版本。 可以免费下载 [Visual Studio Community 2017 RC](https://www.visualstudio.com/vs/visual-studio-2017-rc/#downloadvs) 并开始使用。  若要了解有关 Visual Studio 安装过程的详细信息，请参阅[安装 Visual Studo 2017 RC](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio)。

若要验证是否运行的是最新版本的 Visual Studio 2017 RC，请执行以下操作：

* 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
* 在“关于 Microsoft Visual Studio”对话框中，版本号应该是 15.0.26020.0 或更高版本。

在[发行说明](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes)中可以了解关于 Visual Studio 2017 RC 中更改的详细信息。

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546



<!--HONumber=Jan17_HO3-->


