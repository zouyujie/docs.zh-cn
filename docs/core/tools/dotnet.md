---
title: "dotnet 命令 | Microsoft Docs"
description: "了解 dotnet 命令（.NET Core CLI 工具的通用驱动程序）及其用法。"
keywords: "dotnet, CLI, CLI 命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 256e468e-eaaa-4715-b5fb-8cbddcf80e69
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: e3eedff7d98245bd63d758236840568eabd05445
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-command"></a>dotnet 命令

## <a name="name"></a>名称

`dotnet` - 运行命令行命令的通用驱动程序

## <a name="synopsis"></a>摘要

```
dotnet [command] [arguments] [--version] [--info] [-d|--diagnostics] [-v|--verbose]
dotnet [-h|--help]
```

## <a name="description"></a>描述

`dotnet` 是用于命令行接口 (CLI) 工具链的通用驱动程序。 可自己调用，提供简短的使用说明。

每种特定功能均实现为命令。 若要使用此功能，请在 `dotnet` 后指定该命令，例如 [`dotnet build`](dotnet-build.md)。 该命令后的所有参数均为其自有参数。

`dotnet` 自己作为命令使用的唯一情况是运行可移植应用。 在 `dotnet` 谓词后指定可移植应用程序 DLL 便可执行该应用程序。

## <a name="options"></a>选项

`-v|--verbose`

启用详细输出。

`-d|--diagnostics`

启用诊断输出。

`--version`

打印出 CLI 工具的版本。

`--info`

打印出有关 CLI 工具的更多详细信息，例如当前操作系统、提交该版本的 SHA 等。

`-h|--help`

打印出有关命令的简短帮助。 如果仅使用 `dotnet`，还将打印可用命令的列表。

## <a name="dotnet-commands"></a>dotnet 命令

dotnet 具有以下命令：

* [dotnet-new](dotnet-new.md)
  * 为给定的模板初始化 C# 或 F # 项目。
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
  * 将有效的预览版 2 项目迁移到 .NET Core SDK 1.0 项目。
* [dotnet-msbuild](dotnet-msbuild.md)
  * 提供对 MSBuild 命令行的访问权限。
* [dotnet-clean](dotnet-clean.md)
  * 清理生成输出。
* [dotnet-sln](dotnet-sln.md)
  * 用于添加、删除和列出解决方案文件中项目的选项。
* 项目修改命令
  * 引用 - 添加、删除和列出“项目到项目”引用。
    * [dotnet-add 引用](dotnet-add-reference.md)
    * [dotnet-remove 引用](dotnet-remove-reference.md)
    * [dotnet-list 引用](dotnet-list-reference.md)
  * 包 - 添加和删除项目上的 NuGet 包。
    * [dotnet-add 包](dotnet-add-package.md)
    * [dotnet-remove 包](dotnet-remove-package.md)

## <a name="examples"></a>示例

初始化可以编译和运行的示例 .NET Core 控制台应用程序：

`dotnet new console`

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
