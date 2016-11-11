---
title: ".NET 产品"
description: ".NET 产品"
keywords: ".NET、.NET Core"
author: richlander
manager: wpickett
ms.date: 06/23/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2e38e9d9-8284-46ee-a15f-199adc4f26f4
translationtype: Human Translation
ms.sourcegitcommit: 15c55a87beb64f265a164db918c7721c7690fadf
ms.openlocfilehash: 90deb1903eea6ae1336326ca91f1e7863485dfd1

---

# <a name="net-products"></a>.NET 产品

.NET 是用于生成开发人员产品的一项非常灵活、通用且本质上跨平台的[规范](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)。 它适用于所有最热门的应用类别：桌面、移动、云、游戏和 IoT。

本文档使用了两个略有不同的术语：

- “.NET 产品”- 允许为一个或多个目标平台生成应用。
- “.NET 实现” - 运行时、框架和工具（可以对产品所基于的平台执行“.NET 代码”）的某种组合。

## <a name="product-categories"></a>产品类别

.NET 产品可用于以下每种产品类别。

### <a name="desktop"></a>桌面

可以生成用于 Windowsd 和 macOS 的桌面应用。

- [通用 Windows 应用](https://developer.microsoft.com/windows)（含 [.NET Native](#net-native)）
- 用于 Windows 的 [Windows Presentation Foundation (WPF)](https://msdn.microsoft.com/library/ms754130.aspx)（含 [.NET Framework](#net-framework)）
- 用于 Windows 的 [Windows 窗体](https://msdn.microsoft.com/library/dd30h2yb.aspx)（含 [.NET Framework](#net-framework)）
- 用于 macOS 的 Cocoa（含 [Xamarin](#xamarin-sdk)）
- 用于跨平台桌面的 [Electron](http://electron.atom.io/)（含 [electron-edge](https://github.com/kexplo/electron-edge)）

### <a name="games"></a>游戏

可以生成用于诸多桌面、移动、控制台和虚拟/增强现实设备的游戏。

- 带 [Mono](#mono) 的 [CRYENGINE](http://docs.cryengine.com/display/CEPROG/CE%23+Programming)
- 带 [Mono](#mono) 的 [MonoGame](http://www.monogame.net/documentation/?page=main)
- 带 [Mono](#mono) 的 [Unity](http://docs.unity3d.com/Manual/index.html)

### <a name="iot"></a>IoT

可以生成用于 Windows 10 IoT Core 的 IoT 应用，包括 Raspberry Pi 2/3。

- [Windows 10 IoT 核心版](https://developer.microsoft.com/windows/iot)（含 [.NET Native](#net-native)）

### <a name="mobile"></a>移动电话

可以生成用于 iOS、Android 和 Windows 的移动应用。

- 带 [Xamarin](#xamarin-sdk) 的 iOS 应用
- 带 [Xamarin](#xamarin-sdk) 的 Android 应用
- [通用 Windows 应用](https://developer.microsoft.com/windows)（含 [.NET Native](#net-native)）

### <a name="web-and-cloud"></a>Web 和云

可以生成用于 Windows 和 Linux 的 Web 和云应用。

- 用于 Windows 的 [ASP.NET](http://www.asp.net/)（含 [.NET Framework](#net-framework)）
- 用于 Windows、macOS 和 Linux 的 [ASP.NET Core](http://docs.asp.net/)（含 [.NET Core](#net-core)）

## <a name="net-implementations"></a>.NET 实现

下方按字母顺序列出了主要的商业和开放源 .NET 实现。

### <a name="net-core"></a>.NET 核心

.NET Core 用于生成设备、Web、云和嵌入式/IoT 应用。 它为[开放源](https://github.com/dotnet/core)并且跨平台，支持 Windows、macOS 和 Linux。 [ASP.NET Core](http://docs.asp.net/) 是 .NET Core 的最常用工作负荷。 可以使用它来生成用于本地和云部署的 Web 应用和服务。 .NET Core 还可用于生成工具、实用工具和云辅助应用。

- 了解 [.NET Core](../core/index.md)
- 了解 [ASP.NET Core](http://docs.asp.net/)
- [下载 .NET Core](http://dot.net/core)

下方列出了 .NET Core 的主要特征：

**跨平台** - .NET Core 支持三种操作系统系列：Linux、Windows 和 macOS。 .NET Core 应用默认为跨平台。 可以编写无需修改即可跨所支持操作系统运行的应用和库。

**开放源** - [.NET Core](https://github.com/dotnet/core) 在 GitHub 上可用，并已由 [MIT](https://github.com/dotnet/coreclr/blob/master/LICENSE.TXT) 和 [Apache 2](https://github.com/dotnet/roslyn/blob/master/License.txt) 许可证授权（授权针对每个组件记进行）。 文档由 [CC-BY](https://github.com/dotnet/docs/blob/master/license.txt) 授权。 此外，.NET Core 还利用 [.NET Core 发行说明](https://github.com/dotnet/core/releases)中列出的一组重要开放源行业依赖项。 

**自然购置** - NET Core 分布在多个窗体中，符合特定的开发人员需求。 可以通过 [.NET Core SDK](https://dot.net/core) 安装程序（或压缩），或者通过特定于操作系统的程序包管理器（如 APT 和 Yum）获取 .NET Core。 可在 Docker 中心获取[官方 .NET Core Docker 映像](https://hub.docker.com/r/microsoft/dotnet/)。 可在 [NuGet](http://www.nuget.org/) 上获取更高级别的框架库和更大的 .NET 库生态系统。 

**模块式平台** - .NET Core 使用模块式设计构建而成，允许应用程序仅包括所需的 .NET Core 库和依赖项。 每个应用程序可自己选择 .NET Core 版本控制，避免与共享组件发生冲突。 此方法符合使用 Docker 等容器技术开发软件的趋势。

### <a name="net-framework"></a>.NET Framework

.NET Framework 用于生成面向 Windows 和 Windows Server 的应用。 可使用它来生成具有 Windows Presentation Framework (WPF) 和 Windows 窗体的丰富用户界面。 还支持生成具有 ASP.NET Web 窗体、ASP.NET MVC 和 Windows Communication Framework (WCF) 的服务器应用。 Visual Studio 提供丰富的 .NET Framework 设计器体验，让生成客户端和服务器应用变得简单。 它是编写 Windows 应用的最佳选择。

- 了解 [.NET Framework](https://msdn.microsoft.com/library/w0x726c2.aspx)
- [下载 .NET Framework](https://dot.net)

[Windows 窗体](https://msdn.microsoft.com/library/dd30h2yb.aspx)允许以优于其他任何技术的速度生成“资料表单”桌面 UI。 它使用允许拖放 UI 和非 UI 控件的设计器，将大多数开发任务归结到单个笔势和概念模型。

[Windows Presentation Foundation (WPF)](https://msdn.microsoft.com/library/ms754130.aspx) 以 [XAML](https://msdn.microsoft.com/library/ms752059.aspx) 标记语言描述 UI，以此来分隔代码和 UI 问题。 WPF 非常灵活，常用于需要更复杂用户模型或更典雅外观的 UI。

[Windows Communication Foundation (WCF)](https://msdn.microsoft.com/library/ms731082.aspx) 是一组用于 SOAP Web 服务的库。 它允许创建可以使用各种数据格式通过多种支持的协议进行通信，并且可以托管于所选任何进程中的服务。 这引出了 WCF 的一个主要特性：服务不会关联到任何特定的托管策略或方法。

[ASP.NET](http://www.asp.net/) 是一种 Web 框架。 它具有几个不同部分，可用于生成高性能的现代 Web 应用程序。 

- [ASP.NET Web 窗体](http://www.asp.net/web-forms) 允许使用能够拖放 Web 控件的设计器，以优于其他大多数 Web 技术的速度生成“资料表单”UI。 
- [ASP.NET MVC](http://www.asp.net/mvc) 允许更好地控制从 HTTP 层到用户界面的整个 Web 管道。 
- [ASP.NET WebAPI](http://www.asp.net/web-api) 是基于约定的框架，用于创建 REST 服务。 
- [SignalR](http://www.asp.net/signalr) 允许使用 [WebSocket](https://en.wikipedia.org/wiki/WebSocket) 协议向 Web 应用程序提供基于推送的通信。

### <a name="net-native"></a>.NET Native

.NET Native 是一套用于 .NET Core 的本机生成工具。 .NET Native 是一种预先编译 (AOT) 工具链，通过将 IL 字节代码编译为本机计算机代码来生成本机应用程序。 这意味着生成的二进制文件就是操作系统的执行对象；不存在任何运行的 JIT 和运行时编译。 这会产生更好的启动性能以及某些安全优势。

.NET Native 主要由 .NET [通用 Windows 平台 (UWP)](https://msdn.microsoft.com/library/windows/apps/dn726767.aspx) 应用程序使用。

### <a name="mono"></a>Mono

[Mono](http://www.mono-project.com/docs/about-mono/) 是 .NET 最初的开放源和跨平台实现，源自社区 [Mono 项目](http://mono-project.com)。 现由 Microsoft 提供赞助。 可以将其视作 .NET Framework 的开放和跨平台版本。 其 API 跟踪 .NET Framework，而不是 .NET Core 的进度。

Mono 由多个组件构成：

**C# 编译器** - Mono 的 C# 编译器是对 C# 6 功能的完善。

**Mono 运行时** - 该运行时实现 ECMA 公共语言基础结构 (CLI)。 该运行时提供实时 (JIT) 编译器、预先编译器 (AOT)、库加载器、垃圾回收器、线程处理系统和互操作性功能。

**基类库** - Mono 平台提供一套全面的类，用于提供生成应用程序的坚实基础。 这些类与 Microsoft 的 .Net Framework 类兼容。

**Mono 类库** - Mono 还提供许多优于 .NET Framework 所提供的基类库的类。 这些类提供非常有用（尤其是生成 Linux 应用程序时）的附加功能。 例如用于 Gtk+、Zip 文件、LDAP、OpenGL、Cairo、POSIX 等的类。

### <a name="xamarin-sdk"></a>Xamarin SDK

[Xamarin SDK](http://open.xamarin.com) 用于生成主要面向 Apple 和 Google 生态系统的本机移动应用和设备应用。 它基于 Mono，并且是使用 MIT 许可证的开放源。 可用于生成面向手机、平板电脑和手表的 iOS 和 Android 应用。 [Xamarin.Forms](https://www.xamarin.com/forms) 是一种跨 Apple、Google 和 Windows 应用编写可重用 UI 的常用方式。

- 了解 [Xamarin SDK](https://developer.xamarin.com/)
- [下载 Xamarin](https://www.xamarin.com/platform)



<!--HONumber=Nov16_HO1-->


