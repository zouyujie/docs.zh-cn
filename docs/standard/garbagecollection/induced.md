---
title: "被动回收"
description: "被动回收"
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3e09b9dd-a800-4e56-b468-619f910ae22e
translationtype: Human Translation
ms.sourcegitcommit: 213ce098bcc2b5e31c55e759d895254d5ca33caa
ms.openlocfilehash: a10822518f0687dc7bbb06dd0fb77f6d9a3196fb

---

# <a name="induced-collections"></a>被动回收

在大多数情况下，垃圾回收器可以确定执行回收的最佳时间，应让其独立运行。 在某些不常见的情况下，强制回收可以提高应用程序的性能。 在这些情况下，可以使用 [GC.Collect](xref:System.GC.Collect) 方法强制垃圾回收，引发垃圾回收。 

当应用程序代码中某个确定的点上使用的内存量大量减少时，请使用 [Collect](xref:System.GC.Collect) 方法。 例如，如果应用程序使用包含若干个控件的复杂对话框，则在对话框关闭时调用 [Collect](xref:System.GC.Collect) 可以通过立即回收该对话框占用的内存来提高性能。 请确保应用程序不会过于频繁地引发垃圾回收，否则当垃圾回收器无效率地尝试回收对象时，可能会使性能降低。 可为 [Collect](xref:System.GC.Collect) 方法提供 [GCCollectionMode.Optimized](xref:System.GCCollectionMode.Optimized) 枚举值，以便仅在回收能够带来效率时才进行回收，如下一部分所述。

## <a name="gc-collection-mode"></a>GC 回收模式

可以某个包含 [GCCollectionMode](xref:System.GCCollectionMode) 值的 [GC.Collect](xref:System.GC.Collect) 方法重载来指定强制回收的行为，如下所示。

GCCollectionMode 值 | 描述
---------------------- | ----------- 
[默认](xref:System.GCCollectionMode.Default) | 为正在运行的 .NET Framework 版本使用默认的垃圾回收设置。
[已强制](xref:System.GCCollectionMode.Forced) | 强制立即执行垃圾回收。 这相当于调用 [GC.Collect()](xref:System.GC.Collect) 重载。 它会导致对所有分代进行完全阻塞回收。 也可以在强制立即执行完全阻塞垃圾回收之前，通过将 [GCSettings.LargeObjectHeapCompactionMode](xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode) 属性设置为 [GCLargeObjectHeapCompactionMode.CompactOnce](xref:System.Runtime.GCLargeObjectHeapCompactionMode.CompactOnce) 来压缩大型对象堆。 
[已优化](xref:System.GCCollectionMode.Optimized) | 使垃圾回收器可以确定当前时间是否是回收对象的最佳时间。 垃圾回收器可能判定回收效率不够高，因此回收不合理，在这种情况下将返回而不回收对象。
 
## <a name="background-or-blocking-collections"></a>后台回收或阻塞回收

可以调用 [GC.Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) 方法重载，指定被动回收是否是阻塞性的。 执行的回收类型取决于该方法的 *mode* 和 *blocking* 参数组合。 *mode* 是 [GCCollectionMode](xref:System.GCCollectionMode) 枚举的成员，*blocking* 是一个[布尔](xref:System.Boolean)值。 下表汇总了 mode 和 blocking 自变量的交互。 

*模式* | *blocking* = true | *blocking* = false
------ | ----------------- | ------------------
[Forced](xref:System.GCCollectionMode.Forced) 或 [Default](xref:System.GCCollectionMode.Default) | 尽快执行阻塞回收。 如果后台回收正在进行并且分代为 0 或 1，[Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) 方法将立即触发阻塞回收，并在回收完成后返回。 如果后台回收正在进行，并且 generation 参数为 2，该方法将等到后台回收完成，触发分代 2 的阻塞回收，然后返回。 | 尽快执行回收。 [Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) 方法请求后台回收，但不保证请求成功；根据具体的环境，有时仍可执行阻塞回收。 如果后台回收正在进行，该方法将立即返回。 
[已优化](xref:System.GCCollectionMode.Optimized) | 可根据垃圾回收器和 generation 参数的状态执行阻塞回收。 垃圾回收器会尽量提供最佳性能。 | 根据垃圾回收器的状态，有时可执行回收。 [Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) 方法请求后台回收，但不保证请求成功；根据具体的环境，有时仍可执行阻塞回收。 垃圾回收器会尽量提供最佳性能。 如果后台回收正在进行，该方法将立即返回。 
 
## <a name="see-also"></a>另请参阅

[延迟模式](latency.md)

[.NET 中的垃圾回收](index.md)



<!--HONumber=Nov16_HO1-->


