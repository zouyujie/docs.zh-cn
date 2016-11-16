---
title: "线程安全集合"
description: "线程安全集合"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 92d5515d-f5d6-4a09-8bbb-31865d678643
translationtype: Human Translation
ms.sourcegitcommit: cfe65fcba1b3fdc09ffcac704a760d8ce29ea60b
ms.openlocfilehash: 421d46585b5d83f5772fa6596ad581c8c6acbf71

---

# <a name="threadsafe-collections"></a>线程安全集合

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间包含多个线程安全且可缩放的集合类。 多个线程可以安全高效地从这些集合添加或删除项，而无需在用户代码中进行其他同步。 编写新代码时，只要将集合同时写入多个线程中，就使用并发集合类。 如果仅从共享集合进行读取，则可使用 [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic) 命名空间中的类。 建议不要使用 [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 集合类，除非需要以 .NET Framework 1.1 或早期版本的运行时为目标。

## <a name="finegrained-locking-and-lockfree-mechanisms"></a>细粒度锁定和无锁机制

某些并发集合类型使用的是轻量同步机制，如 [SpinLock](https://docs.microsoft.com/dotnet/core/api/System.Threading.SpinLock)、[SpinWait](https://docs.microsoft.com/dotnet/core/api/System.Threading.SpinWait)、[SemaphoreSlim](https://docs.microsoft.com/dotnet/core/api/System.Threading.SemaphoreSlim) 和 [CountdownEvent](https://docs.microsoft.com/dotnet/core/api/System.Threading.CountdownEvent)。 通常，这些同步类型在将线程置于实际 `Wait` 状态之前会在短时间内使用“繁忙旋转”。 预计等待时间非常短时，旋转比等待所消耗的计算资源少得多，因为后者涉及资源消耗量大的内核转换。 对于使用旋转的集合类，这种效率意味着多个线程能够以非常快的速率添加和删除项。

[ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) 和 [ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) 类根本不使用锁定。 相反，它们依赖互锁操作来实现线程安全性。

> [!NOTE]
> 由于并发集合类支持 [ICollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection)，因此该类可提供针对 `IsSynchronized` 和 `SyncRoot` 属性的实现，即使这些属性不相关。 `IsSynchronized` 始终返回 `false`，而 `SyncRoot` 始终为 null。

下表列出了 [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间中的集合类型。

类型 | 描述
---- | -----------
[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) | 对实现 [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1) 的任何类型提供限制和阻止功能。 有关详细信息，请参阅 [BlockingCollection 概述](blockingcollection-overview.md)。
[ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1) | 无序元素集合的线程安全实现。
[ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) | 键值对字典的线程安全实现。
[ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) | FIFO（先进先出）队列的线程安全实现。
[ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) | LIFO（后进先出）堆栈的线程安全实现。
[IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1) | 类型必须实现以在 `BlockingCollection` 中使用的接口。

## <a name="thread-synchronization-in-the-net-framework-version-10-and-20-collections"></a>.NET Framework 1.0 和 2.0 版集合中的线程同步

可以在 [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 命名空间找到 .NET Framework 1.0 版首次引入的集合。 这些集合（包括常用的 [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList) 和 [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable)）通过 `Synchronized` 属性（此属性以集合为基础返回线程安全包装器）提供一些线程安全性。 该包装器通过对每个添加或删除操作锁定整个集合进行工作。 因此，每个尝试访问集合的线程必须等待，直到轮到它获取锁定。 这不可缩放，并且可能导致大型集合的性能显著下降。 此外，这一设计并不能完全防止争用情况的出现。 

可以在 [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic) 命名空间找到 .NET Framework 2.0 版首次引入的集合类。 这些集合类包括 [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1)、[Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 等。 与 `System.Collections` 类相比，这些类提供的类型安全性和性能更高。 不过，`System.Collections.Generic` 集合类不提供任何线程同步；同时在多个线程上添加或删除项时，用户代码必须提供所有同步。

建议使用 `System.Collections.Concurrent` 集合类，因为它们不仅提供 `System.Collections.Generic` 集合类的类型安全性，还提供比 `System.Collections` 集合所提供的线程安全性更高效完整的线程安全性。

## <a name="related-topics"></a>相关主题

标题 | 描述
----- | -----------
[BlockingCollection 概述](blockingcollection-overview.md) | 描述 `BlockingCollection<T>` 类型提供的功能。
[何时使用线程安全集合](when-to-use-a-thread-safe-collection.md) | 说明何时适合使用线程安全集合。
[如何：在 ConcurrentDictionary 中添加和移除项](how-to-add-and-remove-items.md) | 描述如何从 `ConcurrentDictionary<TKey, TValue>` 添加和删除元素。
[如何：在 BlockingCollection 中逐个添加和取出项](how-to-add-and-take-items.md) | 描述如何在不使用只读枚举器的情况下，从阻止的集合添加和检索项。
[如何：向集合添加限制和阻塞功能](how-to-add-bounding-and-blocking.md ) | 描述如何将任一集合类用作 `IProducerConsumerCollection<T>;` 集合的基础存储机制。
[如何：使用 ForEach 移除 BlockingCollection 中的项](how-to-use-foreach-to-remove.md ) | 描述如何使用 `foreach` 删除阻止集合中的所有项。
[如何：在管道中使用阻塞集合的数组](how-to-use-arrays-of-blockingcollections.md) | 描述如何同时使用多个阻塞集合来实现一个管道。
[如何：使用 ConcurrentBag 创建目标池](how-to-create-an-object-pool.md) | 演示如何使用并发包在可重用对象（而不是继续创建新对象）的情况下改进性能。

## <a name="reference"></a>参考

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)






 





<!--HONumber=Nov16_HO3-->


