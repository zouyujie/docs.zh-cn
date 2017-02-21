---
title: "csproj 引用 | Microsoft Docs"
description: "了解现有文件和 .NET Core csproj 文件之间的区别"
keywords: "引用, csproj, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 07/02/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: 0402707f98af8b716b041ba1260162cd227918cc
ms.openlocfilehash: 98f6ced2a199bdbe2f91f46e48ffd3ac52438cf8

---

# <a name="additions-to-the-csproj-format-for-net-core"></a>.NET Core 的 csproj 格式的新增内容

[!INCLUDE[preview-warning](../../../includes/warning.md)]

本文档概述了作为从 `project.json` 移动到 `csproj` 和 [MSBuild](https://github.com/Microsoft/MSBuild) 的一部分，添加到 csproj 文件的更改。 有关常规项目文件的语法和引用的详细信息，请参阅 [MSBuild 项目文件](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference)文档。  

## <a name="additions"></a>新增内容

* 在项目中指定 NuGet 依赖项的 PackageReference 项。 `Include` 属性指定包 ID。 

```xml
<PackageReference Include="<package-id>" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

## <a name="version"></a>版本
`Version` 指定要还原的包的版本。 此元素遵从 NuGet 版本控制方案的规则。

## <a name="includeassets"></a>IncludeAssets
`IncludeAssets` 属性指定应使用 `<PackageReference>` 指定的包中的哪些资产。 

此属性可以包含下列一个或多个值：

* `Compile` - 可对 lib 文件夹内容进行编译。
* `Runtime` - 分发运行时文件夹内容。
* `ContentFiles` - 使用内容文件文件夹内容。
* `Build` - 使用生成文件夹中的属性/目标。
* `Native` - 将本机资产内容复制到运行时输出文件夹。
* `Analyzers` - 使用分析器。

此属性也可以包含：

* `None` - 不使用任何资产。
* `All` - 使用所有资产。

## <a name="excludeassets"></a>ExcludeAssets
`ExcludeAssets` 属性指定不得使用 `<PackageReference>` 指定的包中的哪些资产。

此属性可以包含下列一个或多个值：

* `Compile` - 可对 lib 文件夹内容进行编译。
* `Runtime` - 分发运行时文件夹内容。
* `ContentFiles` - 使用内容文件文件夹内容。
* `Build` - 使用生成文件夹中的属性/目标。
* `Native` - 将本机资产内容复制到运行时输出文件夹。
* `Analyzers` - 使用分析器。

或者，此元素可以包含：

* `None` - 不使用任何资产。
* `All` - 使用所有资产。

## <a name="privateassets"></a>PrivateAssets
`PrivateAssets` 属性指定应使用 `<PackageReference>` 指定的包中的哪些资产，但不得将这些资产传递到下一个项目。 

> [!NOTE]
> 这是 project.json/xproj `SuppressParent` 元素的新术语。 

此属性可以包含下列一个或多个值：

* `Compile` - 可对 lib 文件夹内容进行编译。
* `Runtime` - 分发运行时文件夹内容。
* `ContentFiles` - 使用内容文件文件夹内容。
* `Build` - 使用生成文件夹中的属性/目标。
* `Native` - 将本机资产内容复制到运行时输出文件夹。
* `Analyzers` - 使用分析器。

此属性也可以包含：

* `None` - 不使用任何资产。
* `All` - 使用所有资产。

* DotnetCliToolReference `<DotnetCliToolReference>` 项元素指定用户要在项目上下文中还原的 CLI 工具。 在 `project.json` 中，它可以替换 `tools` 节点。 

```xml
<DotnetCliToolReference Include="<package-id>" Version="" />
```

## <a name="version"></a>版本
`Version` 指定要还原的包的版本。 此属性遵循 NuGet 版本控制方案规则。

* RuntimeIdentifiers `<RuntimeIdentifiers>` 元素可用于指定项目[运行时标识符 (RID)](../../rid-catalog.md) 的分号分隔列表。 使用 RID ，可发布独立部署。 

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```


* RuntimeIdentifiers `<RuntieIdentifier>` 元素可用于指定项目的唯一[运行时标识符 (RID)](../../rid-catalog.md)。 使用 RID ，可发布独立部署。 

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```


* PackageTargetFallback `<PackageTargetFallback>` 元素可用于指定要在还原包时使用的一组兼容目标。 旨在允许使用 dotnet TxM 的包处理未声明 dotnet TxM 的包。 如果项目使用 dotnet TxM，那么依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。 

以下示例展示了项目中所有目标的回退： 

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

以下示例仅指定了 `netcoreapp1.0` 目标的回退：

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp1.0'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="nuget-metadata-properties"></a>NuGet 元数据属性
迁移到 MSbuild 后，我们已将在打包 NuGet 包时使用的输入元数据从 project.json 移到 csproj 文件中。 输入元数据为 MSBuild 属性。 下面列出了在使用 `dotnet pack` 命令或属于 SDK 的 `Pack` MSBuild 目标时，用作打包进程的输入的属性。 

* IsPackable
* PackageVersion
* PackageId
* 标题
* 作者
* 描述
* Copyright
* PackageRequireLicenseAcceptance
* PackageLicenseUrl
* PackageProjectUrl
* PackageIconUrl
* PackageReleaseNotes
* PackageTags
* PackageOutputPath
* IncludeSymbols
* IncludeSource
* PackageTypes
* IsTool
* RepositoryUrl
* RepositoryType
* NoPackageAnalysis
* MinClientVersion
* IncludeBuildOutput
* IncludeContentInPack
* BuildOutputTargetFolder
* ContentTargetFolders
* NuspecFile
* NuspecBasePath
* NuspecProperties


<!--HONumber=Feb17_HO2-->


