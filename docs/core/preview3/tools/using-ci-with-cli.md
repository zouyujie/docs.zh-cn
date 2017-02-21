---
title: "在持续集成 (CI) 中使用 .NET Core SDK 和工具| Microsoft Docs"
description: "在持续集成 (CI) 中使用 .NET Core SDK 和工具"
keywords: ".NET、.NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0d6e1e34-277c-4aaf-9880-3ebf81023857
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 95c7f0f9911c7cb37c12afec74d0e942db77fbf6

---

# <a name="using-net-core-sdk-and-tools-in-continuous-integration-ci-net-core-tools-rc4"></a>在持续集成 (CI) 中使用 .NET Core SDK 和工具（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅[在持续集成 (CI) 中使用 .NET Core SDK 和工具](../../tools/using-ci-with-cli.md)主题。

## <a name="overview"></a>概述
本文档概述了 .NET Core SDK 及其在生成服务器上的工具的使用情况。 一般情况下，在 CI 生成服务器上，用户希望以某种方式自动化安装。 理想情况下，如果可能的话，自动化不需要管理特权。 

对于 SaaS CI 解决方案，有几个选项。 本文档将介绍两个非常受欢迎的选项：[TravisCI](https://travis-ci.org/) 和 [AppVeyor](https://www.appveyor.com/)。 当然，还存在许多其他选项，但安装和使用机制应该类似。

## <a name="installation-options-for-ci-build-servers"></a>CI 生成服务器的安装选项

## <a name="using-the-native-installers"></a>使用本机安装程序
如果使用需要管理特权的安装程序不是问题，可使用每个平台的本机安装程序来设置生成服务器。 此方法（尤其对 Linux 生成服务器）有一个好处：自动安装运行 SDK 所需的依赖项。 本机安装程序也将安装全系统版本的 SDK（可能期望这样操作）；如果未安装，应查看下文介绍的[安装程序脚本使用情况](#using-the-installer-script)。 

使用此方法非常简单。 对于 Linux，可选择使用基于源的包管理器（例如用于 Ubuntu 的 `apt-get` 或用于 CentOS 的 `yum`），或使用包本身（即 DEB 或 RPM）。 前者需要设置包含包的源。

对于 Windows 平台，可以使用 MSI。 

可在指向最新稳定版本的 [.NET Core 入门页面](https://aka.ms/dotnetcoregs)找到所有这些二进制文件。 若要使用较新（可能不稳定）的版本或最新版本，可使用 [CLI 存储库](https://github.com/dotnet/cli)中的链接。 

## <a name="using-the-installer-script"></a>使用安装程序脚本
使用安装程序脚本允许在生成服务器上进行非管理员安装。 它还允许非常简单的自动化。 脚本自己会下载所需 ZIP/tarball 文件并将其解压缩；它还会将本地计算机上的安装位置添加到 PATH，以便安装后即可为调用提供工具。 

启动生成后，可轻松自动化安装程序脚本，提取和安装所需版本的 SDK 。 “所需版本”指正在生成的应用程序所需的任何版本。 可选择安装路径，因此可本地安装 SDK，然后在生成完成后清理。 这为生成过程带来了额外的封装和隔离性。 

可在 [dotnet-install](dotnet-install-script.md) 文档中找到安装脚本引用。 

### <a name="dealing-with-the-dependencies"></a>处理依赖项
使用安装程序脚本意味着不自动安装本机依赖项，如果在其上安装的操作系统上没有依赖项，则必须安装依赖项。 可在 [CLI 存储库](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)中查看先决条件列表。 

## <a name="ci-services-setup-examples"></a>CI 服务设置示例
以下各节介绍使用提及的 CI SaaS 产品/服务的配置示例。 

### <a name="travisci"></a>TravisCI

可将 [travis-ci](https://travis-ci.org/) 配置为使用 `csharp` 语言和 `dotnet` 键安装 .NET Core SDK。

只需使用：

```yaml
dotnet: 1.0.0-preview2-003121
```

Travis 可在生成矩阵中运行 `osx` (OS X 10.11) 和 `linux` ( Ubuntu 14.04 ) 作业，有关详细信息，请参阅 [example .travis.yml](https://github.com/dotnet/docs/blob/master/.travis.yml)（示例 .travis.yml）。

### <a name="appveyor"></a>AppVeyor

[appveyor.com ci](https://www.appveyor.com/) 已在生成辅助角色进程映像 `Visual Studio 2015` 中安装了 .NET Core SDK preview2。

只需使用：

```yaml
os: Visual Studio 2015
```

可安装 .NET Core SDK 的特定版本，有关详细信息，请参阅 [example appveyor.yml](https://github.com/dotnet/docs/blob/master/appveyor.yml)（示例 appveyor.yml）。 

在本示例中，将 .NET Core SDK 二进制文件下载、解压缩到一个子目录中并添加到 `PATH` env var。

可添加生成矩阵，使用多个版本的 .NET Core SDK 运行集成测试。

```yaml
environment:
  matrix:
    - CLI_VERSION: 1.0.0-preview2-003121
    - CLI_VERSION: Latest

install:
  # .NET Core SDK binaries
  - ps: $url = "https://dotnetcli.blob.core.windows.net/dotnet/preview/Binaries/$($env:CLI_VERSION)/dotnet-dev-win-x64.$($env:CLI_VERSION.ToLower()).zip"
  # follow normal installation from binaries
```


<!--HONumber=Feb17_HO2-->


