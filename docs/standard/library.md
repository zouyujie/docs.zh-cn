---
title: ".NET 标准库"
description: ".NET 标准库"
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c044882c-af15-45f2-96d1-534557a5ee9b
translationtype: Human Translation
ms.sourcegitcommit: 633dcc6d966125139cb21c4e70dac4d4794ee9a4
ms.openlocfilehash: da326fb823c16c7795a6a05ad302c13918b435aa
ms.lasthandoff: 03/20/2017

---

# <a name="net-standard-library"></a>.NET 标准库

.NET 标准库是一套正式的 .NET API 规范，有望在所有 .NET 运行时中推出。 推出标准库的动机是在 .NET 生态系统中建立更好的统一性。 [ECMA 335](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) 持续为 .NET 运行时行为建立统一性，但适用于 .NET 库实现的 .NET 基类库 (BCL) 没有类似的规范。 

.NET 标准库可实现以下重要方案： 

- 为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL API。
- 使开发人员能够通过同一组 API 生成可在各种 .NET 运行时中使用的、可移植的库。
- 减少并有望消除由于 .NET API 方面的原因而对共享源代码的条件性编译（仅适用于 OS API）。

各种 .NET 运行时可实现特定版本的 .NET 标准库。 每个 .NET 运行时版本将会公布它所支持的最高 .NET Standard 版本，这种声明意味着它也支持以前的版本。 例如，.NET Framework 4.6 实现 .NET 标准库 1.3，这意味着它会公开在 .NET 标准库版本 1.0 到 1.3 中定义的所有 API。 同理，.NET Framework 4.6.2 实现 .NET 标准库 1.5，.NET Core 1.0 实现 .NET 标准库 1.6。

## <a name="net-platforms-support"></a>.NET 平台支持

下表显示了支持 .NET 标准库的整套 .NET 运行时。

| 平台名称 | Alias |  |  |  |  |  | | | |
| :---------- | :--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|.NET Standard | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1.5 | 1.6 | 2.0 |
|.NET 核心|netcoreapp|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|1.0|2.0|
|.NET Framework|net|&rarr;|4.5|4.5.1|4.6|4.6.1|4.6.2|vNext|4.6.1|
|Mono/Xamarin 平台||&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|vNext|
|通用 Windows 平台|uap|&rarr;|&rarr;|&rarr;|&rarr;|10.0|&rarr;|&rarr;|vNext|
|Windows|win|&rarr;|8.0|8.1||||||
|Windows Phone|wpa|&rarr;|&rarr;|8.1||||||
|Windows Phone Silverlight|wp|8.0||||||||

## <a name="comparison-to-portable-class-libraries"></a>与可移植类库的比较

可将 .NET 标准库视为下一代[可移植类库 (PCL)](https://msdn.microsoft.com/library/gg597391.aspx)。 .NET 标准库可对标准 BCL 进行组织，从而在各种 .NET 运行时之间建立更好的统一性，改善创建可移植库的体验。 面向 .NET 标准库的库是一个 PCL 或“基于 .NET Standard 的 PCL”。 现有 PCL 是“基于配置文件的 PCL”。

.NET 标准库和 PCL 配置文件是针对类似目的创建的，但在一些重要的方面也存在差异。

类似之处：

- 定义可用于二进制代码共享的 API。

差异：

- .NET 标准库是一套组织有序的 API，而 PCL 配置文件由现有平台的交集定义。
- .NET 标准库的版本线性递增，而 PCL 配置文件则不是这样。
- PCL 配置文件代表 Microsoft 平台，而 .NET 标准库与平台无关。

## <a name="specification"></a>规范

.NET 标准库规范是一组标准化的 API。 该规范由 .NET 运行时实现者（具体而言，是 Microsoft（包括.NET Framework、NET Core 和 Mono）和 Unity）维护。 在建立新 .NET 标准库版本的过程中，将使用公众反馈流程。

### <a name="official-artifacts"></a>正式项目

正式规范是一套 .cs 文件，定义标准中包含的 API。 每个[组件](https://github.com/dotnet/corefx/tree/master/src)的 [ref 目录](https://github.com/dotnet/corefx/tree/master/src/System.Runtime/ref)定义 .NET 标准库 API。 尽管 ref 项目位于 [CoreFX 存储库](https://github.com/dotnet/corefx)中，但它们并不特定于 .NET Core。

[NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) 元包（[源代码](https://github.com/dotnet/standard/blob/master/netstandard/pkg/NETStandard.Library.dependencies.props)）描述用于部分定义一个或多个 .NET 标准库版本的库集。

给定的组件（例如 System.Runtime）描述：

- .NET 标准库的一部分（只限其范围）。
- .NET 标准库在该范围内的多个版本。

标准库提供派生项目以方便读取，并实现某些开发人员方案（例如，使用编译器）。

- Markdown 中的 API 列表（待提供）
- 引用程序集，以 [NuGet 包](../core/packages.md)的形式分发，由 [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/) 元包引用。

### <a name="package-representation"></a>包表示形式

.NET 标准库引用程序集的主要分发载体是 [NuGet 包](../core/packages.md)。 实现将以适用于每个 .NET 运行时的各种方式提供。

NuGet 包面向一个或多个[框架](frameworks.md)。 .NET 标准库包面向“.NET Standard”框架。 可以使用 `netstandard` [精简 TFM](frameworks.md)（例如 `netstandard1.4`）来指定 .NET Standard 框架作为目标。 如果构建的库将在多个运行时中运行，就应将此框架作为目标。 

`NETStandard.Library` 元包引用定义 .NET 标准库的整套 NuGet 包。  要指定 `netstandard` 作为目标，最常见的方法是引用此元包。 它描述并提供了约&40; 个 .NET 库并与 .Net 标准库所定义的 API 相关联。 可以引用以 `netstandard` 为目标的其他包来使用其他 API。 

### <a name="versioning"></a>版本管理

该规范并不是单一的，而是版本不断线性递增的 API 集。 该标准的第一个版本建立了一组基准 API。 后续版本将添加 API，并继承以前的版本定义的 API。 在从标准中移除 API 方面，并没有成文的规定。

.NET 标准库并不特定于任何一种 .NET 运行时，也不与其中任一运行时的版本方案相匹配。

添加到任何运行时（例如 .NET Framework、.NET Core 和 Mono）的 API 可被视为适合添加到规范中的候选项，尤其是本质上非常重要的 API。 [.NET 标准库的新版本](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md#list-of-net-corefx-apis-and-their-associated-net-platform-standard-version)是基于 .NET 运行时版本创建的，因此，可以从 .NET Standard PCL 指定新 API 的目标。 [.NET Core 版本控制](../core/versions/index.md)中更详细介绍了版本控制机制。

.NET 标准库版本控制对于库的使用至关重要。 在获得 .NET 标准库版本的情况下，可以使用面向相同或更低版本的库。 以下做法描述了有关使用 .NET 标准库 PCL（具体而言，指定 .NET 标准库的目标）的工作流。

- 选择要用于 PCL 的 .NET 标准库版本。
- 使用依赖于相同或更低 .NET 标准库版本的库。
- 如果发现某个库依赖于更高的 .NET 标准库版本，则需要采用与此相同的版本，或者不要使用该库。

### <a name="pcl-compatibility"></a>PCL 兼容性

.NET 标准库与一部分 PCL 配置文件兼容。 .NET 标准库 1.0、1.1 和 1.2 与一组 PCL 配置文件重叠。 这种重叠是由以下两个原因产生的：

- 使基于 .NET Standard 的 PCL 能够引用基于配置文件的 PCL。
- 使基于配置文件的 PCL 能够打包为基于 .NET Standard 的 PCL。

基于配置文件的 PCL 兼容性由 [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) NuGet 包提供。 引用包含基于配置文件的 PCL 的 NuGet 包时，需要这种依赖性。

与以常规方式打包的基于配置文件的 PCL 相比，打包为 `netstandard` 的基于配置文件的 PCL 更易于使用。 `netstandard` 打包符合现有用户的需要。

下面列出了与 .NET Standard 兼容的 PCL 配置文件集： 

| 配置文件 | .NET 平台标准版本 |
| ---------| --------------- |
| Profile7 .NET 可移植子集（.NET Framework 4.5、Windows 8） | 1.1 |
| Profile31 .NET 可移植子集（Windows 8.1、Windows Phone Silverlight 8.1）| 1.0 |
| Profile32 .NET 可移植子集（Windows 8.1、Windows Phone 8.1） | 1.2 |
| Profile44 .NET 可移植子集（.NET Framework 4.5.1、Windows 8.1） | 1.2 |
| Profile49 .NET 可移植子集（.NET Framework 4.5、Windows Phone Silverlight 8） | 1.0 |
| Profile78 .NET 可移植子集（.NET Framework 4.5、Windows 8、Windows Phone Silverlight 8） | 1.0 |
| Profile84 .NET 可移植子集（Windows Phone 8.1、Windows Phone Silverlight 8.1） | 1.0 |
| Profile111 .NET 可移植子集（.NET Framework 4.5、Windows 8、Windows Phone 8.1） | 1.1 |
| Profile151 .NET 可移植子集（.NET Framework 4.5.1、Windows 8.1、Windows Phone 8.1） | 1.2 |
| Profile157 .NET 可移植子集（Windows Phone 8.1、Windows Phone 8.1、Windows Phone Silverlight 8.1） | 1.0 |
| Profile259 .NET 可移植子集（Windows Phone 4.5、Windows 8、Windows Phone 8.1、Windows Phone Silverlight 8） | 1.0 |

## <a name="targeting-net-standard-library"></a>指定 .NET 标准库的目标

可以结合使用 `netstandard` 框架和 NETStandard.Library 元包来[构建.NET 标准库](../core/tutorials/libraries.md)。 查看[使用.NET Core 工具指定 .NET 标准库目标](../core/packages.md)的示例。

