---
title: "dotnet-add package 命令 | Microsoft Docs"
description: "使用 dotnet-add package 命令可方便地向项目添加 NuGet 包引用。"
keywords: "dotnet-add, CLI, CLI 命令, .NET Core"
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 88e0da69-a5ea-46cc-8b46-5493242b7af9
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 806f4383452cb250f302dc30ab2d59f7e4772026
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-add-package"></a>dotnet-add package

## <a name="name"></a>名称

`dotnet-add package` - 向项目文件添加包引用。

## <a name="synopsis"></a>摘要

```
dotnet add [project] package <package_name> [-v|--version] [-f|--framework] [-n|--no-restore] [-s|--source] [--package-directory]
dotnet add package [-h|--help]
```

## <a name="description"></a>说明

使用 `dotnet add package` 可方便地向项目文件添加包引用。 运行该命令后，还有一个兼容性检查，确保尝试添加的包与项目中的所有框架兼容。 如果通过了该检查，将运行[还原](dotnet-restore.md)并将 `<PackageReference>` 片断添加到项目文件。

例如，将 `Newtonsoft.Json` 添加到 *ToDo.csproj* 会生成如下输出：

```
Microsoft (R) Build Engine version 15.1.545.13942
Copyright (C) Microsoft Corporation. All rights reserved.

  Writing /var/folders/gj/1mgg_4jx7mbdqbhw1kgcpcjr0000gn/T/tmpm0kTMD.tmp
info : Adding PackageReference for package 'Newtonsoft.Json' into project 'ToDo.csproj'.
log  : Restoring packages for ToDo.csproj...
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json 119ms
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg 27ms
info : Package 'Newtonsoft.Json' is compatible with all the specified frameworks in project 'ToDo.csproj'.
info : PackageReference for package 'Newtonsoft.Json' version '9.0.1' added to file 'ToDo.csproj'.
```

*ToDo.csproj* 文件现包含用于引用的包的 [`<PackageReference>`](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files) 片段。

```xml
<PackageReference Include="Newtonsoft.Json">
  <Version>9.0.1</Version>
</PackageReference>
```

## <a name="arguments"></a>参数

`project`

要操作的项目文件。 如果未指定，此命令会搜索当前目录来获取一个项目文件。

`package_name`

要添加的包引用。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-v|--version <VERSION>`

包的版本。

`-f|--framework <FRAMEWORK>`

仅在以特定框架为目标时添加包引用。

`-n|--no-restore`

在不执行还原预览和兼容性检查的情况下添加包引用。

`-s|--source <SOURCE>`

使用要在还原操作期间使用的特定 NuGet 包源。

`--package-directory <PACKAGE_DIRECTORY>`

将包还原到指定的目录。

## <a name="examples"></a>示例

将 `Newtonsoft.Json` NuGet 包添加到项目：

`dotnet add package Newtonsoft.Json`

向项目添加特定版本的包：

`dotnet add ToDo.csproj package Microsoft.Azure.DocumentDB.Core -v 1.0.0`

使用特定的 NuGet 源添加包：

`dotnet add package Microsoft.AspNetCore.StaticFiles -s https://dotnet.myget.org/F/dotnet-core/api/v3/index.json`

