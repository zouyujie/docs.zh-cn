---
title: "Mac 上 .NET Core 的先决条件 | Microsoft Docs"
description: "在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所支持的 macOS 版本和 .NET Core 依赖项。"
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 03/16/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: ff143583ba62fc1d82561e739a75107e50ebee88
ms.openlocfilehash: da75f5fd56b7ce66b2c46ef488e6e26c55a63ee2
ms.lasthandoff: 03/20/2017

---

# <a name="prerequisites-for-net-core-on-mac"></a>Mac 上 .NET Core 的先决条件

本文介绍了在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所需的受支持的 macOS 版本和 .NET Core 依赖项。 所支持的操作系统版本和随附的依赖项适用于在 Mac 上开发 .NET Core 应用的三种方法：通过[你喜爱的编辑器的命令行](tutorials/using-with-xplat-cli.md)、[Visual Studio Code (VS Code)](https://code.visualstudio.com/) 和 [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)。

## <a name="supported-macos-versions"></a>支持的 macOS 版本

以下 macOS 版本均支持 .NET Core：

* macOS 10.12“Sierra”
* macOS 10.11“El Capitan”

在 [.NET Core 发行说明](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md)中查看受支持的操作系统的完整列表。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

在 macOS 上运行时，.NET Core 需要 OpenSSL。 获取 OpenSSL 的一个简单方法是使用适用于 macOS 的 [Homebrew (“brew”)](http://brew.sh/) 包。 在安装 *brew* 后，通过在终端（命令）提示符处执行以下命令来安装 OpenSSL：

```Terminal
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

安装 OpenSSL 后，获取官方 [.NET Core SDK for Mac 安装程序](https://go.microsoft.com/fwlink/?linkid=843444)。 .NET Core 1.1.1 是最新的版本。 有关长期支持版本和其他下载，请访问 [.NET 下载：所有下载](https://www.microsoft.com/net/download/core)。 如果在 macOS 上安装遇到问题，请查阅[已知问题和解决方法](https://github.com/dotnet/core/blob/master/cli/known-issues.md)。

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

使用 Visual Studio for Mac 在 macOS 上进行 .NET Core 开发需要：

* macOS 操作系统的受支持版本
* Openssl
* .NET Core SDK for Mac
* [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

