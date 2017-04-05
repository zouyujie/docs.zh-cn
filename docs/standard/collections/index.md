---
title: "集合和数据结构"
description: "集合和数据结构"
keywords: ".NET、.NET Core"
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 9e70255a-c02a-4046-86b7-10c84bab2d38
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 30e53c38bd58e15668e01f2af79defb0a0918192
ms.lasthandoff: 04/05/2017

---

# <a name="collections-and-data-structures"></a>集合和数据结构

类似的数据在作为集合而存储和操作时通常可以得到更高效地处理。 可以使用 [System.Array](https://docs.microsoft.com/dotnet/core/api/System.Array) 类或 [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections)、[System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic) 或 [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间中的类来添加、删除和修改集合中的单个元素或某个范围的元素。

有两种主要的集合类型：泛型集合和非泛型集合。 泛型集合在编译时是类型安全的。 因此，泛型集合通常能提供更好的性能。 构造泛型集合时，它们接受类型参数，并在向该集合添加项或从该集合删除项时无需在 [Object](https://docs.microsoft.com/dotnet/core/api/System.Object) 类型间来回强制转换。 非泛型集合将项存储为 [Object](https://docs.microsoft.com/dotnet/core/api/System.Object)，并需要强制转换。 非泛型集合可能会出现在较旧代码中。

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间中的集合可提供高效的线程安全操作，以便从多个线程访问集合项。

## <a name="common-collection-features"></a>常用集合功能

所有集合都提供用于在集合中添加、删除或查找项的方法。 此外，所有直接或间接实现 [ICollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection) 接口或 [ICollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.ICollection-1) 接口的集合均共享这些功能： 

* **可枚举集合**

   .NET Framework 集合实现 [System.Collections.IEnumerable](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) 或 [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1)，以启用要循环访问的集合。 可将枚举器看作集合中可指向任何元素的可移动指针。 `foreach, in` 语句 (C#) 使用由 `GetEnumerator` 方法公开的枚举器并隐藏操作枚举器的复杂性。 此外，任何实现 [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1) 的集合均被视作可查询类型，可用 LINQ 查询。 LINQ 查询提供数据访问的一个通用模式。 它们通常比标准 foreach 循环更简洁、更具可读性，并提供筛选、排序和分组功能。 LINQ 查询还可提高性能。
    
* **可将集合内容复制到数组**

   可使用 `CopyTo` 方法将所有集合复制到数组中；但新数组中元素的顺序基于枚举器返回元素的顺序。 得到的数组始终是一维的，下限为零。
    
此外，许多集合类包含下列功能：

* **容量和计数属性**

   集合的容量是它可包含的元素数。 集合的计数是它实际所含的元素数。 某些集合隐藏容量、计数或将这两者都隐藏。
    
   达到当前容量时，大多数集合会自动扩展容量。 重新分配内存并将元素从旧集合复制到新集合。 这减少了要求使用集合的代码；但集合的性能可能会受到不利影响。 例如，对 [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) 来说，如果 `Count` 比 `Capacity` 少，那么添加项就是一项 O(1) 操作。 如需增加容量以容纳新元素，则添加项成为 O(n) 操作，其中 n 是 `Count`。 避免因多次重新分配而导致的性能较差的最佳方式是：将初始容量设置为集合的估计大小。 
    
   [BitArray](https://docs.microsoft.com/dotnet/core/api/System.Collections.BitArray) 是一种特殊情况；其容量与长度相同，而长度与计数相同。
    
*   **下限一致**

   集合的下限是其第一个元素的索引。 [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 命名空间中所有索引集合的下限均为零，这表示它们从 0 开始建立索引。 [Array](https://docs.microsoft.com/dotnet/core/api/System.Array) 默认下限为零，但使用 `Array.CreateInstance` 创建 `Array` 类的实例时可定义一个更低下限。

*   **用于从多个线程进行访问的同步**（仅 [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 类）。

   [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) 命名空间中的非泛型集合类型通过同步提供一些线程安全性；常通过 `SyncRoot` 和 `IsSynchronized` 成员公开。 这些集合不是默认为线程安全的。 如需对集合进行可扩展、高效的多线程访问，请使用 [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) 命名空间中的其中一个类或考虑使用不可变集合。 有关详细信息，请参阅[线程安全集合](threadsafe/index.md)。    
    
## <a name="choosing-a-collection"></a>选择集合 

一般情况下，应使用泛型集合。 下表介绍了一些常用的集合方案和可用于这些方案的集合类。 如果你是使用泛型集合的新手，此表将帮助你选择最适合你的任务的泛型集合。

我要…… | 泛型集合选项 | 非泛型集合选项
---------- | ---------------------------- | --------------------------------
将项存储为键/值对以通过键进行快速查找 | [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) | [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable)
按索引访问项 | [System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) | [System.Array](https://docs.microsoft.com/dotnet/core/api/System.Array), [System.Collections.ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList)
使用项先进先出 (FIFO) | [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) | [System.Collections.Queue](https://docs.microsoft.com/dotnet/core/api/System.Collections.Queue)
使用数据后进先出 (LIFO) | [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) | [System.Collections.Stack](https://docs.microsoft.com/dotnet/core/api/System.Collections.Stack)
按顺序访问项 | [System.Collections.Generic.LinkedList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1) | 无建议
删除集合中的项或向集合添加项时接收通知。 （实现 [INotifyPropertyChanged](https://docs.microsoft.com/dotnet/core/api/System.ComponentModel.INotifyPropertyChanged) 和 [INotifyCollectionChanged](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.INotifyCollectionChanged)） | [System.Collections.ObjectModel.ObservableCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.ObservableCollection-1) | 无建议
使用已排序的集合 | [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) | [System.Collections.SortedList](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList)
管理唯一元素的高效存储和访问 | [System.Collections.Generic.HashSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.HashSet-1), [System.Collections.Generic.SortedSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedSet-1) | 无建议

## <a name="related-topics"></a>相关主题

标题 | 描述
----- | -----------
[选择集合类](selecting-a-collection-class.md) | 描述不同的集合并帮助你为你的方案选择一个集合。
[常用的集合类型](commonly-used-collection-types.md) | 描述常用泛型和非泛型集合类型，例如 [System.Array](https://docs.microsoft.com/dotnet/core/api/System.Array)、[System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) 和 [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2)。 
[何时使用泛型集合](when-to-use-generic-collections.md) | 讨论泛型集合类型的使用。
[集合内的比较和排序](comparisons-and-sorts-within-collections.md) | 讨论在集合中使用等同性比较和排序比较。
[已排序的集合类型](sorted-collection-types.md) | 描述已排序集合的性能和特征。
[哈希表和字典集合类型](hashtable-and-dictionary-collection-types.md) | 描述泛型和非泛型基于哈希的字典类型的功能。
[线程安全集合](threadsafe/index.md) | 描述支持从多个线程进行安全有效的并发访问的集合类型，例如 [System.Collections.Concurrent.BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) 和 [System.Collections.Concurrent.ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1)。

## <a name="reference"></a>参考

[System.Array](https://docs.microsoft.com/dotnet/core/api/System.Array)

[System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections)

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic)

[System.Collections.Specialized](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized)

[System.Linq](https://docs.microsoft.com/dotnet/core/api/System.Linq)
  

