---
title: ".NET 体系结构组件"
description: "描述主要的 .NET 体系结构组件，例如 .NET 标准库、.NET 运行时和工具。"
keywords: ".NET, .NET 标准库, .NET Standard, .NET Core, .NET Framework, Xamarin, MSBuild, C#, F#, VB, 编译器"
author: cartermp
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 2e38e9d9-8284-46ee-a15f-199adc4f26f4
translationtype: Human Translation
ms.sourcegitcommit: 254e89abefd28419bd2f36a047e4df939f7ff8da
ms.openlocfilehash: d0cd8f44876038167db23e7fd1e5a893460f3d73

---

# <a name="net-architectural-components"></a>.NET 体系结构组件

.NET 由多个主要组件组成。  它具有一个名为 .NET 标准库的标准库，该标准库是一个可随处运行的大型 API 集。  该标准库由三个 .NET 运行时实现，即 NET Framework、.NET Core 和 Mono for Xamarin。  .NET 语言还在任何 .NET 运行时上运行。  此外，还可以通过每个平台上的一些工具生成项目。  无论选择何种运行时，这些工具都相同。

此处是每个先前提及的 .NET 组件以及其组合方式的图示概述。

![所有 .NET 体系结构组件组合在一起](media/components.png)

然后是上面所示的每个主要组件的简要说明。  

## <a name="net-standard-library"></a>.NET 标准库

.NET 标准库是一组由 .NET 运行时实现的 API。

更正式地说，它是构成协定统一集（这些协定是编写代码的依据）的特定 .NET API 组。  这些协定对每个 .NET 运行时都具有基础实现。  这可跨不同的 .NET 运行时实现可移植性，以使代码可有效地“随处运行”。

.NET 标准库还是一个生成目标，这时被称作 .NET 标准。  当前可面向 NET Standard 1.0-1.6。  如果代码面向 .NET Standard 版本，则可确保其可在实现该版本的任意 .NET 运行时上运行。

若要了解有关 .NET 标准库和面向 .NET 标准的详细信息，请参阅 [.NET 标准库](library.md)。

## <a name="net-runtimes"></a>.NET 运行时

Microsoft 积极开发和维护的主要 .NET 运行时有 3 个：.NET Core、.NET Framework 和 Mono for Xamarin。

### <a name="net-core"></a>.NET 核心

.NET Core 是一个经优化用于服务器工作负荷的跨平台运行时。  它实现 .NET 标准库，这意味着任何面向 .NET 标准的代码都可在 .NET Core 上运行。  它是 ASP.NET Core 和通用 Windows 平台 (UWP) 所使用的运行时。  它新式、高效，专用于处理大规模的服务器和云工作负荷。

若要了解有关 .NET Core 的详细信息，请参阅 [.NET Core 指南](../core/index.md)。

### <a name="net-framework"></a>.NET Framework

.NET Framework 是自 2002 年就已存在的历史 .NET 运行时。  它是现有的 .NET 开发人员经常使用的 .NET Framework。  它实现 .NET 标准库，这意味着任何面向 .NET 标准的代码都可在 NET Framework 上运行。  它还包含一些特定于 Windows 的 API，如通过 Windows 窗体和 WPF 进行 Windows 桌面开发的 API。  .NET Framework 非常适合用于生成 Windows 桌面应用程序。

若要了解有关 .NET Framework 的详细信息，请参阅 [.NET Framework 指南](../framework/index.md)。

### <a name="mono-for-xamarin"></a>Mono for Xamarin

Mono 是 Xamarin 应用所使用的运行时。  它实现 .NET 标准库，这意味着任何面向 .NET 标准的代码都可在 Xamarin 应用上运行。  它包含其他适用于 iOS、Android、Xamarin.Forms 和 Xamarin.Mac 的 API。  Mono for Xamarin 非常适合生成 iOS 和 Android 移动应用程序。

若要了解有关 Mono 的详细信息，请参阅 [Mono 文档](http://www.mono-project.com/docs/)。

## <a name="net-tooling-and-common-infrastructure"></a>.NET 工具和常见基础结构

.NET 工具在每个 .NET 实现中也很常见。  其中包括（但不限于）：

* .NET 语言及其编译器
* 运行时组件，例如 JIT 和垃圾回收器
* .NET 项目系统（有时称为“csproj”、“vbproj”或“fsproj”）
* MSBuild（用于生成项目的生成引擎）
* NuGet（适用于.NET 的 Microsoft 程序包管理器）
* .NET CLI（用于生成 .NET 项目的跨平台命令行接口）
* 开放源生成业务流程工具，例如 CAKE 和 FAKE

此处的要点应该是有大量的工具和基础结构可满足选择用来生成应用的任何“风格”的 .NET。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅以下内容：

* [.NET 标准库](library.md)
* [.NET Core 指南](../core/index.md)
* [.NET Framework 指南](../framework/index.md)
* [C# 指南](../csharp/index.md)
* [F# 指南](../csharp/index.md)
* [VB.NET 指南](../csharp/index.md)


<!--HONumber=Nov16_HO3-->


