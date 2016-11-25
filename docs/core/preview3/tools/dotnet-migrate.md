---
title: "dotnet-migrate 命令 | .NET Core SDK"
description: "dotnet-migrate 命令可迁移项目及其所有依赖项。"
keywords: "dotnet-migrate, CLI, CLI 命令, .NET Core"
author: mairaw
manager: wpickett
ms.date: 11/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 70285a83-4103-4617-be8b-d0e1e9a4a91d
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 150d70e3f0a80f7f6e733abee3691a0fe420919f

---

#<a name="dotnet-migrate"></a>dotnet-migrate

## <a name="name"></a>名称 
dotnet-migrate - 将预览版 2 .NET Core 项目迁移到预览版 3 .NET Core 项目

## <a name="synopsis"></a>摘要

`dotnet migrate [--help] [--template-file]  
    [--sdk-package-version] [--xproj-file]  
    [--skip-project-references]  [--report-file] [--format-report-file-json]
    [--skip-backup]
    [<arguments>]`

## <a name="description"></a>描述
`dotnet migrate` 命令将有效的基于预览版 2 `project.json` 的项目迁移到有效的预览版 3 `csproj` 项目。 默认情况下，命令将迁移根项目和根项目包含的任何项目引用。 可以在运行时使用 `--skip-project-references` 选项禁用此行为。 

可以对以下对象进行迁移：

* 通过指定要迁移的 `project.json` 文件来迁移单个项目
* 通过将路径传递到 `global.json` 文件来迁移 `global.json` 文件中指定的所有目录
* 以递归方式迁移给定目录的所有子目录 

migrate 命令将迁移的 `project.json` 文件保存在 `backup` 目录中，如果该目录不存在，将创建一个。 可以使用 `--skip-backup` 选项对其重写。 

默认情况下，迁移操作会将迁移过程的状态输出到标准输出 (STDOUT)。 如果使用 `--report-file` 选项，该输出也将保存到你所指定的文件。 

从预览版 3 开始，`dotnet migrate` 命令仅支持有效预览版 2 `project.json` 文件。 这意味着无法用它将旧的 DNX 或预览版 1 `project.json` 文件直接迁移到 csproj；你需要首先将它们迁移到预览版 2 project.json 文件，然后再迁移到 csproj 文件。 将来，我们将添加对预览版 1 项目的支持。 

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。  

`-t|--template-file <TEMPLATE_FILE>`

用于迁移的模板 csproj 文件。 默认情况下，将使用与被 `dotnet new` 删除的模板相同的模板。 

`-v|--sdk-package-version <VERSION>`

在已迁移应用中将被引用的 sdk 包的版本。 默认为 dotnet new 中 sdk 的版本。

`-x|--xproj-file <FILE>`

要使用的 xproj 文件的路径。 当项目目录中有多个 xproj 时需要。

`-s|--skip-project-references [Debug|Release]`

跳过迁移项目引用。 默认情况下，以递归方式迁移项目引用。

`-r|--report-file <REPORT_FILE>`

除控制台外，还将迁移报告输出到文件。

`--format-report-file-json <REPORT_FILE>`

将迁移报告文件（而非用户消息）作为 json 输出。

`--skip-backup`

在成功迁移后，跳过将 project.json、global.json 和 \*.xproj 移动到 `backup` 目录的步骤。

## <a name="examples"></a>示例

将当前目录中的项目及其所有项目迁移到项目依赖项：

`dotnet migrate`

迁移 `global.json` 文件所指向的所有项目：

`dotnet migrate path/to/global.json`

仅迁移当前项目，不迁移项目到项目的依赖项，并使用特定的 SDK 版本：

`dotnet migrate -s -v 1.0.0-preview3`




<!--HONumber=Nov16_HO3-->


