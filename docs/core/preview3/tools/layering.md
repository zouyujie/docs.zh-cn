---
title: ".NET Core 命令行工具预览版 3 体系结构"
description: "预览版 3 对整体 .NET Core 工具的分层方式作出了某些更改。"
keywords: "CLI, 扩展性, 自定义命令, .NET Core"
author: blackdwarf
manager: wpickett
ms.date: 11/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 233d365b582c274cd3a1f078846a6e854c7a6c95

---

<a name="high-level-overview-of-changes-in-cli-preview-3"></a>CLI 预览版 3 更改的高级概述
-----------------------------------------------

# <a name="overview"></a>概述
本文档详细介绍了从 `project.json` 移动到 MSBuild 和 `csproj` 项目系统带来的更改。 本文将概括介绍工具分层的新方式、提供了哪些新的部分以及新部分在整体结构中的位置。 阅读本文后，应该更深入地了解移动到 MSBuild 和 `csproj` 后所有构成 .NET Core 工具的所有部分。 

> **注意：**本文**并不需要**使用预览版 3 .NET Core 命令行工具。 你可以继续按以往习惯使用工具。 本文完整介绍了移动到 MSBuild 会如何改变整体“分层”以及命令行工具的体系结构。 

# <a name="moving-away-from-projectjson"></a>弃用 project.json
.NET Core 预览版 3 工具最大的改动无疑是[弃用 project.json，改用 csproj](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/) 作为项目系统。 预览版 3 版本的命令行工具是首个不包含任何 project.json 支持的 .NET Core 命令行工具的版本。 这意味着它不能用于生成、运行或发布基于 project.json 的应用程序和库。 若要使用此版本的工具，需要迁移现有项目或启动新的项目。 

作为此次移动的一部分，开发用于生成 project.json 项目的自定义生成引擎被替换为一个功能完整的成熟生成引擎，即 [MSBuild](https://github.com/Microsoft/msbuild)。 MSBuild 是.NET 社区中的知名引擎，因为自该平台首个版本以来，它一直作为一项关键技术。 当然，因为它需要生成 .NET Core 应用程序，所以 MSBuild 已经移植到 .NET Core，并可在 .NET Core 运行的任何平台上使用。 .NET Core 的一个主要的好处是跨平台开发堆栈，我们已确保本次迁移不会破坏此好处。

> **注意：**如果还不熟悉 MSBuild，并且想要了解相关详细信息，可参阅[现有文档](https://msdn.microsoft.com/en-us/library/dd637714.aspx)。 

# <a name="the-tooling-layers"></a>工具层
随着弃用现有项目系统以及改换生成引擎，自然会出现一个疑问：这些更改会改变整体 .NET Core 工具生态系统的整体“分层”吗？ 是否有新的位和组件？

首先来简要介绍下预览版 2 分层，如下图所示：

![预览版 2 工具高级体系结构](media/p2-arch.png)

这些工具的分层非常简单。 在底部，我们将 .NET Core 命令行工具作为基础。 所有其他高级工具（例如 Visual Studio 或 VS Code）依靠 CLI 来生成项目、还原依赖关系以及完成其他操作。 这意味着，例如，如果 Visual Studio 要执行还原操作，它会在 CLI 中调入 `dotnet restore` 命令。 

随着迁移到新的项目系统，之前的图表会更改： 

![预览版 3 工具高级体系结构](media/p3-arch.png)

主要区别在于 CLI 不再作为基础层；现由“共享 SDK 组件”充当此角色。 共享 SDK 组件是一组负责编译代码、发布代码、打包 nuget 包等操作的目标和关联任务。SDK 本身是一个开源代码，可在 GitHub 上的 [SDK 存储库](https://github.com/dotnet/sdk)中获得。 

> **注意：**“目标”是一个表示 MSBuild 可调用的已命名操作的 MSBuild 术语。 其通常伴随着执行此目标应执行的某个逻辑的一个或多个任务。 MSBuild 支持多个现成的目标，如 `Copy` 或 `Execute`；它还允许用户使用托管代码编写自己的任务，并定义要执行这些任务的目标。 可在 [MSDN](https://msdn.microsoft.com/en-us/library/ms171466.aspx) 上阅读有关 MSBuild 任务的详细信息。 

现在所有工具集使用共享 SDK 组件及其目标，包括 CLI。 例如，下个版本的 Visual Studio 不会调用到 `dotnet restore` 命令来还原 .NET Core 项目的依赖关系，它会直接使用“还原”目标。 由于这些皆是 MSBuild 目标，因此你也可通过 [dotnet msbuild](dotnet-msbuild.md) 命令使用原始 MSBuild 来执行。 

## <a name="preview-3-cli-commands"></a>预览版 3 CLI 命令
共享 SDK 组件意味着大部分现有 CLI 命令已重新实现为 MSBuild 任务和目标。 这对 CLI 命令和工具集的使用意味着什么？ 

从使用角度而言，它不会更改使用 CLI 的方式。 CLI 仍具有预览 2 版本中存在的核心命令：

* `new`
* `restore`
* `run` 
* `build`
* `publish`
* `test`
* `pack` 

这些命令的作用没有发生改变（仍可新建项目、生成项目、发布项目、打包项目等等）。 大部分选项未作更改，仍然存在，你可以（使用 `dotent <command> --help`）查看命令帮助屏幕或本站点上的预览版 3 文档来了解更改。 

从执行角度而言，CLI 命令会采用其参数并构造对“原始”MSBuild 的调用，从而设置所需属性和运行所需目标。 为更好的说明这点，请参考下面的命令： 

    `dotnet publish -o pub -c Release`. 
    
此命令会使用“发布”配置将应用程序发布到 `pub` 文件夹。 在内部，此命令会转换成下面的 MSBuild 调用： 

    `dotnet msbuild /t:Publish /p:OutputPath=pub /p:Configuration`

此规则值得注意的例外是 `new` 和 `run` 命令，因为它们未实现为 MSBuild 目标。 

# <a name="conclusion"></a>结束语 
本文档在高级别概述了整体 CLI 工具体系结构所发生的更改以及预览版 3 中附带的功能。 它在预览版 3 中引入了共享 SDK 组件的概念，也从技术角度解释了 CLI 命令的工作原理。 




<!--HONumber=Nov16_HO3-->


