---
title: "何时使用线程安全集合"
description: "何时使用线程安全集合"
keywords: ".NET、.NET Core"
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a2a42d44-f6a5-4f16-9000-026221d66349
translationtype: Human Translation
ms.sourcegitcommit: e07788926a995b41571be276379ad9285747951d
ms.openlocfilehash: 74f421a5badd9f2c7bf10fa1dfdf98161bba2ce8

---

# <a name="when-to-use-a-threadsafe-collection"></a>何时使用线程安全集合

`ConcurrentQueue`、`ConcurrentStack`、`ConcurrentDictionary`、`ConcurrentBag` 和 `BlockingCollection` 集合类型专门为支持多线程添加和删除操作而设计。 为了实现线程安全性，这些新类型使用多种高效的锁定和免锁定同步机制。 同步会增加操作的开销。 开销数取决于所用的同步类型、执行的操作类型和其他因素，例如尝试并行访问该集合的线程数。

在某些方案中，同步开销可忽略不计，使多线程类型的执行速度和缩放水平远远超过其受外部锁保护的非线程安全同等类型。 在其他方案中，开销可能会导致线程安全类型的执行速度和缩放水平与该类型外部锁定的非线程安全版本相同，甚至更差。

以下部分提供有关何时使用线程安全集合与其非线程安全同等集合（其读写操作受用户提供的锁定保护）的通用指南。 由于性能可能因多种因素而异，所以本指南并不针对某特定情况且不一定对所有情况都有效。 如果性能非常重要，那么确定要使用的集合类型的最佳方式是基于典型计算机配置和负载衡量性能。 本文档使用以下术语：

纯制造者-使用者方案：任何给定线程添加或删除元素，但二者不同时进行。

混合制造者-使用者方案：任何给定线程同时添加和删除元素。

加速：相对于同一方案中其他类型更快的算法性能。

可伸缩性：与计算机上的内核数成正比的性能提升。 一种可伸缩的算法，相比两个内核，八个内核上的执行速度更快。

## <a name="concurrentqueuelttgt-vs-queuelttgt"></a>ConcurrentQueue&lt;T&gt; 与 Queue&lt;T&gt;

在纯制造者-使用者方案中，每个元素的处理时间都非常短（几条指令），而 [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) 相比带有外部锁的 [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) 可提供适度的性能优势。 在此方案中，当某一专用线程排队，而另一专用线程取消排队时，`ConcurrentQueue<T>` 的性能最佳。 如果不强制执行此规则，那么 `Queue<T>` 在多内核计算机上的执行速度甚至可能稍快于 `ConcurrentQueue<T>`。 

处理时间大约为 500 FLOPS（浮点运算）或更长时，该双线程规则不适用于 `ConcurrentQueue<T>`，这将具有很好的可伸缩性。 `Queue<T>` 在此情况下无法正常伸缩。

在混合制造者-使用者方案中，处理时间非常短时，带外部锁的 `Queue<T>` 的伸缩性优于 `ConcurrentQueue<T>`。 但是，处理时间大约为 500 FLOPS 或更长时，`ConcurrentQueue<T>` 的伸缩性更佳。

## <a name="concurrentstack-vs-stack"></a>ConcurrentStack 与堆栈

在纯制造者-使用者方案中，当处理时间非常短时，[System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) 和带外部锁的 [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) 在使用一个专用推送线程和一个专用弹出线程时的执行性能可能大致相同。 但是，随着线程数的增加，这两种类型的执行性能会因争用增加而降低，并且 `Stack<T>` 的执行性能可能优于 `ConcurrentStack<T>`。 处理时间大约为 500 FLOPS 或更长时，这两种类型的伸缩速率大致相同。 

在混合制造者-使用者方案中，对于小型和大型工作负荷，`ConcurrentStack<T>` 的速度更快。

使用 `PushRange` 和 `TryPopRange` 可能会大大加快访问速度。

## <a name="concurrentdictionary-vs-dictionary"></a>ConcurrentDictionary 与词典

通常，在从多个线程中并行添加和更新键或值的任何方案中，会使用 [System.Collections.Concurrent.ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2)。 在涉及频繁更新和相对较少读取操作的方案中，`ConcurrentDictionary<TKey, TValue>` 通常具备一些优势。 在涉及许多读取和更新操作的方案中，`ConcurrentDictionary<TKey, TValue>` 通常在具备任意数量内核的计算机上运行速度更快。

在涉及频繁更新的方案中，可以提高 `ConcurrentDictionary<TKey, TValue>` 中的并发度，然后进行衡量，查看含有多个内核的计算机的性能是否有所提升。 如果更改并发级别，请尽可能避免全局操作。

如果仅读取键或值，则 [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) 的速度更快，因为如果字典未经任何线程修改，则不需要进行同步。

## <a name="concurrentbag"></a>ConcurrentBag

在纯制造者-使用者方案中，[System.Collections.Concurrent.ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1) 的执行速度可能慢于其他并发集合类型。

在混合制造者-使用者方案中，对于大型和小型工作负荷，相比其他任何并发集合类型，往往 `ConcurrentBag<T>` 的执行速度更快且伸缩性更佳。

## <a name="blockingcollection"></a>BlockingCollection

需要限制和阻止语义时，[System.Collections.Concurrent.BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 的执行速度可能优于任何自定义实现。 它还支持诸多取消、枚举和异常处理操作。

## <a name="see-also"></a>另请参阅

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[线程安全集合](index.md)



<!--HONumber=Nov16_HO1-->


