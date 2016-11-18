---
title: "正则表达式中的编译和重复使用"
description: "正则表达式中的编译和重复使用"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3adea434-e2ed-4023-b4f5-b0608b4cf53f
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: e14e386a04c64726e4eacb63dc8855a356a18ba0

---

# <a name="compilation-and-reuse-in-regular-expressions"></a>正则表达式中的编译和重复使用

通过了解正则表达式引擎编译表达式的方式以及正则表达式的缓存方式，可以优化大量使用正则表达式的应用程序的性能。 本主题介绍编译和缓存。

## <a name="compiled-regular-expressions"></a>已编译的正则表达式

默认情况下，正则表达式引擎将正则表达式编译成内部指令序列（这些指令序列是不同于 Microsoft 中间语言 (MSIL) 的高级代码）。 当引擎执行正则表达式时，会解释内部代码。

如果 [Regex](xref:System.Text.RegularExpressions.Regex) 对象是通过 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 选项构造的，则它会将正则表达式编译为显式 MSIL 代码，而不是高级正则表达式内部指令。 这样，.NET 的实时 (JIT) 编译器便可以将表达式转换为本机代码以获得更高的性能。

但是，生成的 MSIL 不能卸载。 卸载代码的唯一方法是卸载整个应用程序域（即，卸载应用程序的所有代码）。 实际上，一旦使用 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 选项编译正则表达式，.NET 就永远不会释放由编译的表达式使用的资源，即使创建该正则表达式的 [Regex](xref:System.Text.RegularExpressions.Regex) 对象本身已被释放并进行了垃圾回收，也是如此。

必须注意限制使用 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 选项编译的不同正则表达式的数目，避免消耗过多的资源。 如果应用程序必须使用较大数量或极大数量的正则表达式，应该解释每个表达式，而不要编译它们。 但是，如果重复使用数目较少的正则表达式，则应使用 [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) 来编译它们，以获得更好的性能。 

## <a name="the-regular-expressions-cache"></a>正则表达式缓存

为了提高性能，正则表达式引擎为已编译的正则表达式维护了一个应用程序范围的缓存。 该缓存只存储静态方法调用中使用的正则表达式模式。 （不缓存提供给实例方法的正则表达式模式。）这样，在每次使用正则表达式时，就无需将正则表达式重新分析成高级字节代码。

缓存的正则表达式的最大数目由 `static`（在 Visual Basic 中为 `Shared`）[Regex.CacheSize](xref:System.Text.RegularExpressions.Regex.CacheSize) 属性的值决定。 默认情况下，正则表达式引擎最多可缓存 15 个已编译的正则表达式。 如果已编译正则表达式的数目超过缓存大小，则丢弃最早使用的正则表达式并缓存新的正则表达式。 

应用程序可通过以下两种方式之一来利用预编译的正则表达式：

* 使用 [Regex](xref:System.Text.RegularExpressions.Regex) 对象的静态方法定义正则表达式。 如果要使用的正则表达式模式已在其他静态方法调用中定义，则正则表达式引擎将从缓存中检索该模式。 如果不是这样，则引擎将编译正则表达式并将其添加到缓存中。

* 重复使用现有的 [Regex](xref:System.Text.RegularExpressions.Regex) 对象（在需要使用其正则表达式模式时）。


由于对象实例化和正则表达式编译会产生大量的系统开销，因此创建大量 [Regex](xref:System.Text.RegularExpressions.Regex) 对象并迅速销毁它们的过程将占用大量资源。 对于使用大量不同正则表达式的应用程序，可通过调用静态方法 [Regex](xref:System.Text.RegularExpressions.Regex) 并尽量增加正则表达式缓存的大小来优化其性能。

## <a name="see-also"></a>另请参阅

[.NET 正则表达式](regular-expressions.md)




<!--HONumber=Nov16_HO3-->


