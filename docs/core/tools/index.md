---
title: ".NET Core 命令行接口 (CLI) 工具 | Microsoft Docs"
description: "命令行接口 (CLI) 的定义及其主要功能的概述"
keywords: "CLI, CLI 工具, .NET, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 7c5eee9f-d873-4224-8f5f-ed83df329a59
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 4e3137d8506342662d145481d5e9fde1d53b9ba3
ms.lasthandoff: 03/07/2017

---

# <a name="net-core-command-line-interface-tools-net-core-sdk-10-tools"></a>.NET Core 命令行接口工具（.NET Core SDK 1.0 工具）

.NET Core 命令行接口 (CLI) 工具是用于开发 .NET Core 应用程序的新型基础性跨平台工具链。 “基础性”在于它是可以在其中生成其他更高级别工具（如集成开发环境 (IDE)、编辑器和生成 orchestrator）的主层。 

此外，默认情况下，它是跨平台的，每个受支持平台上的外围应用都相同。 这意味着，如果了解如何使用此工具，便可以在任何受支持的平台以相同方式使用它。 

## <a name="installation"></a>安装
与任何工具一样，首先应将工具安装到计算机上。 根据具体情况，可以使用本机安装程序安装 CLI 或使用 shell 脚本安装。

本机安装程序主要用于开发人员的计算机。 可以使用所有受支持的平台的本机安装机制发布 CLI，例如 Ubuntu 上的 DEB 或 Windows 上的 MSI 包。 这些安装程序将根据需要为用户安装并设置环境，以便在安装完成后可立即使用 CLI。 但是，这些安装程序也需要对计算机的管理权限。 有关安装说明信息，请参阅 [.NET Core 入门页](https://aka.ms/dotnetcoregs)。

另一方面，安装脚本不需要管理权限。 但是，它们也不会在计算机上安装任何系统必备组件；需要手动安装所有系统必备组件。 这些脚本主要用于设置生成服务器或希望安装工具但没有管理权限的情况（请务必注意上述系统必备组件注意事项）。 可以在[安装脚本引用主题](dotnet-install-script.md)中找到详细信息。 如果对如何在持续集成 (CI) 生成服务器上设置 CLI 感兴趣，可以查看 [CI 服务器的 CLI](using-ci-with-cli.md) 主题。 

默认情况下，CLI 将以并行 (SxS) 方式安装。 这意味着多个版本的 CLI 工具在任何给定时间内可在一台计算机上共存。 有关如何使用正确版本的详细信息，请参阅[驱动程序](#driver)部分。 

### <a name="what-commands-come-in-the-box"></a>框中有哪些命令？
默认安装以下命令：

* [new](dotnet-new.md)
* [migrate](dotnet-migrate.md)
* [restore](dotnet-restore.md)
* [run](dotnet-run.md)
* [build](dotnet-build.md)
* [test](dotnet-test.md)
* [publish](dotnet-publish.md)
* [pack](dotnet-pack.md)

此外，还有一种方法可以基于每个项目导入更多命令并添加自己的命令。 有关详细信息，请参阅[扩展性部分](#extensibility)。 

## <a name="working-with-the-cli"></a>使用 CLI

开始了解更多详细信息之前，我们来看看从 10,000 英尺的视图中使用 CLI 的情形。 以下示例利用 CLI 标准安装中的多个命令来初始化新的简单控制台应用程序、还原依赖项、生成应用程序，然后运行该应用程序。 

```console
dotnet new console
dotnet restore
dotnet build --output /stuff
dotnet /stuff/new.dll
```

如上例中所示，其中有一种使用 CLI 工具的模式。 在该模式中，我们可以确定每个命令的三大主要部分：

1. [驱动程序（“dotnet”）](#driver)
2. [命令或“谓词”](#the-verb)
3. [命令参数](#the-arguments)

### <a name="driver"></a>驱动程序
驱动器名为 [dotnet](dotnet.md)。 这是调用的第一部分。 该驱动程序有以下两项职责：

1. 运行可移植应用
2. 执行谓词

它所执行的职责取决于命令行上指定的内容。 在第一种情况下，需要指定可移植应用 DLL，`dotnet` 将以如下方式运行该 DLL：`dotnet /path/to/your.dll`。 

在第二种情况下，驱动程序将尝试调用指定命令。 这将启动 CLI 命令执行过程。 首先，驱动程序确定所需工具的版本。 可在 [global.json](global-json.md) 文件中使用 `version` 属性指定版本。 如果不可用，驱动程序将查找安装在磁盘上的工具的最新版本并使用该版本。 确定版本后，将立即执行该命令。 

### <a name="the-verb"></a>“谓词”
谓词仅仅是执行操作的命令。 `dotnet build` 生成代码。 `dotnet publish` 发布代码。 以按约定命名的控制台应用程序实现谓词：`dotnet-{verb}`。 在表示谓词的控制台应用程序中实现所有逻辑。 

### <a name="the-arguments"></a>参数
在命令行上传递的参数是正被调用的实际谓词/命令的参数。 例如，键入 `dotnet publish --output publishedapp` 时，会将 `--output` 参数传递给 `publish` 命令。 

## <a name="types-of-application-portability"></a>应用程序可移植性的类型
CLI 以两种主要方式实现应用程序的可移植性：

1. 可随处运行 .NET Core 的完全可移植应用程序已安装
2. 独立部署

可在 [.NET Core 应用程序部署](../deploying/index.md)主题中了解以上两点的详细信息。 

## <a name="migration-from-projectjson"></a>从 project.json 迁移
如果使用预览版 2 工具和 *project.json* 项目，可以参考 [dotnet migrate](dotnet-migrate.md) 命令文档，了解该命令以及如何迁移项目。 

> [!NOTE]
> `dotnet migrate` 命令当前不会迁移预览版 2 *project.json* 文件。 

## <a name="extensibility"></a>扩展性
当然，并非要在工作流中使用的每个工具都将成为核心 CLI 工具的一部分。 但是，.NET Core CLI 具备可使你为项目指定其他工具的扩展性模型。 有关详细信息，请参阅 [.NET Core CLI 扩展性模型](extensibility.md)主题。

## <a name="summary"></a>摘要
本文简短改善了 CLI 最重要的功能。 通过使用本站点上的引用和概念性主题可了解详细信息。 此外，还可以使用其他资源：
* [dotnet/CLI](https://github.com/dotnet/cli/) GitHub 存储库
* [入门说明](https://aka.ms/dotnetcoregs/)

