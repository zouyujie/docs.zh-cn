---
title: ".NET Core 版本控制"
description: ".NET Core 版本控制"
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: f6f684b1-1d2c-4105-8376-7c1959e23803
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 636c86fed9952542a256c075eb9e388b70cff174
ms.lasthandoff: 03/02/2017

---

# <a name="net-core-versioning"></a>.NET Core 版本控制

.NET Core 是 [NuGet 包](../packages.md)和框架的平台，作为单元分布。 每个平台层都可单独进行版本控制，以实现产品敏捷性并准确描述产品更改。 虽然有巨大的版本控制灵活性，但需要将平台作为单元进行版本控制以使产品更易于理解。

通过包管理器 (NuGet) 进行描述并交付为包，产品在某些方面具有唯一性。 虽然通常将 .NET Core 作为独立的 SDK获取，SDK 在很大程度上是比 NuGet 包更方便的体验，因此与包没有不同之处。 因此，版本控制对包而言是首要且最重要的，其他版本控制体验以此为基础。

## <a name="semantic-versioning"></a>语义版本控制

.NET Core 使用[语义版本控制 (SemVer)](http://semver.org/)，采用 major.minor.patch 版本控制，通过版本号的各部分来描述更改程度和类型。

以下版本控制模板通常适用于 .NET Core。 在一些情况下，已通过调整来适应现有版本控制。 本文档稍后会介绍此类情况。 例如，框架仅用于表示平台和 API 功能，这符合主要/次要版本控制。

### <a name="versioning-form"></a>版本控制窗体

MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]

### <a name="decision-tree"></a>决策树

以下情况为 MAJOR：
  - 放弃对平台的支持
  - 采用现有依赖项的较新 MAJOR 版本 
  - 默认情况下禁用兼容性

以下情况为 MINOR：
  - 添加公共 API 外围应用 
  - 添加新行为
  - 采用现有依赖项的较新 MINOR 版本
  - 引入新依赖项 
  
以下情况为 PATCH：
  - 修复 bug
  - 添加对较新平台的支持
  - 采用现有依赖项的较新 PATCH 版本
  - 任何其他更改（未通过其他方式捕获）

确定增加内容时若有多个更改，请选择最高类型的更改。

## <a name="versioning-scheme"></a>版本控制方案

.NET Core 将通过以下方式定义并进行版本控制：

- 以包的形式分发的运行时和框架实现。 对每个包进行独立的版本控制，特别是对于修补程序版本控制。
- 将细粒度包作为版本控制单元引用的一组元包。 从包单独对元包进行版本控制。
- 表示逐渐变大的 API 集的一组框架（如 `netstandard`），如一组版本控制快照中所述。

### <a name="packages"></a>包

库包单独发展，并单独进行版本控制。 与 .NET Framework 系统重叠的包。\* 程序集通常使用 4.x 版本控制，这符合 .NET Framework 4.x 版本控制（历史选择）。 不与 .NET Framework 库重叠的包（如 [System.Reflection.Metadata](https://www.nuget.org/packages/System.Reflection.Metadata)）通常从 1.0 开始并由此增加。

由于处于平台的基底，由 [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) 描述的包将被特殊处理。

- NETStandard.Library 包通常作为集进行版本控制，因为其之间具有实现级依赖项。
- API 将仅作为主要或次要 .NET Core 版本的一部分添加到 NETStandard.Library 包，因为这样做需要添加新的 `netstandard` 版本。 这是 SemVer 要求之外的要求。

### <a name="metapackages"></a>元包

.NET Core 元包的版本控制基于其映射的框架。 元包采用在包关闭中其映射框架的最高版本号（如 netstandard1.6）。 

元包的修补程序版本用于表示对元包的更新以引用更新的包。 修补程序版本绝不会包含更新的框架版本。 因此，元包不严格符合 SemVer，因为其版本控制方案不表示基础包中的更改程度，而是主要表示 API 级别。 

.NET Core 有两种主要的元包。

**NETStandard.Library**

- 自 .NET Core 1.0 的 v1.6 开始（这些版本通常不匹配或不特意匹配）。
- 映射到 `netstandard` 框架。 
- 描述被视为新式应用开发所需，且 .NET 平台必须实现以被视为 [.NET Standard](../../standard/library.md) 平台的包。

**Microsoft.NETCore.App**

- 自 .NET Core 1.0 的 v1.0 开始（这些版本将匹配）。
- 映射到 `netcoreapp` 框架。
- 描述 .NET Core 分发中的包。

注意：[`Microsoft.NETCore.Portable.Compatibility`](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) 是另一个 .NET Core 元包。 它不映射到特殊框架，因此其版本控制与包相同。

### <a name="frameworks"></a>框架

添加新 API 时，会更新框架版本。 它们没有修补程序版本的概念，因为其表示 API 形状，不表示实现问题。 主要和次要版本控制将按照之前指定的 SemVer 规则进行。

`netcoreapp` 框架已关联到 .NET Core 分发。 它将遵循由 .NET Core 使用的版本号。 例如，发布 .NET Core 2.0 时，它将面向 `netcoreapp2.0`。 考虑到其对所有 .NET 运行时均同样适用，`netstandard` 框架不匹配任何 .NET 运行时的版本控制方案。

## <a name="versioning-in-practice"></a>版本控制实践

每天，在 GitHub 上的 .NET Core 存储库中都有提交和 PR，因此会新生成许多库。 为每个更改创建 .NET Core 的新公共版本是不切实际的。 在制作新的公共稳定 .NET Core 版本前，将在一些松散定义的时期（如周或月）聚合更改。

新版本的 .NET Core 可能意味着以下内容：

- 包和元包的新版本。
- 各种框架的新版本，假定添加新 API。
- .NET Core 分发的新版本。

### <a name="shipping-a-patch-release"></a>传送修补程序版本

传送 .NET Core v1.0.0 稳定版本后，对 .NET Core 库进行修补程序级别更改以修复 bug 并改进性能和可靠性。 更新各种元包以引用更新的 .NET Core 库包。 将元包作为修补程序更新 (x.y.z) 进行版本控制。 不更新框架。 发布新的 .NET Core 分发，其具有与 `Microsoft.NETCore.App` 元包匹配的版本号。

可在以下 project.json 示例中看到修补程序更新。

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.1"
  },
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

### <a name="shipping-a-minor-release"></a>传送次要发布

传送 .NET Core v1.0.0 稳定版本后，将新的 API 添加到 .NET Core 库以启用新方案。 更新各种元包以引用更新的 .NET Core 库包。 将元包作为修补程序更新 (x.y) 进行版本控制，以匹配更高的框架版本。 更新各种框架以描述新的 API。 发布新的 .NET Core 分发，其具有与 `Microsoft.NETCore.App` 元包匹配的版本号。

可在以下 project.json 示例中看到显示的次要更新。

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.1.0"
  },
  "frameworks": {
    "netcoreapp1.1": {}
  }
}
```

### <a name="shipping-a-major-release"></a>传送主要发布

给定 .NET Core v1.y.z 稳定版本，将新的 API 添加到 .NET Core 库以启用主要新方案。 也许，已放弃对平台的支持。 更新各种元包以引用更新的 .NET Core 库包。 `Microsoft.NETCore.App` 元包和 `netcore` 框架作为主要更新 (x.) 进行版本控制。 `NETStandard.Library` 元包可能作为次要更新 (x.y) 进行版本控制，因为其适用于多个 .NET 实现。 将发布新的 .NET Core 分发，其具有与 `Microsoft.NETCore.App` 元包匹配的版本号。

可在以下示例的 project.json 元包引用中查看显示的主要更新。

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "2.0.0"
  },
  "frameworks": {
    "netcoreapp2.0": {}
  }
}
```

