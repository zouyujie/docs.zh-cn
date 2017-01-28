---
title: "为服务器应用选择 .NET Core 或 .NET Framework"
description: "关于用户在 .NET 中生成服务器应用时应考虑使用哪种版本的 .NET 的指南。"
keywords: .NET, .NET Core, .NET Framework
author: cartermp
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 155553e4-89a2-418d-be88-4e75f6c3cc69
translationtype: Human Translation
ms.sourcegitcommit: 572bec82e08d6b47a188e51964c8c2f440fa471c
ms.openlocfilehash: e23514daacb34739b26b7a31afea2ccb30296e79

---

# <a name="choosing-between-net-core-and-net-framework-for-server-apps"></a>为服务器应用选择 .NET Core 或 .NET Framework

有两种支持的运行时可用于通过 NET Framework 和 .NET Core 生成服务器端应用程序。 这两者共享了大量相同的 .NET 平台组件，用户可在它们之间共享代码。 但两者之间存在根本的差异，可根据需要实现的目标进行选择。  本文介绍了在何种情况下进行选择。

在以下情况，应该为服务器应用程序选择使用 .NET Core：

* 用户有跨平台需求。
* 用户正在面向微服务。
* 用户正在使用 Docker 容器。
* 用户需要高性能和可扩展的系统。
* 用户根据应用程序需要并排 .NET 版本。

在以下情况，应该为服务器应用程序选择使用 .NET Framework ：

* 应用程序当前正在使用 .NET Framework（建议扩展而不是迁移）
* 用户需要使用不可用于 .NET Core 的第三方 .NET 库或 NuGet 包。
* 用户需要使用不可用于 .NET Core 的 .NET 技术。
* 用户需要使用不支持 .NET Core 的平台。

## <a name="when-to-choose-net-core"></a>选择 .NET Core 的情形

以下是对前面提到的选择 .NET Core 的原因的更详细的说明。

### <a name="cross-platform-needs"></a>跨平台需求

如果你的目标是拥有能跨平台（Windows、Linux 和 macOS）运行的应用程序（Web/服务），.NET Core 无疑是最佳选择。

.NET Core 作为开发工作站还支持前面提到的操作系统。 Visual Studio 提供用于 Windows 的集成开发环境 (IDE)。  你还可以在 macOS、Linux 和 Windows 上使用 Visual Studio Code，它们完全支持 .NET Core，包括 IntelliSense 和调试。 此外，你还可以使用大多数第三方编辑器（如 Sublime、Emacs 和 VI）面向 .NET Core，并使用开源 [Omnisharp](http://www.omnisharp.net/) 项目获取编辑器 IntelliSense。 也可以不使用任何代码编辑器，直接使用适用于所有支持平台的 .NET Core 命令行工具。

### <a name="microservices-architecture"></a>微服务体系结构

如果你要选择使用面向微服务的系统（该系统由多个独立的、可动态伸缩的、有状态或无状态的微服务组成），.NET Core 将是最佳选择。 .NET Core 是轻型平台，其 API 图面可最小化到微服务范围。 微服务体系结构还允许混合跨服务边界的技术，从而逐渐接受新微服务的 .NET Core，这些新的微服务与使用 .NET Framework、Java、Ruby 或其他整体化技术开发的其他微服务或服务结合使用。

可供使用的基础结构平台有很多。 对于大型和复杂微服务系统，可以使用 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)。 对于无状态的微服务，还可以使用其他产品（如 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)）。 基于 Docker 的微服务备选方案也适合于任何一种微服务方法，将在下一部分中进行说明。 所有这些平台都支持 .NET Core，是托管微服务的理想选择。

### <a name="containers"></a>容器

虽然容器通常与微服务体系结构结合使用，但是也可用于容器化遵循任何体系结构模式的 Web 应用或服务。 虽然能够将 .NET Framework 用于 Windows 容器，但 .NET Core的模块化和轻型性质使之成为容器的最佳选择。  在创建和部署时容器时，使用 .NET Core 时容器的映像大小要远小于使用 .NET Framework 时的大小。  例如，因为它是跨平台的，所以可以将服务器应用部署到 Linux Docker 容器。

然后，可以在自己的 Linux 或 Windows 基础结构中托管 Docker 容器，或使用云服务（例如 [Azure 容器服务](https://azure.microsoft.com/services/container-service/)），在云中管理、协调和缩放基于容器的应用程序。

### <a name="a-need-for-high-performance-and-scalable-systems"></a>需要高性能和可扩展的系统

如果系统需要最佳的性能和可伸缩性，.NET Core 和 ASP.NET Core 是最佳的选择。 ASP.NET Core 的性能比 ASP.NET 高出 10 倍，领先于微服务的其他行业技术（例如 Java servlets、Go 和 node.js）。

这一点对微服务体系结构尤为重要，你可以运行数百个微服务。 通过使用 ASP.NET Core，能够大大减少运行系统所用的服务器/VM，最终节省基础结构和托管的费用。

### <a name="a-need-for-side-by-side-of-net-versions-per-application-level"></a>需要按应用程序级别选择并行的 .NET 版本

如果想要在 .NET 的不同版本的框架上安装具有依赖项的应用程序，需要使用提供百分百并行的 .NET Core。 由于在同一台计算机上可轻松地并行安装不同版本的 .NET Core，用户可在同一台计算机上拥有多个服务，每个服务都在自己版本的 .NET Core 上，从而消除了风险并节约了应用程序升级和 IT 运营方面的资金。

## <a name="when-to-choose-net-framework"></a>选择 .NET Framework 的情形

虽然 .NET Core 为新的应用程序和应用程序模式带来的好处很明显，但在很多现有情况下仍然会选择 .NET Framework，因此不会将所有服务器应用程序的 .NET Framework 将替换为 .NET Core。

### <a name="current-net-framework-applications"></a>现有的 .NET Framework 应用程序

在大多数情况下，不需要将现有应用程序迁移到 .NET Core。 相反，若要扩展现有的应用程序（例如，在 ASP.NET Core 中写入新的 Web 服务），建议使用 .NET Core。

### <a name="a-need-to-use-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>需要使用不可用于 .NET Core 的第三方 .NET 库或 NuGet 包

库可以快速接受 .NET Standard，这样可跨各种 .NET 版本（包括 .NET Core）共享代码。 如使用 .NET Standard 2.0，上述操作将更简单，因为 .NET Core API 图面会明显变大，.NET Core 应用程序可直接使用现有的 .NET Framework 库。 但此转换不会即时性生效，因此，我们建议在选择其中的一种方法前，请检查应用程序所需的特定库。

### <a name="a-need-to-use-net-technologies-not-available-for-net-core"></a>需要使用不可用于 .NET Core 的 .NET 技术

某些 .NET Framework 技术在 .NET Core 中不可用。 虽然某些技术将在更高版本的 .NET Core 中可用，但其他技术不会应用于 .NET Core 面向的新应用程序模式，因此可能永远不可用。 以下列表显示无法在 .NET Core 1.0 中找到的最常见技术：

* ASP.NET Web 窗体应用程序：ASP.NET Web 窗体上仅在 .NET Framework 中可用，因此该情况下不能使用 ASP.NET Core /.NET Core 。 目前没有将 ASP.NET Web 窗体引入 .NET Core 的计划。

* ASP.NET 网页应用程序：ASP.NET Core 1.0 中不包含 ASP.NET 网页，但计划将在未来版本中包括此项，详情请查看 [.NET Core 路线图](https://github.com/aspnet/Home/wiki/Roadmap)。

* ASP.NET SignalR 服务器/客户端实现。 在 .NET Core 1.0 发布时间范围内（2016 年 6 月），ASP.NET Core 不提供 ASP.NET SignalR（包括客户端和服务器），但计划将在未来版本中包括此项，详情请查看 [.NET Core 路线图](https://github.com/aspnet/Home/wiki/Roadmap)。 [服务器端](https://github.com/aspnet/SignalR-Server)和[客户端库](https://github.com/aspnet/SignalR-Client-Net) GitHub 存储库上的预览状态可用。

* WCF 服务的实现。 虽然 [WCF 客户端库](https://github.com/dotnet/wcf)可从 .NET Core 使用 WCF 服务，但从 2016 年 6 月起，WCF 服务器实现只能在 .NET Framework 上可用 。 这种情况虽然不属于 .NET Core 当前计划，但将来会考虑这点。

* 工作流相关的服务：Windows Workflow Foundation (WF)、工作流服务（WCF + 单个服务中的 WF）和 WCF 数据服务（以前称为“ADO.NET 数据服务”）仅在 .NET Framework 上可用，尚未计划将其引入 .NET Core。

* 语言支持：Visual Basic 和 F # 目前没有工具支持 .NET Core，但 Visual Studio 2017 和更高版本的 Visual Studio 将支持这两种语言。

除了正式的路线图，还有其他框架植入 .NET Core - 若要查看完整列表，请查看标记为[端口到核心](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core)的 CoreFX 问题。 请注意，此列表不代表 Microsoft 承诺将这些组件引入 .NET Core — 而只是从社区搜集达成此项的意愿。 尽管如此，如果对以上所列的任何组件感兴趣，请参与 GitHub 上的讨论，发表你的看法。 如果认为丢失了某些内容，请[在 CoreFX 存储库中提出新的问题](https://github.com/dotnet/corefx/issues/new)。

### <a name="a-need-to-use-a-platform-that-doesnt-support-net-core"></a>需要使用不支持 .NET Core 的平台

某些 Microsoft 或第三方平台不支持 .NET Core。 例如，某些 Azure 服务（如 Service Fabric Stateful Reliable Services 和 Service Fabric Reliable Actors）需要 .NET Framework。 某些其他服务提供尚不可用于 .NET Core 的 SDK。 这只是过渡情况，因为所有 Azure 服务都将使用 .NET Core。 在此期间，可用始终使用等效的 REST API 取代客户端 SDK。

## <a name="further-resources"></a>其他资源

* [.NET Core 指南](../core/index.md)
* [从 .NET Framework 移植到 .NET Core](../core/porting/index.md)
* [Docker 上的 .NET Framework 指南](../framework/index.md)
* [.NET 组件概述](components.md)



<!--HONumber=Jan17_HO3-->


