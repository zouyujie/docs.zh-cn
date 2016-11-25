---
title: "dotnet 命令 | .NET Core SDK"
description: "了解 dotnet 命令（.NET Core CLI 工具的通用驱动程序）及其用法。"
keywords: "dotnet, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 93015521-2127-4fe9-8fce-ca79bcc4ff49
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: bbc13c8cca82e660f0f8ccf7d88c0340d9c06e68

---

#<a name="dotnet-command"></a>dotnet 命令

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
   * 将有效的预览版 2 项目迁移到预览版 3 项目
* [dotnet-msbuild](dotnet-msbuild.md)
   * 提供对 MSBuild 命令行的访问权限

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




<!--HONumber=Nov16_HO3-->


