---
title: ".NET 教程"
description: ".NET 平台的一些重要功能指导教程。"
keywords: ".NET, .NET Core, 教程, 编程语言, 不安全, 内存管理, 类型安全, 异步"
author: cartermp
ms.author: wiwagn
ms.date: 02/09/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
translationtype: Human Translation
ms.sourcegitcommit: 48563be13dc07000ced2e6817b3028e6117abd93
ms.openlocfilehash: ee6ced104137a453267b409fea05716d781ef83f
ms.lasthandoff: 03/22/2017

---

# <a name="tour-of-net"></a>.NET 教程

.NET 是一个通用开发平台。  它具有几项关键功能，例如多种编程语言、异步和并发编程模型以及本机互操作性，可以支持跨多个平台的各种方案。

本文还提供了 .NET 平台的一些关键功能的指导教程。

请参阅 [.NET 体系结构组件](components.md)，了解 .NET 的每个体系结构“部分”及其用途。

## <a name="how-to-run-the-code-samples"></a>如何运行代码示例

要了解如何设置开发环境以运行代码示例，请查看[入门](getting-started.md)。  可以将代码示例从此页复制并粘贴到你的环境中以执行它们。 

> [!NOTE]
将来，本文档站点能够在浏览器中运行这些代码示例。

## <a name="programming-languages"></a>编程语言

.NET 支持多种编程语言。  .NET 运行时实现[公共语言基础结构 (CLI)](https://www.visualstudio.com/license-terms/ecma-c-common-language-infrastructure-standards/)，其中（除其他事项外）指定与语言无关的运行时和语言互操作性。  这意味着可以选择任何 .NET 语言在 .NET 上生成应用和服务。

Microsoft 积极开发和支持三种 .NET 语言：C#、F# 和 Visual Basic .NET。 

* C# 是一种简单、强大、类型安全、面向对象的语言，同时保留了 C 语言的表达力度和简洁性。 熟悉 C 和类似语言的任何人在适应 C# 的过程中几乎不会遇到什么问题。  请查看 [C# 指南](../csharp/index.md)，了解有关 C# 的详细信息。

* F# 是一种跨平台、功能优先的编程语言，它也支持传统的面向对象的编程和命令式编程。  请查看 [F# 指南](../fsharp/index.md)，了解有关 F# 的详细信息。

* Visual Basic 是一种简单易学的语言，可用于构建在 .NET 上运行的各种应用程序。

## <a name="automatic-memory-management"></a>自动内存管理

.NET 使用[垃圾回收](garbagecollection/index.md)为程序提供自动内存管理。  GC 以一种“懒散”的方式进行内存管理，它优先考虑应用程序吞吐量，而不是立即回收内存。  要了解有关 .NET GC 的详细信息，请查看[垃圾回收 (GC) 的基础](garbagecollection/fundamentals.md)。

以下两行代码都会分配内存：

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L1-L2)]

无法使用任何类似的关键字来取消分配内存，因为当垃圾回收器通过其计划的运行规则回收内存时，会自动发生取消分配。

垃圾回收站只是一种帮助确保*内存安全*的服务。  内存安全的固定条件非常简单：如果某个程序仅访问分配的内存（未释放），则该程序就是内存安全的。  例如，运行时可确保程序编制索引的范围不超过数组末尾，且确保其仅访问对象范围内的虚构字段。

下例中，运行时将引发 `InvalidIndexException` 异常，强制确保内存安全。

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L4-L5)]

## <a name="working-with-unmanaged-resources"></a>处理未托管的资源

部分对象会引用*未托管的资源*。 未托管的资源是指不由 .NET 运行时自动维护的资源。  例如，文件句柄就是未托管的资源。  @System.IO.FileStream 对象是一个托管对象，但它引用未托管的文件句柄。  用完文件流之后，需要释放文件句柄。

在 .NET 中，引用未托管资源的对象会实现 @System.IDisposable 接口。  用完对象后，需调用此对象的 @System.IDisposable.Dispose 方法，该方法会释放所有为托管的资源。  .NET 语言为此类对象提供了一种便捷的 `using` 语法，如下例所示：

[!code-csharp[UnmanagedResources](../../samples/csharp/snippets/tour/UnmanagedResources.csx#L1-L6)]

`using` 块完成后，.NET 运行时将自动调用 `stream` 对象的 @System.IDisposable.Dispose 方法，该方法会释放文件句柄。  如果某异常造成控件退出块，则运行时也会执行此操作。

有关详细信息，请参阅以下页面：

* [Using 语句](../csharp/language-reference/keywords/using-statement.md)（针对 C#）
* [资源管理：`use` 关键字](../fsharp/language-reference/resource-management-the-use-keyword.md)（针对 F#）
* [Using 语句](../visual-basic/language-reference/statements/using-statement.md)（针对 Visual Basic）

## <a name="type-safety"></a>类型安全

对象按类型分配。 给定对象允许的唯一操作及其消耗的内存都属于特定的类型。 `Dog` 类型可能具有 `Jump` 和 `WagTail` 方法，但不太可能有 `SumTotal` 方法。 程序只能调用给定类型的声明方法。 其他所有调用将导致编译时错误或运行时异常（如果使用动态功能或 `object`）。

.NET 语言面向对象，包含基类和派生类的层次结构。 .NET 运行时仅允许与对象层次结构相符的对象强制转换和调用。 请记住，任何 .NET 语言中定义的每个类型都派生自 `object` 基类型。

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L18-L23)]

使用类型安全还有助于强制实施封装，因为它可以保证访问器关键字的保真度。 访问器关键字是控制其他代码访问给定类型的成员的项目。 这些关键字通常用于某个类型中用来管理类型行为的各种数据。

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L3-L3)]

C#、Visual Basic 和 F# 支持本地**类型推理**。 类型推理是指编译器根据右侧的表达式推断左侧表达式的类型。 这并不意味着类型安全遭到破坏或规避。 生成的类型**具有**一个隐含所有信息的强类型。 让我们重新编写上述示例中的前两行代码，以便于介绍类型推理。 注意，该示例的余下内容完全相同。

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L28-L34)]

与在 C# 和 Visual Basic 中找到的方法本地类型推理相比，F# 的类型推理能力更强。  若要了解详细信息，请查看[类型推理](../fsharp/language-reference/type-inference.md)。

## <a name="delegates-and-lambdas"></a>委托和 lambda

委托类似于 C++ 函数指针，一个重要差别在于，它们是类型安全的。 它们是 CLR 类型系统中某种断开连接的方法。 正则方法已连接到某个类，只能通过静态或实例调用约定来直接调用。

委托可在 .NET 领域的各种 API 和场合中使用，尤其是通过 lambda 表达式（LINQ 的基石）使用。

在[委托和 lambda](delegates-lambdas.md) 文档中了解有关委托的详细信息。

## <a name="generics"></a>泛型

泛型是 .NET Framework 2.0 中的新增功能。 简而言之，泛型可让程序员在设计类时引入一个“类型参数”，这样，客户端代码（类型的用户）便可以指定要使用哪个确切的类型来取代类型参数。

添加泛型的目的是帮助程序员实现通用数据结构。 在泛型问世之前，举例来说，要将 `List` 类型用作泛型，必须处理 `object` 类型的元素。 这就会造成各种性能和语义问题，更不必说那些微妙的运行时错误。 例如，当数据结构包含整数和字符串时，如果在处理列表的成员时引发 `InvalidCastException`，则就会出现运行时错误这种非常棘手的问题。

以下示例显示了使用 @System.Collections.Generic.List%601 类型实例运行的基本程序。

[!code-csharp[GenericsShort](../../samples/csharp/snippets/tour/GenericsShort.csx)]

有关详细信息，请参阅[泛型类型（泛型）概述](generics.md)一文。

## <a name="async-programming"></a>异步编程

异步编程是 .NET 中的一个先进概念，它在运行时、框架库和 .NET 语言构造中提供异步支持。 在内部，异步编程基于利用操作系统尽可能高效地执行 I/O 绑定型作业的对象（例如 `Task`）。

若要了解有关 .NET 中异步编程的详细信息，请先阅读[异步概述](async.md)。

## <a name="language-integrated-query-linq"></a>语言集成查询 (LINQ)

LINQ 是适用于 C# 和 VB 的强大功能集，可用于编写简单的声明性代码来处理数据。 数据可以采用多种形式（例如，内存中对象、位于 SQL 数据库或 XML 文档中），但针对每个数据源编写的 LINQ 代码看上去往往没有差别！

若要了解详细信息和查看示例，请参阅 [LINQ（语言集成查询）](using-linq.md)。

## <a name="native-interoperability"></a>本机互操作性

当前使用的每种操作系统为各种编程任务提供了众多的平台支持。 .NET 可让用户以多种方式利用这些 API。 总而言之，这种支持称为“本机互操作性”。本部分将会探讨如何从托管的 .NET 代码访问本机 API。

实现本机互操作性的主要方式是使用“平台调用”，简称 P/Invoke。 所有 Linux 和 Windows 平台都在 .NET Core 中提供了这项支持。 实现本机互操作性的另一种方式称为“COM 互操作”（仅限 Windows），用于在托管代码中操作 [COM 组件](https://msdn.microsoft.com/library/bwa2bx93.aspx)。 这种方式建立在 P/Invoke 基础结构之上，但工作原理略有不同。

针对 Java 和 Objective-C 的 Mono（以及 Xamarin）互操作性支持基本上以类似的方式构建，也就是说，它们运用相同的原理。

有关详细信息，请阅读[本机互操作性](native-interop.md)文档。

## <a name="unsafe-code"></a>不安全代码

使用 CLR 可以通过 `unsafe` 代码访问本机内存和执行指针算法。 某些算法和系统互操作性需要这些操作。 尽管不安全代码的功能强大，但除非有必要与系统 API 互操作或实现最高效的算法，否则不建议使用。 在不同的环境中，不安全代码的执行方式可能不同，使用它还会丧失垃圾回收器和类型安全带来的好处。 建议尽可能地限制和集中化使用不安全代码，并全面测试该代码。

以下示例是 `StringBuilder` 类中 `ToString()` 方法的修改版本。  它演示了如何使用 `unsafe` 代码直接移动内存区块，从而有效实现某种算法：

[!code-csharp[Unsafe](../../samples/csharp/snippets/tour/Unsafe.csx)]

## <a name="next-steps"></a>后续步骤

如果对 C# 功能的教程感兴趣，请参阅 [C# 教程](../csharp/tour-of-csharp/index.md)。

如果对 F# 功能的教程感兴趣，请参阅 [F# 教程](../fsharp/tour.md)。

如果想开始自己编写代码，请参阅[入门](getting-started.md)。

要了解 .NET 的重要组件，请参阅 [.NET 体系结构组件](components.md)。

