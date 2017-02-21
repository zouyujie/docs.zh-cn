---
title: "dotnet 命令 | Microsoft Docs"
description: "了解 dotnet 命令（.NET Core CLI 工具的通用驱动程序）及其用法。"
keywords: "dotnet, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 256e468e-eaaa-4715-b5fb-8cbddcf80e69
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: c80b5e7e26366b5253816e81a8203f90690eec1e

---

#<a name="dotnet-command-net-core-tools-rc4"></a>dotnet 命令 |（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 .NET Core 工具预览版 2，请参阅 [dotnet 命令](../../tools/dotnet.md)主题。

## <a name="name"></a>名称

dotnet - 运行命令行命令的通用驱动程序

## <a name="synopsis"></a>摘要

`dotnet [--version] [--verbose] [--info] [command] [arguments] [--help]`

## <a name="description"></a>描述
`dotnet` 是用于命令行接口 (CLI) 工具链的通用驱动程序。 可自己调用，提供简短的使用说明。 

每种特定功能均实现为命令。 若要使用此功能，请在 `dotnet` 后指定该命令，例如 [`dotnet build`](dotnet-build.md)。 该命令后的所有参数均为其自有参数。 

`dotnet` 自己作为命令使用的唯一情况是运行可移植应用。 在 `dotnet` 谓词后指定可移植应用程序 DLL 便可执行该应用程序。    

## <a name="options"></a>选项

`-v|--verbose`

启用详细输出。

`--version`

打印出 CLI 工具的版本。

`--info`

打印出有关 CLI 工具的更多详细信息，例如当前操作系统、提交该版本的 SHA 等。 

`-h|--help`

打印出有关命令的简短帮助。 如果仅使用 `dotnet`，还将打印可用命令的列表。  

## <a name="dotnet-commands"></a>dotnet 命令

dotnet 具有以下命令：

* [dotnet-new](dotnet-new.md)
   * 初始化 C# 或 F # 控制台应用程序项目。
* [dotnet-restore](dotnet-restore.md)
  * 还原给定应用程序的依赖项。 
* [dotnet-build](dotnet-build.md)
  * 生成 .NET Core 应用程序。
* [dotnet-publish](dotnet-publish.md)
   * 发布 .NET 可移植或独立应用程序。
* [dotnet-run](dotnet-run.md)
   * 从源运行应用程序。
* [dotnet-test](dotnet-test.md)
   * 使用 project.json 中指定的测试运行程序运行测试。
* [dotnet-pack](dotnet-pack.md)
   * 创建代码的 NuGet 包。
* [dotnet-migrate](dotnet-migrate.md)
   * 将有效的预览版 2 项目迁移到 RC4 项目。
* [dotnet-msbuild](dotnet-msbuild.md)
   * 提供对 MSBuild 命令行的访问权限。

## <a name="examples"></a>示例

初始化可以编译和运行的示例 .NET Core 控制台应用程序：

`dotnet new`

还原给定应用程序的依赖项：

`dotnet restore`

生成给定目录中的项目及其依赖项： 

`dotnet build`

运行名为 `myapp.dll` 的可移植应用：`dotnet myapp.dll`

## <a name="environment"></a>环境 

`DOTNET_PACKAGES`

主包缓存。 如未设置，在 Unix 上则默认为 $HOME/.nuget/packages 或在 Windows 上默认为 %HOME%\NuGet\Packages。

`DOTNET_SERVICING`

指定加载运行时期间共享主机要使用的服务索引的位置。

`DOTNET_CLI_TELEMETRY_OPTOUT`

指定是否收集并向 Microsoft 发送 .NET Core 工具使用情况的相关数据。 若要选择退出遥测功能（接受的值有：true、1 或“是”），则为 `true`；否则为 `false`（接受的值有：false、0 或“否”）。 如未设置，则默认为 `false`，即遥测功能处于开启状态。




<!--HONumber=Feb17_HO2-->


