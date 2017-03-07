---
title: "延迟模式"
description: "延迟模式"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 810bd8be-5a48-42c6-b080-3afdb31fc61b
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 1d99ac95527cae80b74c96f5a2e6be81b94176c5
ms.lasthandoff: 03/02/2017

---

# <a name="latency-modes"></a>延迟模式

若要回收对象，垃圾回收器必须停止应用程序中所有正在执行的线程。 在某些情况下（例如当应用程序检索数据或显示内容时），关键时刻可能发生完整的垃圾回收，从而妨碍性能。 可以通过将 [GCSettings.LatencyMode](xref:System.Runtime.GCSettings.LatencyMode) 属性设置为某个 [System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode) 值来调节垃圾回收的干扰。 

延迟指垃圾回收干扰应用程序的时间。 在低延迟期间，垃圾回收对正在回收的对象保守性更强、干扰性更弱。 [System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode) 枚举提供两种低延迟设置：

* [LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) 禁止第 2 代回收，仅执行第 0 代和第 1 代回收。 只能在短时间内使用。 在更长时间内，如果系统处于内存压力下，垃圾回收器将触发一次回收，这样会暂时暂停应用程序并中断对时间要求很急的操作。 此设置仅对工作站垃圾回收可用。 

* [SustainedLowLatency](xref:System.Runtime.GCLatencyMode.SustainedLowLatency) 禁止第 2 代前台回收，仅执行第 0 代、第 1 代回收和第 2 代后台回收。 它可以长时间使用，并对工作站和服务器垃圾回收都可用。 如果[并发垃圾回收](https://msdn.microsoft.com/library/yhwwzef8.aspx)已禁用，则无法使用此设置。

在低延迟期间，除非发生以下情况，否则禁止第 2 代回收：

* 系统收到操作系统的低内存通知。

* 应用程序代码通过调用 [GC.Collect](xref:System.GC.Collect(System.Int32)) 方法并将 generation 参数指定为 2 来包含回收。

下表列出了使用 [GCLatencyMode](xref:System.Runtime.GCLatencyMode) 值的应用程序方案。

延迟模式 | 应用程序方案
------------ | --------------------- 
[Batch](xref:System.Runtime.GCLatencyMode.Batch) | 对于不具有 UI 或服务器端操作的应用程序。 这是[并发垃圾回收](https://msdn.microsoft.com/library/yhwwzef8.aspx)被禁用时的默认模式。
[Interactive](xref:System.Runtime.GCLatencyMode.Interactive) | 对于具有 UI 的大多数应用程序。 对于不具有 UI 或服务器端操作的应用程序。 当[并发垃圾回收](https://msdn.microsoft.com/library/yhwwzef8.aspx)启用时，这是默认模式。
[LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) | 对于具有短期时效性操作（操作期间垃圾回收器的干扰可能会引起中断）的应用程序。 例如执行动画呈现或数据采集函数的应用程序。
[SustainedLowLatency](xref:System.Runtime.GCLatencyMode.SustainedLowLatency) | 适用于在有限但有可能更长的时间内具有时效性操作并且在此期间垃圾回收器中断具有破环性的应用程序。 例如，需要随着交易时间内的市场数据变化做出快速响应的应用程序。   此模式会比其他模式产生更大的托管堆大小。 由于它不压缩托管堆，因此可能产生更多碎片。 确保有足够的可用内存。
 
## <a name="guidelines-for-using-low-latency"></a>低延迟使用指南

使用 [LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) 模式时，请注意以下指导原则：

* 尽可能地缩短低延迟时段。

* 避免在低延迟时段分配大量内存。 由于垃圾回收回收的对象较少可能出现低内存通知。 

* 在低延迟模式下，最大限度减少分配次数，尤其是大型对象堆和固定对象上的分配。 

* 知道可以分配的线程。 由于 [LatencyMode](xref:System.Runtime.GCSettings.LatencyMode) 属性设置属于进程范围的设置，因此可以在可分配的任何线程上生成 [OutOfMemoryException](xref:System.OutOfMemoryException)。 

* 在低延迟期间，可以通过调用 [GC.Collect(Int32, GCCollectionMode)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode)) 方法强制进行第 2 代回收。

## <a name="see-also"></a>另请参阅

[System.GC](xref:System.GC)

[已引发回收](induced.md)

[.NET 中的垃圾回收](index.md)

