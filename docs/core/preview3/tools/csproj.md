---
title: "csproj 引用 | .NET Core SDK"
description: "了解现有文件和 .NET Core csproj 文件之间的区别"
keywords: "引用, csproj, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 1a0178cc5763f06213d45b9b3826c56ce970776c

---

# <a name="additions-to-csproj-format-for-net-core"></a>.NET Core 的 csproj 格式的新增内容

本文档概述了作为从 project.json 移动到 csproj.json 和 [MSBuild](https://github.com/Microsoft/MSBuild) 的一部分，添加到 csproj 文件的更改。 本文档仅简单介绍**非核心 csproj 文件的增量**。 如果需要有关常规项目文件的语法和引用的详细信息，请参阅 [MSBuild 项目文件]()文档。 

> ![注意] 本文档会不断更新，因此请时常查阅以了解新增内容。 

## <a name="additions"></a>新增内容

### <a name="packagereference"></a>PackageReference
指定项目中的 NuGet 依赖项。 `Include` 属性指定包 ID。 

```xml
<PackageReference Include="<package-id>">
    <Version></Version>
    <PrivateAssets></PrivateAssets>
    <IncludeAssets></IncludeAssets>
    <ExcludeAssets></ExcludeAssets>
</PackageReference>
```

#### <a name="version"></a>版本
`<Version>` 指定要还原的包的版本。 此元素遵从 NuGet 版本控制方案的规则。

#### <a name="includeassets"></a>IncludeAssets
`<IncludeAssets>` 子元素指定应使用父级 `<PackageReference>` 指定的包所属的哪些资产。 

此元素可以包含下面的一个或多个值：

* 编译 - 是可用于进行编译的 lib 文件夹的内容
* 运行时 - 是分布的运行时文件夹的内容
* 内容文件 - 是所用内容文件文件夹的内容
* 生成 - 使用生成文件夹中的属性/目标
* 本机 - 是从本机资产复制到运行时输出文件夹的内容
* 分析器 - 使用分析器

或者，此元素可以包含：

* 无 - 没有使用上述任何值
* 全部 - 使用了上述所有值。

#### <a name="excludeassets"></a>ExcludeAssets
`<ExcludeAssets>` 子元素指定不应使用父级 `<PackageReference>` 指定的包所属的哪些资产。

此元素可以包含下面的一个或多个值：

* 编译 - 是可用于进行编译的 lib 文件夹的内容
* 运行时 - 是分布的运行时文件夹的内容
* 内容文件 - 是所用内容文件文件夹的内容
* 生成 - 使用生成文件夹中的属性/目标
* 本机 - 是从本机资产复制到运行时输出文件夹的内容
* 分析器 - 使用分析器

或者，此元素可以包含：

* 无 - 没有使用上述任何值
* 全部 - 使用了上述所有值。

#### <a name="privateassets"></a>PrivateAssets
`<PrivateAssets>` 子元素指定应使用父级 `<PackageReference>` 指定的包所属的哪些资产，但这些资产不应传递到下一个项目。 

> [!NOTE]
> 这是 project.json/xproj `SuppressParent` 元素的新术语。 

此元素可以包含下面的一个或多个值：

* 编译 - 是可用于进行编译的 lib 文件夹的内容
* 运行时 - 是分布的运行时文件夹的内容
* 内容文件 - 是所用内容文件文件夹的内容
* 生成 - 使用生成文件夹中的属性/目标
* 本机 - 是从本机资产复制到运行时输出文件夹的内容
* 分析器 - 使用分析器

或者，此元素可以包含：

* 无 - 没有使用上述任何值
* 全部 - 使用了上述所有值。

### <a name="dotnetclitoolreference"></a>DotnetCliToolReference
`<DotnetCliToolReference>` 元素指定用户想要在项目的上下文中还原的 CLI 工具。 在 `project.json` 中，它可以替换 `tools` 节点。 

#### <a name="version"></a>版本
`<Version>` 指定要还原的包的版本。 此元素遵从 NuGet 版本控制方案的规则。

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers
`<RuntimeIdentifiers>` 元素可用于指定项目的[运行时标识符](../../rid-catalog.md)的列表（以分号分隔）。 以上功能允许发布独立部署。 




<!--HONumber=Jan17_HO3-->


