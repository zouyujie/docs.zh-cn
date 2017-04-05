---
title: "垃圾回收"
description: "垃圾回收"
keywords: ".NET、.NET Core"
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.devlang: dotnet
ms.assetid: db39a0f5-e363-490f-a7e6-adb9a6ff2a8c
translationtype: Human Translation
ms.sourcegitcommit: ffc0530b2263db0e073f351aac2d539de6701ead
ms.openlocfilehash: 4646a7e8c75315bb1a13bc5fddecd77888f6ae69
ms.lasthandoff: 04/05/2017

---

# <a name="garbage-collection"></a>垃圾回收

垃圾回收功能是 .NET 托管代码平台最重要的功能之一。 垃圾回收器 (GC) 负责分配和释放内存。 无需了解如何分配和释放内存，也无需管理使用该内存的对象的生命周期。 新建对象或对值类型进行装箱时，即生成分配。 分配通常非常迅速。 当没有足够内存来分配对象时，GC 必须收集并释放垃圾内存，使得新分配能够使用内存。 此过程称为“垃圾回收”。

垃圾回收器用作自动内存管理器。 它提供如下优点：

*   使你可以在开发应用程序时不必释放内存。
*   有效分配托管堆上的对象。
*   回收不再使用的对象，清除它们的内存，并保留内存以用于将来分配。 托管对象会自动获取干净的内容来开始，因此，它们的构造函数不必对每个数据字段进行初始化。
*   通过确保对象不能使用另一个对象的内容来提供内存安全。

.NET GC 分为 3 代。 每一代各有其用于存储所分配对象的堆。 基本原则是，大多数对象不是短期存在就是长期存在的。 首先在第 0 代分配对象。 对象存在的时间通常不超过第 1 代，因为下一次垃圾回收时已不再使用这些对象（超出使用范围）。 第 0 代回收垃圾速度很快，因为与其关联的堆很小。 第 1 代实际上是第二次机会空间。 短期存在而（通常由于时机巧合）被第 0 代回收保留的对象进入第 1 代\.。第 1 代回收的速度也很快，因为与其关联的堆也很小。 前两个对较小是因为它们只收集对象会或将对象提升到下一代的堆。 所有长期存在的对象都处于第 2 代。 第 2 代的堆可以变得非常庞大，因为它包含的对象可能在很长时间内存在，并且不存在第 3 代堆来进一步提升对象。

GC 具有用于大型对象的附加堆，称为大型对象堆 (LOH)。 该堆保留用于收集 85,000 字节或更大的对象。 含有 85,000 个元素的字节数组 (Byte[]) 是大型对象的一个示例。 大型对象不会分配到各代的堆，而是直接分配到 LOH。

对于运行了较长时间或对大量数据进行操作的程序，第 2 代和 LOH 回收可能花费较长时间。 已知大型服务器程序拥有数十 GB 的堆。 GC 会运用各种技术，缩短其阻止程序运行的时间。 主要方法是通过后台线程，以不干扰程序执行的方式进行尽可能多的垃圾回收工作。 GC 向开发人员提供了几种可影响其行为的方法，对于提高性能十分有用。

## <a name="related-topics"></a>相关主题

标题 | 描述
----- | ----------- 
[自动内存管理和垃圾回收](gc.md) | 介绍 .NET 中内存管理的基本概念
[垃圾回收的基本知识](fundamentals.md) | 描述垃圾回收的工作原理、如何在托管堆上分配对象，以及其他核心概念。
[已引发回收](induced.md) | 描述如何完成垃圾回收。
[延迟模式](latency.md) | 描述确定垃圾回收侵入性的模式。
[弱引用](weak-references.md) | 描述允许应用程序访问对象的同时也允许垃圾回收器收集相应对象的功能。
 
## <a name="reference"></a>参考

[System.GC](xref:System.GC)

[System.GCCollectionMode](xref:System.GCCollectionMode)

[System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode)

[System.Runtime.GCSettings](xref:System.Runtime.GCSettings)

[GCSettings.LargeObjectHeapCompactionMode](xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode)

[Object.Finalize](xref:System.Object.Finalize)

[System.IDisposable](xref:System.IDisposable)

## <a name="see-also"></a>另请参阅

[清理未托管资源](unmanaged.md)


