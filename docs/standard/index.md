---
title: "关于 .NET"
description: "了解 .NET 平台。"
keywords: .NET, .NET Core
author: richlander
ms.author: ronpet
ms.date: 10/31/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: be44dce8181be45f6d73fcf498a873fb94aa56a6
ms.lasthandoff: 03/02/2017

---

# <a name="net-platform-guide"></a>.NET 平台指南

> [!NOTE]
这篇文章将重写。

> 请查看[“.NET Core 入门”教程](../core/getting-started.md)，了解如何创建简单的 .NET Core 应用程序。 只需几分钟即可生成并运行第一个应用。

.NET 是一个通用开发平台。 在使用通用解决方案的任何类型的应用或工作负荷中，都可以使用 .NET。 .NET 提供很多开发人员都会感兴趣的一些重要功能，包括自动内存管理和现代编程语言，可方便开发人员有效构建优质应用程序。 .NET 允许具有许多便利功能的高级编程环境，同时提供对本机内存和 API 的底层访问。

C#、F# 和 Visual Basic 是面向并依赖 .NET 平台的热门语言。 .NET 语言因其异步编程模型、语言集成查询、泛型类型和类型系统反射等主要功能而闻名。 该语言也是面向对象和功能性编程范例的不错选择。

这些语言在理念和语法，以及共享类型系统所提供的对称方面存在诸多差异。 此类型系统由基础运行时环境提供。 .NET 围绕“公共语言运行时”理念设计，支持多种语言要求（例如，动态和静态类型的语言），并可实现语言间的互操作性。 例如，可以在语言之间传递 `People` 对象集合，且不丢失语义或功能。

.NET 基于指定平台的基本要素的开放式 [.NET 标准](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)，提供多种 [.NET 实现和产品](components.md)。 这些实现和产品已针对不同的应用程序类型（例如桌面、移动、游戏和云）进行单独优化，支持多种芯片（例如 x86/x64 和 ARM）和操作系统（例如 Windows、Linux、iOS、Android 和 macOS）。 开放源代码也是 .NET 生态系统的重要组成部分，其中包含多种 .NET 实现和许多的库，购买 OSI 批准的许可证后即可使用这些库。

- 了解 [C#](../csharp/index.md)
- 了解 [F#](../fsharp/index.md)
- 浏览 [.NET API 库](../../api/index.md)
- [公共语言运行时简介](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/intro-to-clr.md)

<a name="fundamentals"></a>基础知识
------------

**多语言** - .NET 提供可由多种语言使用的明确定义的类型系统、文件格式、运行时、框架和工具，目的是为了实现自身执行，同时与使用共享货币所用的 .NET 组件的语言进行互操作。

**托管内存** - .NET 通过垃圾回收器自动为你管理内存。 确保你能始终引用活动对象，保证避免缓冲区溢出和访问冲突等棘手问题。 这包括数组边界检查。

**类型安全性** -- 功能和内存表现形式的主 .NET 模型为“类型”。 类型可定义形状和行为（可选）。 运行时确保调用代码根据其定义和指定的成员可见性，仅对类型执行操作，从而提供一致、可靠、安全的结果。

<a name="features"></a>功能
--------

**用户定义的值类型** - 值类型是类型的实用类别，因为它们提供“按值传递”而非“按引用传递”的语义，与类的情况类似。 值类型对于数值数据特别有用。 .NET 允许基元类型（如整数）和用户定义的类型使用值类型。

**泛型类型** - 泛型类型是包含一个或多个类型参数的类型，具体情况可根据每次实例化进行指定。 这可用于多种类型，在其他情况下，还会将内容公开为 Object 类型或需要多个类型定义。 例如，集合类型的给定实例化可能特定于人员、GPS 位置或字符串。

**反射** - .NET 定义元数据格式，该格式用于描述二进制文件中的类型。 反射子系统使用此数据公开在运行时读取和实例化类型的 API。 此功能非常适用于不方便预先了解某程序的确切实现的动态方案。

**灵活的代码生成** - .NET 不指定将 .NET 二进制文件转换为机器码的特定方法。 已成功使用多种方法，包括转译、实时 (JIT) 编译以及有/无实时回退的预编译。 以上每种策略都很有用，并存在共同使用这些策略的情况。

**跨平台** - .NET 自推出之日起便已支持跨平台。 二进制格式和指令集包括操作系统、CPU 并与指针大小无关。 2000 年生成的在 32 位 Windows 计算机上运行的给定 .NET 二进制文件无需修改即可在 2016 ARM64 iOS 设备上运行。

<a name="open-source"></a>打开源
-----------

.NET 的 [.NET Core](https://github.com/dotnet/core) 和 [Mono](https://github.com/mono/mono) 实现是使用 MIT 许可证的开放源代码。 文档使用[知识共享 CC-BY](https://creativecommons.org/licenses/by/4.0/)许可证。 .NET Core 和 Mono 由 Microsoft 提供赞助，并拥有许多来自社区的参与者。 

这些通用运行时可用作学术研究、教学/学习或者商业产品的基础。 其开放性还意味着只要产品存在 bug 或用户渴求新功能，任何人都可以向上游产品代码提供反馈。

<a name="projects"></a>项目
--------

- [CoreCLR](https://github.com/dotnet/coreclr) - .NET 运行时，适用于 .NET Core。
- [Mono](https://github.com/mono/mono) - .NET 运行时，适用于 Xamarin 和其他环境。
- [CoreFX](https://github.com/dotnet/coreclr) - .NET 类库，适用于 .NET Core 和 Mono（Mono 在某种程度上通过源共享使用）。
- [Roslyn](https://github.com/dotnet/roslyn) - C# 和 Visual Basic 编译器，适用于大多数 .NET 平台和工具。 公开用于读取、编写和分析源代码的 API。
- [F#](https://github.com/microsoft/visualfsharp) - F# 编译器。
- [Xamarin SDK](http://open.xamarin.com) - 采用 C# 和 F# 编写 Android、iOS 和 macOS 所需的工具和库。

<a name="standardized"></a>标准化
------------

通过打开 [ECMA 标准](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)指定 .NET，该标准概述了其功能，并可用于开发新实现。 还有其他 .NET 实现，除了 Microsoft 实现外，最热门的是 Mono 和 Unity。


